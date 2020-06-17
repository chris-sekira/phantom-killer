# phantom-killer
[phantom-killer.ps1](powershell/phantom-killer.ps1) is a simple cross-platform Powershell script to safely close lingering (zombie) processes that have been abandoned by their previously-closed parent process. This script only kills processes without a parent, while leaving other instances alone.

## About
### Purpose
Sometimes programs create child processes, and sometimes those parent processes die without cleaning up their children -- producing zombies! Then you're stuck wondering why you're magically out of RAM, or why you can't delete a folder because _"child.exe is being used by another program"_.

Instead of having to open Task Manager, find the process, and terminate them manually, this script will do it for you!

### Compatibility
This script works with both Windows "Desktop" Powershell and the newer Powershell "Core" on Windows/Linux without any additional dependencies. It has been specifically verified with:
- Desktop (Windows)
    - Powershell 5.1
- Core (Windows/Linux)
  - Powershell Core 6.0
  - Powershell Core 6.1
  - Powershell 7.0 (LTS)

#### Note:
Prior to Powershell 6.0, the `Get-Process` cmdlet lacked the ability to return information about the parent process, requiring a lengthy workaround using `Get-CimInstance` calls. Starting with Powershell 6.0, all of the logic can be reduced down to a simple 1-line statement of
```powershell
# $ProcessName contains the name of the zombie process, without the extension (ie: phantomjs, PlexTranscoder, ...)
Get-Process -Name $ProcessName -ErrorAction SilentlyContinue | Where-Object { ($null -eq $_.Parent) -or $($_.Parent.HasExited) }
```

## Usage and Help
Download [phantom-killer.ps1](powershell/phantom-killer.ps1), open `powershell` or `pwsh`, and run `Get-Help ./phantom-killer.ps1` to see usage info
### Get PowerShell Help
Use the built-in help info from PowerShell for usage, parameters, etc.
```shell
PS C:\> Get-Help .\phantom-killer.ps1
```
### See what will be terminated with a dry-run

As a sanity check it's always good to see what processes will be killed, this will list all `phantomjs` processes that would be killed off
```shell
PS C:\> .\phantom-killer.ps1 -ProcessName 'phantomjs' -DryRun
```

### Kill some Zombie Processes
```shell
PS C:\> .\phantom-killer.ps1 -ProcessName 'phantomjs'
```

## Misc
### Why is it called "Phantom Killer"?
Because 95% of the times that I use this script, it's for rogue `phantomjs.exe` processes.

## Contributing
For now, just open up an issue or submit a PR

