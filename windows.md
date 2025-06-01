# Install Starship Windows PowerShell
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
-------------------------------------------------------

# Install Starship PowerShell 7
Thanks for the detailed error — this happens when you accidentally **run the `$PROFILE` path as a command**, instead of opening it with an editor.

---

### ✅ Correct way to open (or create) your PowerShell 7 profile

#### 🔁 You're probably doing this (incorrect):

```powershell
C:\Users\marius\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
```

Which tries to **run** the file — that’s why you see that error.

---

### ✅ Instead, do this step-by-step:

#### 1. **Create the folder (if missing):**

```powershell
New-Item -Type Directory -Path (Split-Path -Parent $PROFILE) -Force
```

#### 2. **Create the profile file:**

```powershell
New-Item -Path $PROFILE -ItemType File -Force
```

#### 3. **Open the file in Notepad:**

```powershell
notepad $PROFILE
```

#### 4. **Paste this inside the file:**

```powershell
Invoke-Expression (&starship init powershell)
```

#### 5. **Save the file and restart PowerShell 7 (`pwsh`)**

You should now see the **Starship pastel powerline prompt** in your PowerShell 7 session.

---

Let me know if you'd like to do this in **WSL Ubuntu** next or set this as default in Windows Terminal.

https://learn.microsoft.com/en-us/windows/wsl/setup/environment
