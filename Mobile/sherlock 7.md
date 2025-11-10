Category: Mobile

Points: 500
### Description
The suspect maintains a list of victims ensnared by ransomware, which he consults on a dashboard within a web application called "hackbook" to determine if any of his victims are willing to comply with the ransom he has imposed. How many victims has the suspect successfully coerced into paying the demanded ransom?

Flag format : `SADC{xxxxxxxxxxx}`

---
### File
[data.rar](https://drive.google.com/file/d/1fPd0ecbXzJLDVQrMqIA-yHX-rWopXSwH/view?usp=drive_link) (It's the same file as in sherlock 1)

---
### Solution
Let's use `grep` on the extracted archive with the pattern `hackbook` and seen what we get.

#### Command

```sh
grep -rIi "hackbook" .
```

We got a bunch of results, but this folder caught my attention.

![](attachments/Pasted%20image%2020251110202323.png)

Folder path : `./data/com.android.chrome/cache/Offline\ Pages/archives/`

Let's jump there with `cd` and open `thunar`.

![](attachments/Pasted%20image%2020251110202501.png)

We can see some `MHTML` files. The file that contains the answer to our questions is `e9abe359-4a40-4765-baf8-103e7f9bc851.mhtml`. Opening it led to a web page : 

![](attachments/Pasted%20image%2020251110203237.png)

From this, we know the suspect is named **Lucas** and he has **3** victims.

Flag: `SADC{3}`

GG!