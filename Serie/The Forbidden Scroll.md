Category: Serie

Points: 400

Authors: Barracuda0x01, foundhack
### Description
In the hidden village, a precious Forbidden Scroll has been stolen and hidden deep within the maze. This ancient labyrinth is protected by explosive tags placed according to an ancient mathematical pattern that only the wisest shinobi can decipher. You are part of Team 7 tasked with recovering the scroll. Goodluck !!!

**Flag format:** `SADC{...}`

---
### Solution
To solve it, you will need to find the `crackme` present in the chall [The Forbidden Scroll](The%20Forbidden%20Scroll.md).
Since I already found it, you can download it [here](https://drive.google.com/file/d/1jmIOsH53tBa74pCNMqQ90kN_JSA-XMQW/view?usp=drive_link).

After running the `crackme` binary, I noticed that it was a `Minesweeper game`

![](attachments/Pasted%20image%2020251108222638.png)

But I figured out that we don't need to play it. Just use the command `strings` on the crackme.

```sh
strings crackme | grep -i SADC
```

![](attachments/Pasted%20image%2020251108222851.png)

Flag: `SADC{RU57_M@Z3_M@573R_0x15}`

GG!