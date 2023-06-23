## Hi there 👋
![Red-Ish Logo](![radish-flat-icon-colorful-logo-vector-16961539](https://github.com/Red-team-401d6/.github/assets/123131865/c31b12b0-712c-4bd0-a4cc-aa443587993c)
)

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
| 22    | ssh              |                                                                      |                                                                                                      |
| 80    | http             | Misconfiguration of web application, SQL injection                   |                                                                                                      |
| 8089  | unknownkali      |                                                                      |                                                                                                      |

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


### Host 10.0.0.197 Process Documentation


### 3.5. Reporting & Recomendations

Finally, this is where will  prepare a report detailing your findings, including the vulnerabilities detected and the potential impact. The report might also include recommendations for mitigating the detected vulnerabilities.
