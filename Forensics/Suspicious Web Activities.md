Category: Forensics 

Points: 100
### Description
You are a cybersecurity analyst tasked with investigating a suspected security breach on a web server. The server's access.log file contains records of HTTP requests and server responses. Your goal is to examine this log file and answer a series of questions to piece together the sequence of events and identify the attack vector used by the attacker.

1. What is the IP address of the attacker?
2. What tool did the attacker use to scan for open ports and services?
3. What tool did the attacker use to search for endpoints on the web application?Format (tool/version)
4. What other exploitation tool did the attacker tried to use to exploit the application?Format (tool/version)
5. What endpoint did the other used to exploit the target? Format(/name/file)
6. What vulnerability did the attacker exploit to gain access to the target? Format(Name)

Flag format: `SADC{1_2_3_4_5_6}`

---
### File
[access.log](https://drive.google.com/file/d/1LD9Tm3XI7cnvOus3wM5kGvRcUkRQIoyO/view?usp=drive_link)

---
### Solution
I used the shell and a text editor btw. I’m a forensics neophyte go easy on me please.

1. What is the IP address of the attacker?
   
   To answer to this question, I used the `IP` regex `(?:(?:\d|[01]?\d\d|2[0-4]\d|25[0-5])\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d\d|\d)(?:\/\d{1,2})?` with `grep`, `cut` and `uniq`
   
```sh
grep -P '(?:(?:\d|[01]?\d\d|2[0-4]\d|25[0-5])\.){3}(?:25[0-5]|2[0-4]\d|[01]?\d\d|\d)(?:\/\d{1,2})?' access.log | cut -d' ' -f2 | uniq
```

![](attachments/Pasted%20image%2020251109194006.png)

**Answer 1**: 141.44.201.11

2. What tool did the attacker use to scan for open ports and services?
   
   When we are looking at the logs, we can clearly see that `Nmap` was used.

![](attachments/Pasted%20image%2020251109194322.png)

**Answer 2**: Nmap

3. What tool did the attacker use to search for endpoints on the web application?Format (tool/version)
   
   I looked for tools like `dirb`, `ffuf` and `gobuster`.  I found `gobuster`

![](attachments/Pasted%20image%2020251109194650.png)

**Answer 3**: gobuster/3.5

4. What other exploitation tool did the attacker tried to use to exploit the application?Format (tool/version)

**Answer 4:** sqlmap/1.7.6

5. What endpoint did the other used to exploit the target? Format(/name/file)

**Answer 5:** /cgi-bin/statsconfig

6. What vulnerability did the attacker exploit to gain access to the target? Format(Name)

I found a line with `() { :; };`. This pattern is associated with the Bash vulnerability that leads to remote code execution `RCE`, known as `Shellshock`

![](attachments/Pasted%20image%2020251109195210.png)

**Answer 6:** Shellshock

Flag: 
`SADC{141.44.201.11_nmap_gobuster/3.5_sqlmap/1.7.6_/cgi-bin/statsconfig_Shellshock}`

GG!