Category: Forensics 

Points: 345

Author: foundhack
### Description
**Agent 47** and Diana have been tirelessly searching for what shifted in the shadows. Perhaps Agent 46 holds the key. Uncover the change and recover the flag.

Flag format : `SADC{...}`

---
### File
[Agent47](https://drive.google.com/file/d/1daLezRr_rjkVb1MVzBxEQpmpFpH5fdjt/view?usp=drive_link)

---
### Solution
After some analysis, I noticed that each pair of bytes in the file has been swapped. 

![](attachments/Pasted%20image%2020251109150005.png)

I used `dd` to reverse the initial operation made on the file.

![](attachments/Pasted%20image%2020251109150237.png)

```sh
dd if=Agent47 of=Agent47.png conv=swab
```

I got this image.

![](attachments/Agent47.png)

After some steg analysis, I found a corrupted chunk on the `Agent47.png` with `pngcheck`

![](attachments/Pasted%20image%2020251109150538.png)
To extract the corrupted chunk, we need his offset and is lenght. We can know it with `pngcheck -v`.

![](attachments/Pasted%20image%2020251109182051.png)

Let's extract it : 

```sh
tail -c +$((0x2e139 + 5240)) Agent47.png > corrupted.bin
```


We can input the `corrupted.bin` to [CyberChef](https://cyberchef.org) and decode it with the `ROT47 Brute force` recipe.

![](attachments/Pasted%20image%2020251109183609.png)

Holy steg !

Flag: `BattleCTF{Jo1n_the_4dv3nture_in_4fric@!58963}`

GG!