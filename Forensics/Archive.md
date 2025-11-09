Category: Forensic

Points: 100

Author: BJ SEC
### Description
Just archives...

---
### File
[ultimate_challenge.b64](https://drive.google.com/file/d/1U7Y_EKk8vaSphx7ZopqCR-069i0IALWe/view?usp=drive_link)

---
### Solution
The file is encoded to base 64. Let's decode it :

![](attachments/Pasted%20image%2020251109184323.png)

Command : `base64 -d ultimate_challenge > decoded`

After decoding it, I noticed that it was a multi-layer zipped file.

I used this command to automate the task : 

```sh
for i in $(seq 498 -1 0); do unzip -o layer_zip_$i.zip; done
```

After the last zip layer unzipped, I found another multi-layer archive file but this time, it was a tar archive.

![](attachments/Pasted%20image%2020251109190533.png)

I used this command to automates its extraction: 

```sh
for i in $(seq 499 -1 0); do tar -xf layer_$i.tar; done
```

The last layer contains the `flag.txt`. Now, my folder is a mess.

Flag: `SADC{th3_qu357_15_c0mpl3t3d_3njoy_your_g1f7_buddy}`

GG!