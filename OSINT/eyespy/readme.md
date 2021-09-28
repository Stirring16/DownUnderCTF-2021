# eyespy

>With the phone number you found, we were able to see their phone pinging off a cell tower. We intercepted their call and need to track down the registration number of the plane that their accomplice left on and and where the flight was heading. We recorded their call and were given the following transcript, can you analyse it for us?

> Flag format: DUCTF{plane-registration-number_flight destination}

> Author: xXl33t_h@x0rXx

[transcript19092021.pdf](https://github.com/Stirring16/DownUnderCTF-2021/files/7242028/transcript19092021.pdf)

# Chat analysis
 
![image](https://user-images.githubusercontent.com/62060867/135044587-21678f0a-02d6-4b7f-8bcd-82107e5254ab.png)

In this photo we have


Date: `19/09/202`

![image](https://user-images.githubusercontent.com/62060867/135044765-b9f6d80f-4ff6-48c0-a416-fa1144e64c7f.png)

Time: 14h30-14h37

![image](https://user-images.githubusercontent.com/62060867/135044921-da50376f-9e5b-45bb-80b6-708b3003cb5b.png)

And this photo we have

![image](https://user-images.githubusercontent.com/62060867/135045061-c33fb123-f5fd-400a-9147-af8d110734f1.png)

Where did he go: `Melbourne`

![image](https://user-images.githubusercontent.com/62060867/135045289-87694abc-f7ba-4b26-aae0-35778e96a62b.png)

Time: `15h06-15h12`

![image](https://user-images.githubusercontent.com/62060867/135045458-31cf9e1f-7e09-45a9-b868-1ffe05859ff3.png)

And duration of the flight: `An hour`

![image](https://user-images.githubusercontent.com/62060867/135045713-5d66ebc9-580b-421d-848b-de5e036c9dcc.png)

## Get Flag

So we have all the information about the flight: flight date, flight time, location, duration of the flight

Low take that [https://www.radarbox.com/data/airports/YMML?tab=arrivals](https://www.radarbox.com/data/airports/YMML?tab=arrivals)

look at the departure timing, I got it:

![image](https://user-images.githubusercontent.com/62060867/135046350-e04e2f54-5207-4cbc-b069-cd8cc63a44e9.png)

> So we got the flag: `DUCTF{VH-YIB_Melbourne}`








