# How to pronounce GIF

> Our machine that makes QR Codes started playing up then it just said "PC LOAD LETTER" and died. This is all we could recover...

> Author: xXl33t_h@x0rXx

![challenge](https://user-images.githubusercontent.com/62060867/134872353-05e72485-cb0c-477f-99cd-30cc21bffc4f.gif)

> ## Solution

We have the GIF animation. So we will need to reconstruct the QR in order to read it.

We can separate all the frames with [https://ezgif.com/](https://ezgif.com/)

![image](https://user-images.githubusercontent.com/62060867/134874098-d0109eb2-1239-4727-a0c5-4a07405339ca.png)

Now I can run this command to recreate each QR code:



> convert frame_010_delay-0.05s.gif frame_020_delay-0.05s.gif frame_030_delay-0.05s.gif frame_040_delay-0.05s.gif frame_050_delay-0.05s.gif frame_060_delay-0.05s.gifframe_070_delay-0.05s.gif frame_080_delay-0.05s.gif frame_090_delay-0.05s.gif frame_100_delay-0.05s.gif frame_110_delay-0.05s.gif -append QRcode1.png 


![image](https://user-images.githubusercontent.com/62060867/134876663-4c346e75-1304-4b89-9c4e-2253d3830183.png)

And similar the next 9. We have all the QR codes and we can see their content.

Or we can use this script which I read from another write up

```
from PIL import Image


images = [Image.new("RGB", size=(300, 21 * 12)) for i in range(10)]

for i in range(120):
	img = Image.open(f"frame{i + 1}.bmp")
	images[(i - 1) % 10].paste(img, (0, 21 * ((i - 1) // 10)))

for i in range(10):
	images[i].save(f"qr{i}.jpg")
```


![image](https://user-images.githubusercontent.com/62060867/134877447-034b1d88-bb11-47ad-9f30-246a0aff1d0b.png)

```
QRcode6: RFVDVEZ7YU1
QRcode8: fMV9oYVhYMHJfbjB3P30=
```

Concatenate them and decode base64. So we have flag





