Category: Serie

Points: 500

Authors: foundhack, Barracuda0x01 
### Description
Member of Team 7, you’re assisting a cybersecurity expert who between manga conventions prepared a test for the team. During one of his trips he hid an encrypted archive inside an image and sent you the file with one instruction: prove your OSINT and forensics skills.

**Note:** The flag is the checksum of the recovered crackme file.

**Flag format**:`SADC{checksum}`

---
### Hints
1: Why not look at the archives?
2: What about using Cupp dictionary to create a wordlist based on the informations ?

---
### Files
[screenshot.jpg](https://drive.google.com/file/d/1AIa_ZOlkWKX2jEs-nGEUN0Mt4iZIEFDG/view?usp=drive_link)

[final.png](https://drive.google.com/file/d/1iUFenucj4pbRzYPJA2SMfxx_hSL3Cn9_/view?usp=drive_link)

---
### Solution
First of all, I used `binwalk` to extract a zip archive hidden in the file `final.png`.

![](attachments/Pasted%20image%2020251108213341.png)

![](attachments/Pasted%20image%2020251108213705.png)

I tried to unzip the archive, but it was password‑protected, so I used `zip2john` to extract the hash and brute‑force it.

 ```sh
 zip2john 3EDF96.zip > hash
 ```

To generate a wordlist I used [cupp](https://github.com/Mebus/cupp) and the configuration shown in the `screeshot.jpg`.

---
#### Steps to generate the wordlist

After cloning the repo [cupp](https://github.com/Mebus/cupp), edit the file `cupp.cfg` by setting the variables`wcfrom` and `wcto` respectively to `20` and `30`.

![](attachments/Pasted%20image%2020251108215616.png)

![](attachments/Pasted%20image%2020251108214633.png)

 Run `cupp.py` and follow the configurations as in the `scrennshot` .  `DO NOT CHOOSE "Y" FOR THE HYPERSPEED PRINT YOU WILL WASTE TOUR TIME` . 

---
After running john with the  `ganymede.txt` wordlist, I found the password of the archive.

![](attachments/Pasted%20image%2020251108215949.png)

Password: `laughlinTristene%'#'@`

After extracting the archive, I found a bunch of `PNG` file. Sploiler: they’re basically a QR code that’s been split into multiple PNG pieces.

Using this script, I managed to reassemble the `QR code`.

```python
from PIL import Image
import os
import math
import re

# Folder storing the files
input_dir = "."

# Recover all the files img_XXX.png
files = sorted(
    [f for f in os.listdir(input_dir) if re.match(r"img_\d+\.png", f)],
    key=lambda x: int(re.findall(r"\d+", x)[0])
)

# tile size (25x25)
tile_size = 25

# Total number of tile
n = len(files)

# Automatic grid size deduction
grid_size = int(math.sqrt(n))
if grid_size * grid_size != n:
    print(f"[!] Attention : {n} morceaux -> {grid_size}x{grid_size} ne tombe pas juste")
    print("    Essaie manuellement avec une autre taille si l'image est mal assemblée.")
print(f"[+] Grille détectée : {grid_size}x{grid_size}")

# Creates an empty image
final_img = Image.new("RGBA", (tile_size * grid_size, tile_size * grid_size))

# Placement of pieces
for idx, file in enumerate(files):
    img = Image.open(os.path.join(input_dir, file))
    x = (idx % grid_size) * tile_size
    y = (idx // grid_size) * tile_size
    final_img.paste(img, (x, y))

# Saving
output_path = "reconstructed_qr.png"
final_img.save(output_path)
print(f"[+] QR code reconstruit -> {output_path}")
```


The `QR code`.

![](attachments/Pasted%20image%2020251108221229.png)

Scanning it lead us to a crackme on `MEGA`

![](attachments/Pasted%20image%2020251108221449.png)

If the crackme is no longer available on `MEGA`, you can download it [here](https://drive.google.com/file/d/1jmIOsH53tBa74pCNMqQ90kN_JSA-XMQW/view?usp=drive_link.)

The flag is the `SHA256` of the `crackme`. To find it, I used `sha256sum`

```sh
sha256sum crackme
```

Flag: `SADC{39d9c23da3504ef00dc22760977b8724b18123786efc28f6c6997472ec76bba1}`

GG!