Category: OSINT

Points: 100

Author: BJ SEC
### Description
The BJ SEC team invites you to explore their universe through a special mission. Locate the publication date of the LinkedIn post related to Code2Hack, follow the link to our CTF platform, then identify the creator of the challenge **Agentic**.

Flag format: `SADC{DDMMYYYY_CREATORNAME}`

Example: SADC{14022022_D4V3}

---
### Hints
No hint.


---
### Solution
I located **BJ SEC**’s LinkedIn profile using a basic Google search.

![](attachments/Pasted%20image%2020251108231844.png)

![](attachments/Pasted%20image%2020251108232006.png)

The first ever post published by `BJ SEC` about the `Code2Hack` was the correct one.

![](attachments/Pasted%20image%2020251108232509.png)

I extracted the post’s publication date using the online tool [LinkedIn Post Date Extractor](https://trevorfox.com/linkedin-post-date-extractor.html).

![](attachments/Pasted%20image%2020251108232816.png)


I also found their CTF platform : 

![](attachments/Pasted%20image%2020251108232941.png)

link `https://bjsec.xyz` 

After creating an account on the platform, I found the chall `Agentic`, an AI exploitation chall.

![](attachments/Pasted%20image%2020251108233706.png)

The author is `afrinic`.

Flag: `SADC{01042025_afrinic}`

GG!