## Hi there 👋
![image](https://github.com/Red-team-401d6/.github/assets/123131865/3a1972d2-7961-4c79-beea-be06b2dc1802)




<!--

**Here are some ideas to get you started:**

🙋‍♀️ A short introduction - what is your organization all about?
🌈 Contribution guidelines - how can the community get involved?
👩‍💻 Useful resources - where can the community find your docs? Is there anything else the community should know?
🍿 Fun facts - what does your team eat for breakfast?
🧙 Remember, you can do mighty things with the power of [Markdown](https://docs.github.com/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
-->
Red-ish Teams Penetration Test Report

## 1.0 Introduction
This report will contain all efforts that were conducted in order to gain access to the target network of 10.0.0.0/24. The purpose of this report is to keep track of the attacks and vulnerabilities that the Red-ish team finds on this network. 

### 1.2 Objective 
Our team was tasked with enumerating the target network (10.0.0.0/24) from a “black box” position starting w/ a foothold on a single endpoint (openvpn of 172.27.232.1). We must discover as many vulnerabilities as we can and document them. 

### 1.2 Requirements
We will find and document as many of the vulnerabilities as we can, we will also fill out this form to report fully on the tests applied. We will include
Overall High-Level Summary and Recommendations (non-technical)
Methodology walkthrough and detailed outline of steps taken.
Include screenshots, walkthrough, and sample code if applicable.

## 2.0 High-Level Summary



## 3.0 Methodologies



### 3.1. Reconnaissance (Information Gathering)
Here we focused mostly on nmap scans against these ip address

| 10.0.0.197 | 10.0.0.126 |
|------------|------------|
| 10.0.0.175 | 10.0.0.74  |
| 10.0.0.82  | 10.0.0.123 |

### 3.2. Scanning
During this methodology approach, we used Nmap as our port scanning tool. The goal is to identify live hosts, open ports, the nature of the services running on those ports, and the operating system of the hosts. 

|Nmap command | Switch | Target host |
|-------------|--------|-------------|
|Sudo nmap -A -sS -sV | sS, sV, sT, sU| 10.0.0.74 |
|Sudo nmap -A -sS -sV | sS, sV, A, O, | 10.0.0.82 |
|Sudo nmap -A -sS -sV | sS, sV, A, O  | 10.0.0.123|
|Sudo nmap -A -sS -sV | A, sS, sV     | 10.0.0.126|
|Sudo nmap -A -sS -sV | A, sS, sV     | 10.0.0.175|
|Sudo nmap -A -sS -sV | A, sS, sV     | 10.0.0.197|


### 3.3. Vulnerability Assessment
After the hosts, ports, services, and operating systems have been identified, you would move on to identifying potential vulnerabilities. Nmap itself is not a vulnerability scanner but it provides crucial information that can be used by vulnerability scanners.

### IP 10.0.0.82
| Port  | Service        | Vulnerability                                                  | Attack Method                                                                               |
|-------|----------------|---------------------------------------------------------------|---------------------------------------------------------------------------------------------|
| 21    | ftp            | Was able to gain access w/ credentials vagrant/vagrant. We may be able to escalate these tomorrow. | Use hydra to test log in credentials and then metasploit the ftp connection. Then drop a surprise message for the blue team. |
| 80    | http           |                                                               |                                                                                             |
| 3389  | ms-wbt-server  | Gained access with the above credentials.                      | Use hydra to gain credentials and either use rdesktop or metasploit to gain access.          |
| 49152 | msrpc          |                                                               |                                                                                             |
| 49153 | msrpc          |                                                               |                                                                                             |
| 49154 | msrpc          |                                                               |                                                                                             |
| 49155 | msrpc          |                                                               |                                                                                             |
| 49165 | msrpc          |                                                               |                                                                                             |


### IP 10.0.0.123
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|---------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 21    | ftp              | Was able to gain access w/ credentials vagrant/vagrant.              | Use hydra to test log in credentials and then metasploit the ftp connection. Then drop a surprise message for the blue team.                                 |
| 22    | ssh              | It’s Open to anyone from anywhere                                    | Once I get my public key in the directory I will ssh in.                                              |
| 80    | http             |                                                                     |                                                                                                      |
| 111   | rpcbind          | .                                                                   |                                                                                                      |
| 2049  | nfs              | Any IP address can access and place things in the Network Shared Folder. | Mount the directory to my machine, create user, add user to group w/ privileges to modify directory, add personal ssh key, ssh in.                    |
| 3389  | ms-wbt-server    | Gained access with the above credentials.                            | Use hydra to gain credentials and either use rdesktop or metasploit to gain access.                   |
| 49152 | msrpc            |                                                                     |                                                                                                      |
| 49153 | msrpc            |                                                                     |                                                                                                      |
| 49154 | msrpc            |                                                                     |                                                                                                      |
| 49155 | msrpc            |                                                                     |                                                                                                      |
| 49165 | msrpc            |                                                                     |                                                                                                      |
| 8089  | ssl/http splunkd httpd |                                                                      |                                                                                                      |


### IP 10.0.0.175
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 22    | ssh              |      is an open port, that is vulnerable to bruteforce attack        |     Brute force attack, using Hydra, Metasploit                                                                                                 |
| 80    | http             | Misconfiguration of web application, SQL injection                   | SQLI injection using burp suite and fuzzing technique using payload, dirbuster, sqlmap                                      |
| 8089  | ssl/http         |   is used for splunk to splunk and spluk web browing acitivy         | burp suite and metasploit                                                                                                      |

### IP 10.0.0.197
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 3389  | rdp | Network Level Authhentication(NLA) disable. Disabling NLA means that anyone can attempt to connect to the remote desktop without first providing valid credentials  | Brute force |

### IP 10.0.0.74
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 1900  | upnp | Universal Plug and Play (UPnP) protocol have been associated with several vulnerabilities in the past. | |
| 3389  | rdp | Network Level Authhentication(NLA) disable. Disabling NLA means that anyone can attempt to connect to the remote desktop without first providing valid credentials  | Brute force |

### IP 10.0.0.126
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 445   | smb | After a successful brute force, could be used to move laterally along the network.| All NetBIOS attacks |
| 3389  | rdp | Possible Misconfigurations | RDP |


Nmap has a scripting engine (NSE) that can execute scripts for more advanced service detection, vulnerability detection, and other types of reconnaissance.

### 3.4.  Exploitation

Once potential vulnerabilities have been identified, the next step would be to attempt to exploit these vulnerabilities. This might involve using tools such as Metasploit or manual techniques to exploit the identified vulnerabilities.

### Host 10.0.0.74 process Documentation
After running nmap scans we notice that port 3389 was open and was vulnerable.

<img width="314" alt="rdeskconnect" src="https://github.com/Red-team-401d6/Supporting-files/blob/main/Screenshot%20from%202023-06-25%2023-12-04.png">

We use metasploit rdp scanner to investigate further 

<img alt="rdeskconnect" src="https://github.com/Red-team-401d6/Supporting-files/blob/main/Screenshot%20from%202023-06-25%2023-17-55.png">

### Host 10.0.0.82 Process Documentation
First we noticed that ftp was open on port 21 and so was port 3389. 
With that info we know we need to run Hydra in an effort to get the log in credentials, we also noticed the name of the computer was vagrant so we figured we could try that as the user name as well
* Hydra:
  Bruteforce Attack.
  Hydra -L path/to/folder-of-usernames -P /path/to/folder-of-passwords 10.0.0.82 ftp
<img width="599" alt="Hydra 82attack" src="https://github.com/Red-team-401d6/.github/assets/108830695/e975348d-dc24-4e96-a21d-86b4fb8427ba">

Then I was able to use those creds to log into ftp on port 21

<img width="500" alt="ftp-connection" src="https://github.com/Red-team-401d6/.github/assets/108830695/8e35492c-5d97-48d9-877d-8325687da6bf">

and rdp on port 3389

<img width="314" alt="rdeskconnect" src="https://github.com/Red-team-401d6/.github/assets/108830695/e7c8ba64-e4fb-417b-a0ad-71c82e9f5531">


### Host 10.0.0.123 Process Documentation
Through Recon we discovered port 22 was open and nfs was up and running on 2049. With both of these open we decide to see what network file share we have access to
<img width="234" alt="showmount" src="https://github.com/Red-team-401d6/.github/assets/108830695/ad6846d4-36a3-4680-9150-5815e336752f">
This indicates the home/peter directory is mountable by anyone on the network. We start by creating a tmp directory to mount the home/peter directory to.
<img width="228" alt="mkdir" src="https://github.com/Red-team-401d6/.github/assets/108830695/8009c02e-24cf-4153-80fd-37b03d9c033c">

then we can mount that home/peter directory to the newly created /tmp/infosec directory

<img width="434" alt="mount" src="https://github.com/Red-team-401d6/.github/assets/108830695/0f3e35e0-92c9-422d-9069-da82431c34d6">

From here on the file directory that was /tmp/infosec has been changed to /mnt/peter2 as I had to start over and try again.Having created the directory and mounting the target machines nfs directory we can see what all is in there

<img width="510" alt="listpre" src="https://github.com/Red-team-401d6/.github/assets/108830695/6b69a6a2-b606-40c4-bfc2-4bb72e04b938">

After mounting the directory we can create a new group call it peter and associated it with the 1005 group 

<img width="370" alt="gadd" src="https://github.com/Red-team-401d6/.github/assets/108830695/70b7f6ca-e61e-45ee-9755-7461ea7b87d7">

Then we can add the user peter to that group and give him the user id of 1005 

<img width="544" alt="addpet" src="https://github.com/Red-team-401d6/.github/assets/108830695/bd42e444-8a31-4509-b6a2-45239d1013ee">

Now we can see the new group and user in said group
<img width="540" alt="listpost" src="https://github.com/Red-team-401d6/.github/assets/108830695/c993919d-ace4-4a17-ba1d-ff980ae642f3">

Then we just needed to switch to peter using;
‘su peter’
add a .ssh folder to hold our own ssh key using the following command;
Mkdir .ssh
Then we created a new ssh key as peter
<img width="439" alt="keygen" src="https://github.com/Red-team-401d6/.github/assets/108830695/2e7cadb4-b566-4dbf-8511-48b6aa6e6215">

Then we cd into the ssh folder and move our ssh public key to the mounted directory
“Cat ~/.ssh/id_rsa.pub >> /mnt/peter2/.ssh/authorized_keys”
Then I was able to ssh in as peter
<img width="526" alt="success" src="https://github.com/Red-team-401d6/.github/assets/108830695/ede83f66-6246-4042-a21b-b90879f9945e">

### Host 10.0.0.126 Process Documentation:


Attempted brute force attacks using 

Metasploit: Payload Delivery attempts executed using the following lines
	(use exploit/windows/smb/ms17_010_psexec)
	(use exploit/windows/smb/ms17_010_eternalblue)
	And their proceeding commands, RHOSTS, lhosts, etc...
Hydra: 
	Bruteforce Attacks attempts
	(hydra -L /home/kali/Desktop/TryTheseUSER.txt -P /home/kali/SecLists/Passwords/probable-v2-top1575.txt 10.0.0.126 smb -V -t4), 
	(hydra -L /home/kali/Desktop/TryTheseUSER.txt -P /home/kali/SecLists/Passwords/probable-v2-top207.txt 10.0.0.126 smb -V -t4)

Attempted to monitor traffic in hopes of acquiring login credentials or sensitive information using: 

Burp Suite: Interceptor proxy
Wireshark: ip.addr == 10.0.0.126


Reached a successful connection using kali terminal commands:


This command is an RDP brute force attack targeting an IP address, a single username, and a password list:(sudo python3 crowbar.py -b rdp -s 10.0.0.126/32 -u administrator -C /usr/share/wordlists/rockyou.txt)
This command allowed my RDP access to the host itself. rdesktop -u administrator 10.0.0.126 and then logged in with LongPass123. Successfully can now access the host remotely as administrator.

Was looking into running an ARPspoof to get information. However, that never came to fruition.

### Host 10.0.0.175 Process Documentation
After an extensive reconnaissance, we found out that the following ports are opened:
**Port 22**, which is been used for SSH, running an  Ubuntu 4ubuntu0.2 (Ubuntu Linux; protocol 2.0)
**Port  80**, which is used for http, running a Apache http 2.4.41 ((Ubuntu))
**Port 8089**, which is used for ssl/http, running a Splunkd http
Vulnerabilities that can be exploited

To exploit these, I consider the following approaches:using a bruteforce attack, to gain access to the target host

SSH (OpenSSH 8.2p1 Ubuntu 4ubuntu0.2): I attempted to brute force the SSH login using a tool like Hydra, John the Ripper, metasploits .  However I could not gain initial access to this machine.

**Hydra**: I used this command, hydra -l /home/kali/Downloads/SecLists/Usernames/top-usernames-shortlist.txt -P /home/kali/Downloads/SecLists/Passwords/500-worst-passwords.txt 10.0.0.175 ssh -t 4

**Metasploits**: using the following command:Here's an example of how you might use Metasploit to gain access to a system via SSH:
Start Metasploit: First, you need to launch Metasploit. You can do this by typing msfconsole in your terminal and pressing enter. Wait for Metasploit to load up.

Use SSH auxiliary scanner: Metasploit contains an auxiliary scanner for SSH. You can use it by typing use auxiliary/scanner/ssh/ssh_version.

Set the RHOSTS: Now you need to tell Metasploit which target or targets you want to scan. You can do this with the set RHOSTS command followed by the target IP address or addresses. For example, set RHOSTS 10.0.0.175.

Run the scanner: Now that everything is set up, you can run the scanner with the run or exploit command. 

**HTTP 80 (Apache http 2.4.41)**: You could look for web vulnerabilities. Run a tool like  Burp suite, dirbuster, sqlmap, to find potential vulnerabilities in the web application running on port 80. In addition, you can manually inspect the website for misconfigurations, insecure direct object references, SQL injection, etc.
**Dirbuster**: This are my findings:

**SQLMAP**: This are my findings sqlmap -u "http://10.0.0.175/simcorp/sqli_1.php?title=" --cookie="security_level=0; PHPSESSID=qc24358cjie3b9ero1tpt4nqus" --level=3 --risk=3 --random-agent --tamper=space2comment --time-sec=15 --delay=1 --dbs

Ran Tamper set: sqlmap -u "http://10.0.0.175/simcorp/sqli_1.php?title=" --cookie="security_level=0; PHPSESSID=qc24358cjie3b9ero1tpt4nqus" --level=3 --risk=3 --random-agent --tamper=space2comment --time-sec=15 --delay=1 --dbs. This are the result
**Result**:GET parameter I was able to we full access to all the database, username, Hashes, and was able to crack the hashes and get there password as well, using the hash values.

**WFUZZ** :Using this command, wfuzz -c -z file,/home/kali/Downloads/SecLists/Usernames/top-usernames-shortlist.txt --hc 404 http://10.0.0.175/FUZZ
**Result**: I was not able to inject anything.
**Overall Result**: I was unable to gain access using brute force attack.


**Splunkd http (Port 8089)**: Depending on the version of Splunk being used, there may be possible exploits. This port is typically used for Splunk-to-Splunk and Splunk web browsing activity. Splunk's REST API also listens on this port, and if poorly configured, may be vulnerable to attacks.

For each of these, I perform more in-depth scanning and analysis to identify potential vulnerabilities. Tools such as Burp suite, and metasploit  are helpful in identifying known vulnerabilities for the services detected.

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 34.57 seconds


I used Burp suit for injection on port 80: I try I try to use a authentication bypass to bypass the website authentication process,it was not successful, which is shown with the first screenshot below:

**Result**: .I was  able to confirmed a true positive with an SQLI injection, using  Fuzzing technique(White Box Fuzzing), I was able to found anomaly as a result of injecting payloads to  the search button after I created a user account on the website 

I also try to attack port 8089 which shows they are running  Splunk server on it, it was not  a success either, I used metasploit : 
Open Metasploit by typing msfconsole in the terminal.

You can search for available Splunk exploits by typing search splunk.

If an exploit for your specific version of Splunk is available, you can select it by typing use followed by the exploit name.

Set the target by typing set RHOSTS target_ip_address.

Set any other required options.

Run the exploit by typing exploit.
**Result**: Unable to get the session cookies.

### Host 10.0.0.197 Process Documentation


### Host 10.0.0.206 Process Documentation

### 3.5. Reporting & Recomendations

Finally, this is where will  prepare a report detailing your findings, including the vulnerabilities detected and the potential impact. The report might also include recommendations for mitigating the detected vulnerabilities.

### IP: 10.0.0.74

### IP: 10.0.0.82
***Port 21: (Open ftp)*** 
This should be set to only recieve connections from approved ip locations, as that will help to defend against attacks when an attacker has aquired log in credentials.  

***Port 80:(Open http)*** 
With port 80 being completly open you're vulnerable to DOS attacks or Buffer overflow attacks.

***Port 3389: (Open RDP)***
This should be set to only recieve connections from approved ip locations, as that will help to defend against attacks when an attacker has aquired log in credentials.  I gained entrance through this port.

**Remediations:** Filter http traffic through a firewall, Increase the password complexity and length requirements, set ports 21 and 3389 to recieve connections from specific IPs, apply Microsoft security updates to the IIS server.

### IP: 10.0.0.123
***Port 22: (Open-SSH)***
should be set to recieve connections from specific IP addresses to prevent breaches when a threatactor has aquired authentication credentials. Should update version of SSH to current version. I utilized this exact vulnerability to gain access to the system after getting my own ssh key into the network file share.

***Port 2049: (nfs)***
Update to the current nfs patch and set the directory to only be mountable be specific IPs so not just anyone can add to the directory.

### IP: 10.0.0.126 Report and Remediation Suggestions

#### Due to the vulnerable ports and lack of heavy credential security, this IP was highly susceptable to a Brute-Force attack as well as left little resistance to privilege escalation and access persistence.

Addressing vulnerabilities on ports 445 and 3389 requires the implementation of specific measures to effectively mitigate potential risks. Here are recommended remedies for each port:

***Port 445 (SMB):***

- Disable SMB version 1: It is crucial to disable SMBv1 as it is an outdated and vulnerable protocol. Ensuring that SMBv1 is deactivated on all systems is imperative to enhance security.

- Implement robust password policies: Enforce the use of strong, complex passwords to fortify defenses against successful brute force attacks. Encouraging users to employ passwords that combine uppercase and lowercase letters, numbers, and special characters is essential.

- Enable account lockout policies: Implementing account lockout policies that temporarily suspend user accounts after a specific number of failed login attempts adds an extra layer of protection against brute force attacks. This measure helps mitigate the risk of unauthorized access.

- Apply regular security patches: Consistently updating systems and applications with the latest security patches and updates is crucial. By doing so, known vulnerabilities can be promptly addressed, reducing the likelihood of exploitation.

- Implement network segmentation: Dividing the network into separate segments and restricting SMB traffic between them is a recommended practice. This segmentation limits the potential lateral movement within the network, thus containing the impact of a successful attack.

***Port 3389 (RDP):***

- Change the default RDP port: Modifying the default port for RDP from 3389 to a less predictable port enhances security by making it harder for attackers to identify and target the RDP service.

- Enforce strong passwords and account lockout policies: Requiring strong passwords for RDP accounts, incorporating a combination of diverse character types, and implementing account lockout policies act as deterrents against brute force attacks.

- Enable network-level authentication (NLA): Activating network-level authentication provides an additional layer of security by requiring users to authenticate before establishing an RDP session. This safeguard reduces the risk of unauthorized access.

- Implement two-factor authentication (2FA): Enabling 2FA for RDP adds an extra layer of authentication, making it significantly more challenging for attackers to gain unauthorized access. The combination of something the user knows (password) with something the user possesses (such as a token or mobile device) enhances security.

- Implement an RDP gateway: Deploying an RDP gateway or Remote Desktop Gateway (RD Gateway) allows for centralized control and access management for RDP sessions. This implementation provides an additional layer of security by effectively controlling and monitoring RDP connections.

##### In addition to these measures, adherence to general security best practices is vital. This includes regularly updating and patching systems, utilizing firewall rules to restrict access to necessary ports, deploying intrusion detection and prevention systems, and conducting frequent security audits and assessments. By following these practices, organizations can enhance their overall security posture and minimize the risk of exploitation.

### IP: 10.0.0.175
**Defending against SQL injection (SQLi) attacks** for host **10.0.0.175** requires implementing a set of best practices. These include **using prepared statements or parameterized queries**, **validating and sanitizing user inputs**, **following the principle of least privilege**, **whitelisting input filtering**, **avoiding dynamic SQL queries**, **practicing secure coding**, **utilizing a web application firewall**, **conducting regular security audits and testing**, **keeping software and libraries updated**, and **promoting security awareness and training**. By adhering to these practices, organizations can significantly reduce the risk of SQL injection vulnerabilities and bolster the security of their web applications.

### IP: 10.0.0.197

### IP: 10.0.0.206
