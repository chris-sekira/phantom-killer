# phantom-killer
A simple Powershell script to safely close zombie processes that have been abandoned while leaving other processes (with active parents) still running.

## About
Sometimes programs create child processes, and sometimes those parent processes die without cleaning up their children -- producing zombies! Then you're stuck wondering why you're magically out of RAM, or why you can't delete a folder because _"child.exe is being used by another program"_.

Instead of having to open Task Manager, find the process, and terminate them manually, this script will do it for you!

## Why is it called "Phantom Killer"?
Because 95% of the times that I use this script, it's for rogue `phantomjs.exe` processes.

## Usage
Download [phantom-killer.ps1](powershell/phantom-killer.ps1), open `powershell` or `pwsh`, and run `Get-Help ./phantom-killer.ps1` to see usage info
