Category:  Misc

Points: 200

Author: [BJ SEC](https://bjsec.xyz)
### Description
My keyboard just started doing what he wants ! I don't know what to do but this is what I wanna give you : OAEJ?F0g{jab{p34e{cy{m4bZ{I047+

---
### Solution
It is obviously the flag but it is encoded. The title of the chall makes us think about some keyboard encoding or something like that. After some digging, I found out it was a keyboard mapping. Let's use [dcode](https://www.dcode.fr/chiffre-changement-clavier) to find the flag.

I used the `automatic` decoding and found `sadc[y)U-CAN-R#$D-IT-M$N/-g)$&]` with the convertion `DVORAK` to `QWERTY`

![](attachments/Pasted%20image%2020251108211240.png)

I used the string `sadc[y)U-CAN-R#$D-IT-M$N/-g)$&]` with the same `automatic` decoding and it found the flag with the convertion `lowercase` to `uppercase`.

![](attachments/Pasted%20image%2020251108211649.png)

Flag : `SADC{Y0u_can_r34d_it_m4n?_G047}`

GG!