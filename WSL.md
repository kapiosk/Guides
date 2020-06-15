# WSL

List wsl instances and version

```powershell
wsl -l -v
```

Run wsl command from powershell

```powershell
wsl ls
```

Enable hyperv protection (will loose other vm functionality)

```powershell
bcdedit /set hypervisorlaunchtype auto
```

Disable hyperv protection (will loose WSL2/Sandbox)

```powershell
bcdedit /set hypervisorlaunchtype off
```
