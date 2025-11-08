Category: OSINT

Points: 100
### Description
Find the website where this email originated, search the events for the one that corresponds to SADC NextGenCyber CTF and ....flag

---
### Hints
No hint

---
### File
[hi.jpg](https://drive.google.com/file/d/1DEzZ2lyHeugWftuExm9l31ERuEVNP8C4/view?usp=drive_link)

---
### Solution
Using the google lens with the file `hi.jpg` lead us to a post made by `CybZan` about a platform called `CTF Radar`.

![](attachments/Pasted%20image%2020251108235107.png)

![](attachments/Pasted%20image%2020251108235217.png)

link: `https://ctf-radar.cybzan.com/`

I found the announcement of the `NextGeninCyber` on `CTF Radar`.
In the description  there is a `base64` encoded string. 

![](attachments/Pasted%20image%2020251108235538.png)

After decoding it, I found this message : 

![](attachments/Pasted%20image%2020251109000200.png)

After following the instructions in the message, I was able to receive the flag by email.

![](attachments/Pasted%20image%2020251109000509.png)

Flag: `SADC{w3lc0m3_t0_CTF-r4d4r__go0d_LUCK2329}`