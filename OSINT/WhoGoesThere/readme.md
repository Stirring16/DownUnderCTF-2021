# Who Goes There?
>Disclaimer: Please note that this storyline, including any previous or future additions are all fictional and created solely for this challenge as part of DownUnder CTF. These are real places however they have no association/affiliation to the event, you are not required to call any place or make contact with anyone, doing so may disqualify you from the event.

>Welcome to the team, glad you chose to join us - hopefully you’ll like it here and want to stay. Let me tell you about your first task:

>We’ve observed an underground criminal RaaS operation calling back to this domain, can you find the number of the individual who registered the domain?

>646f776e756e646572.xyz

>Flag format is DUCTF{+61<number>}

>Author: xXl33t_h@x0rXx
  
## Solution

We are given this domain to find out the phone number of the registrar, `646f776e756e646572.xyz`
  
We can run a simple `whois` to obtain the URL from the domain.
  
  ![image](https://user-images.githubusercontent.com/62060867/135025321-28d680c4-7755-44c8-b202-478d7b59caa8.png)
  
And then use the whois from their service (namecheap), to obtain the phone number.
  
  ![image](https://user-images.githubusercontent.com/62060867/135025382-0c0d913a-f7ff-48e7-b34e-386e31988ebe.png)

 >  So we got the flag: `DUCTF{+61.420091337}`


