# Install Starship
1. Open PowerShell as Administrator (very important).
Run this command to set the execution policy for the current user only:
```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```
To make **Starship** load automatically every time you open **PowerShell**, you need to add the initialization command to your PowerShell profile script.

Here’s how you can do it:

### 🔧 Step-by-Step Guide

1. **Open PowerShell** as Administrator (optional, but safer for editing profile).

2. Check your PowerShell profile path:

   ```powershell
   $PROFILE
   ```

   This shows the path to your profile script, usually something like:

   ```
   C:\Users\YourName\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
   ```

3. **Create the file** if it doesn’t exist:

   ```powershell
   if (!(Test-Path -Path $PROFILE)) {
       New-Item -ItemType File -Path $PROFILE -Force
   }
   ```

4. **Edit the profile** file:

   ```powershell
   notepad $PROFILE
   ```

   Or use any editor you like (e.g., `code $PROFILE` if you have VS Code).

5. **Add this line to the bottom** of the file:

   ```powershell
   Invoke-Expression (&starship init powershell)
   ```

6. **Save and close** the editor.

7. Restart your terminal to see Starship in action.

Let me know if you also want to customize the Starship prompt or change the font to a Nerd Font like JetBrains Mono.


Great! Since you're on **Windows**, the path `~/.config/starship.toml` translates to:

```
C:\Users\<YourUsername>\.config\starship.toml
```

Here's how to apply the `pastel-powerline` preset properly:

---

### ✅ Step-by-step to apply `pastel-powerline` preset for Starship on Windows:

1. **Create the config folder (if it doesn’t exist):**

   Run this in PowerShell:

   ```powershell
   New-Item -ItemType Directory -Path "$HOME\.config" -Force
   ```

2. **Generate and save the preset:**

   Run this to generate the preset and save it:

   ```powershell
   starship preset pastel-powerline -o "$HOME\.config\starship.toml"
   ```

3. **(Optional) Edit your config:**

   You can open and tweak the config with:

   ```powershell
   notepad "$HOME\.config\starship.toml"
   ```

4. **Restart your terminal** to apply the changes.

---

You should now see the beautiful `pastel-powerline` prompt next time you open PowerShell or Windows Terminal.

Let me know if you want to customize anything in the prompt (like removing time, changing colors, etc).
----------------------------------------
That error means that **the WSL virtualization feature isn't enabled** or **the required Windows services aren’t running**, specifically the **Hyper-V services** needed for WSL 2.

Let’s fix it step by step:

---

## ✅ Fix WSL Error: `HCS_E_SERVICE_NOT_AVAILABLE`

### 1. **Check Windows Version**

WSL 2 requires:

* **Windows 10** (version 2004 or later) with **Build 19041+**
* **Windows 11** – all versions supported

Check with:

```powershell
winver
```

---

### 2. **Enable Required Features**

Open **PowerShell as Administrator** and run:

```powershell
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
```

Optional but recommended (especially for Docker):

```powershell
dism.exe /online /enable-feature /featurename:HypervisorPlatform /all /norestart
```

Then **restart your computer**.

---

### 3. **Check BIOS for Virtualization Support**

Make sure the following are **enabled** in BIOS/UEFI:

* **Intel VT-x** or **AMD-V**
* **Virtualization Technology**

---

### 4. **Reinstall WSL (if needed)**

If it's still not working, try reinstalling WSL:

```powershell
wsl --unregister Ubuntu
wsl --uninstall
wsl --install
```

---

### 5. **Start Fresh**

After reboot:

```powershell
wsl --install -d Ubuntu
```

---

Let me know if you want help setting up **Docker, DDEV, or Node** inside WSL once it’s working.

