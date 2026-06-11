---
---

You can automate a repeatable setup for Windows Sandbox by using:

1. A `.wsb` sandbox config file
2. A startup PowerShell script
3. A shared host folder containing installers/scripts

That way, every time the sandbox opens, it automatically installs apps, downloads files, maps folders, and launches your environment.

List of what to install :
'''
opera
.net
sublime text and/or vs studio
cursor
git
notepad ++
'''

how to reduce boilerplate
'''
insignify
'''

---

# 1. Enable Windows Sandbox

Requirements:

* Windows 10/11 Pro, Enterprise, or Education
* Virtualization enabled in BIOS

Enable it:

1. Press `Win + R`
2. Run:

```powershell
optionalfeatures
```

3. Enable:

* Windows Sandbox

Reboot.

---

# 2. Create a Shared Host Folder

Example:

```text
C:\SandboxSetup
```

Put inside:

* installers
* scripts
* portable apps
* config files

Example structure:

```text
C:\SandboxSetup
│
├── setup.ps1
├── apps\
│   ├── vscode.exe
│   ├── chrome.exe
│   └── git.exe
└── files\
```

---

# 3. Create the Startup Script

Example `setup.ps1`:

```powershell
# Create folders
New-Item -ItemType Directory -Force -Path "C:\Tools"

# Install apps silently
Start-Process "C:\Users\WDAGUtilityAccount\Desktop\SandboxSetup\apps\vscode.exe" -ArgumentList "/silent" -Wait
Start-Process "C:\Users\WDAGUtilityAccount\Desktop\SandboxSetup\apps\git.exe" -ArgumentList "/VERYSILENT" -Wait

# Download files automatically
Invoke-WebRequest `
  -Uri "https://example.com/file.zip" `
  -OutFile "C:\Tools\file.zip"

# Open apps
Start-Process "code"
Start-Process "notepad"

Write-Host "Environment Ready"
```

---

# 4. Create the `.wsb` Config File

Example `DevSandbox.wsb`:

```xml
<Configuration>

  <MappedFolders>
    <MappedFolder>
      <HostFolder>C:\SandboxSetup</HostFolder>
      <SandboxFolder>C:\Users\WDAGUtilityAccount\Desktop\SandboxSetup</SandboxFolder>
      <ReadOnly>false</ReadOnly>
    </MappedFolder>
  </MappedFolders>

  <LogonCommand>
    <Command>powershell.exe -ExecutionPolicy Bypass -File "C:\Users\WDAGUtilityAccount\Desktop\SandboxSetup\setup.ps1"</Command>
  </LogonCommand>

</Configuration>
```

Now double-click the `.wsb` file.

The sandbox will:

* open
* mount your setup folder
* run the script automatically
* install/download/open everything

---

# 5. Faster Method: Use Winget

Instead of storing installers manually, use Windows Package Manager.

Example:

```powershell
winget install Microsoft.VisualStudioCode -e
winget install Git.Git -e
winget install Google.Chrome -e
```

This is usually the cleanest solution.

---






# Recommended Setup

Best practical structure:

```text
C:\SandboxSetup
│
├── DevSandbox.wsb
├── setup.ps1
├── apps\
├── configs\
├── projects\
└── portable\
```

Double-click `DevSandbox.wsb` and your environment rebuilds automatically in ~1–3 minutes.
