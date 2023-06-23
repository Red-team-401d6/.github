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
| 445   | smb | | |
| 3389  | rdp | | |

### IP 10.0.0.74
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 135   | rcp  | | |
| 139   | netbios | | |
| 445   | smb | | |
| 3389  | rdp | | |

### IP 10.0.0.126
| Port  | Service          | Vulnerability                                                        | Attack Method                                                                                        |
|-------|------------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------------------|
| 445   | smb | After a successful brute force, could be used to move laterally along the network.| All NetBIOS attacks |
| 3389  | rdp | Possible Misconfigurations | RDP |


Nmap has a scripting engine (NSE) that can execute scripts for more advanced service detection, vulnerability detection, and other types of reconnaissance.

### 3.4.  Exploitation

Once potential vulnerabilities have been identified, the next step would be to attempt to exploit these vulnerabilities. This might involve using tools such as Metasploit or manual techniques to exploit the identified vulnerabilities.

### Host 10.0.0.74 process Documentation


### Host 10.0.0.82 Process Documentation
First we noticed that ftp was open on port 21 and so was port 3389. 
With that info we know we need to run Hydra
* Hydra:
  Bruteforce Attack.
  Hydra -L path/to/folder-of-usernames -P /path/to/folder-of-passwords 10.0.0.82 ftp

Then I was able to use those creds to log into both ftp and through rdp on port 3389



### Host 10.0.0.123 Process Documentation
Through Recon we discovered port 22 was open and nfs was up and running on 2049. With both of these open we decide to see what network file share we have access to
This indicates the home/peter directory is mountable by anyone on the network. We start by creating a tmp directory to mount the home/peter directory to. 
 then we can mount that home/peter directory to the newly created /tmp/infosec directory

From here on the file directory that was /tmp/infosec has been changed to /mnt/peter2 as I had to start over and try again.Having created the directory and mounting the target machines nfs directory we can see what all is in there

After mounting the directory we can create a new group call it peter and associated it with the 1005 group 

Then we can add the user peter to that group and give him the user id of 1005 

Now we can see the new group and user in said group

Then we just needed to switch to peter using;
‘su peter’
add a .ssh folder to hold our own ssh key using the following command;
Mkdir .ssh
Then we created a new ssh key as peter

Then we cd into the ssh folder and move our ssh public key to the mounted directory
“Cat ~/.ssh/id_rsa.pub >> /mnt/peter2/.ssh/authorized_keys”
Then I was able to ssh in as peter


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

**SQLMAP**: This are my findings sqlmap -u "http://192.168.1.250/?p=1&forumaction=search" --dbs

Ran Tamper set: sqlmap -u "http://10.0.0.175/?p=1&forumaction=search" '--tamper=space2comment' . This are the result
**Result**:GET parameter 'forumaction' does not seem to be injectable

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


### 3.5. Reporting & Recomendations

Finally, this is where will  prepare a report detailing your findings, including the vulnerabilities detected and the potential impact. The report might also include recommendations for mitigating the detected vulnerabilities.
**Defending against SQL injection (SQLi) attacks** requires implementing a set of best practices. These include **using prepared statements or parameterized queries**, **validating and sanitizing user inputs**, **following the principle of least privilege**, **whitelisting input filtering**, **avoiding dynamic SQL queries**, **practicing secure coding**, **utilizing a web application firewall**, **conducting regular security audits and testing**, **keeping software and libraries updated**, and **promoting security awareness and training**. By adhering to these practices, organizations can significantly reduce the risk of SQL injection vulnerabilities and bolster the security of their web applications.

