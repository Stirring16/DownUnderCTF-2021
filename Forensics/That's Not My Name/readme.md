# That's Not My Name

> I think some of my data has been stolen, can you help me?

> Author: Conletz#5420

[notmyname.pcapng](https://drive.google.com/file/d/1CdQstrqDWuBMXRug81eQkhAmVHdRYPwU/view?usp=sharing)

# Analysis

We've been provided with a PCAP file, and based off the challenge has been led to believe some data exfiltration is at play. First thing that comes to mind for that topic is DNS exfiltration and tunneling

![image](https://user-images.githubusercontent.com/62060867/134886687-00f3e3e7-b4fa-4f62-bb12-7f69bbb6a7e9.png)

After running that search there's plenty of traffic that seems ordinary. However, by scrolling down further we can start to see a large amount of traffic to a suspicious domain and a different IP than the rest of the DNS traffic

`qawesrdtfgyhuj.xyz | 3.24.188.205`

![image](https://user-images.githubusercontent.com/62060867/134887098-3fd3c937-39fd-49aa-a21d-98b1791238f5.png)

By having a look at the UDP stream, we're able to see a large amount of back and forth traffic with the same stream, which is unsual for ordinary DNS traffic. To investigate further, we can use the commandline equivalent of wireshark - tshark, to extract all queries to a file called result.txt .

```tshark -nr notmyname.pcapng -Y "dns.flags.response == 0" -T fields -e dns.qry.name -e dns > result.txt```

Based on the outputs of the file, the subdomains appear to be hexed. So I wrote script python to convert it

```
import re
import binascii

with open('result.txt', 'r') as f:
    for name in f:
        m = re.findall('([a-z0-9\.]+)\.qawesrdtfgyhuj.xyz', name)
        if m:
            print binascii.unhexlify(m[0].replace('.', ''))
```
![image](https://user-images.githubusercontent.com/62060867/134888525-5838cef1-7674-404c-8c47-0814619c35d0.png)

So we got the flag
