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
