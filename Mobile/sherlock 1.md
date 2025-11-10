Category: Mobile

Points: 100
### Description
You are a member of a computer forensic investigation team, summoned to examine the cell phone of a suspected cybercriminal to uncover evidence of his wrongdoing.
The suspect impersonates a banking structure. What is the name of the structure ?

> Flag format : SADC{xxxxxxxxxxxxxxx}

---
### Files
[data.rar](https://drive.google.com/file/d/1fPd0ecbXzJLDVQrMqIA-yHX-rWopXSwH/view?usp=drive_link)

---
### Solution
We were provided with an archive named `data.rar`. Let's extract it. You can use whatever you prefer. I used the GUI of Kali linux😅.

After the extraction, we were left with a bunch of android folder.

![](attachments/Pasted%20image%2020251110195550.png)

If the suspect impersonates a banking structure, he might have launch a `phishing attack`. Let's search some email addresses in the dump with `grep` .

#### Syntax
```sh
grep -rI '@gmail\.com' .
```

I found a bunch of Gmail address. The suspect didn't even bother to register a domain. What a pity 😭.

![](attachments/Pasted%20image%2020251110200329.png)

The bank name that came up often was `YASOBANK`.

Flag: `SADC{yasobank}`

GG!