# Want to Play a Game?

>My PC has been infected! I need help finding out what happened. I managed to get a memory dump, not sure if that can help you?

>In order to recover from this infection, I need the following information:

>What is the name of the malware that infected my PC?
>What is the name of the persistence mechanism?
>What folder did the infection originate from?
>Flag format: DUCTF{lowerCaseMalwareName_persistenceName_originatingFolderName}

>You can download the memory dump [here](https://mirror.aarnet.edu.au/pub/DownUnderCTF/JacobsPC.7z)

>The file is password protected. The password is I83xOkTzeljDmpMmZWTi.

>Author: Conletz#5420

 ## Solution
 
 We are provided with a memdump to look for malware signs, the flag consists of 3 parts; the malware name, it’s persistence folder and the origin of infection..raw

First step is to determine the profile and OS of the memory dump - (with volatility)

```
/home/kali/Desktop/volatility/volatility -f JacobsPC.raw imageinfo                                   
Volatility Foundation Volatility Framework 2.6
INFO    : volatility.debug    : Determining profile based on KDBG search...
          Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_23418, Win2008R2SP1x64
                     AS Layer1 : WindowsAMD64PagedMemory (Kernel AS)
                     AS Layer2 : FileAddressSpace (/home/kali/Desktop/JacobsPC.raw)
                      PAE type : No PAE
                           DTB : 0x187000L
                          KDBG : 0xf80002848120L
          Number of Processors : 1
     Image Type (Service Pack) : 1
                KPCR for CPU 0 : 0xfffff8000284a000L
             KUSER_SHARED_DATA : 0xfffff78000000000L
           Image date and time : 2021-09-13 12:11:28 UTC+0000
     Image local date and time : 2021-09-13 22:11:28 +1000

```

With the new version downloaded I ran `imageinfo` to determine the profile that volatility would recommend, but failed to get any useful information. At this point I simply guessed that it was  Win7SP0x64 which worked, so ran with this profile and performed a `pstree` to list all running processes at the time of the memory dump, output shown below.

```
/home/kali/Desktop/volatility/volatility -f JacobsPC.raw --profile=Win7SP0x64 pstree 
Volatility Foundation Volatility Framework 2.6
Name                                                  Pid   PPid   Thds   Hnds Time
-------------------------------------------------- ------ ------ ------ ------ ----
............
. 0xfffffa8004604480:chrome.exe                      4724   3660     14    325 2021-09-13 11:36:27 UTC+0000
 0xfffffa8004df95b0:explorer.exe                     1148   2024     36   1006 2021-09-12 17:45:51 UTC+0000
. 0xfffffa8004561690:soffice.exe                     3748   1148      1     67 2021-09-12 17:57:02 UTC+0000
.. 0xfffffa80045d0920:soffice.bin                    5228   3748     11    443 2021-09-12 17:57:02 UTC+0000
. 0xfffffa8004e35b00:VBoxTray.exe                    1620   1148     15    149 2021-09-12 17:45:52 UTC+0000
. 0xfffffa8004f98b00:iexplore.exe                    2516   1148     11    586 2021-09-12 17:46:12 UTC+0000
.. 0xfffffa80029f65f0:iexplore.exe                   2280   2516     30    723 2021-09-12 17:46:47 UTC+0000
... 0xfffffa8001ad0b00:ie_to_edge_stu                3444   2280      0 ------ 2021-09-12 17:47:55 UTC+0000
 0xfffffa8001e9eb00:drpbx.exe                       3628   1152      4    128 2021-09-13 12:10:19 UTC+0000
 0xfffffa80018b1040:System                              4      0     90    576 2021-09-12 17:45:36 UTC+0000
. 0xfffffa8002a14040:smss.exe                         272      4      2     29 2021-09-12 17:45:36 UTC+0000
 0xfffffa800466f060:winlogon.exe                      472    400      3    113 2021-09-12 17:45:40 UTC+0000
 0xfffffa8004244b00:csrss.exe                         416    400     12    780 2021-09-12 17:45:40 UTC+0000
 0xfffffa80043b3220:Discord.exe                      1828   3552     34    691 2021-09-12 17:52:32 UTC+0000
. 0xfffffa80020593b0:Discord.exe                     5396   1828     30    580 2021-09-12 17:52:38 UTC+0000
. 0xfffffa80043127d0:Discord.exe                     4408   1828     13    315 2021-09-12 17:52:33 UTC+0000
. 0xfffffa8001dd2060:Discord.exe                     4908   1828      8    120 2021-09-12 17:52:33 UTC+0000
.....
```

Running pstree in volatility, we can find a weird process named drpbx.exe which doesn’t follow the typical naming convention.

![image](https://user-images.githubusercontent.com/62060867/134973963-48e73616-f7dc-414c-af94-86bbcd6621d7.png)

Some searching tells that it is a process ran by the Jigsaw Ransomware.

![image](https://user-images.githubusercontent.com/62060867/134975007-918f40db-095f-4cdb-93e0-516b927a0ec0.png)

> So we have lowerCaseMalwareName is: `jigsaw`

Diving deeper by having a look at the `dlllist` with `pid 3628`

```
/home/kali/Desktop/volatility/volatility -f JacobsPC.raw --profile=Win7SP0x64 dlllist -p 3628
Volatility Foundation Volatility Framework 2.6
************************************************************************
drpbx.exe pid:   3628
Command line : "C:\Users\Jacob\AppData\Local\Drpbx\drpbx.exe" C:\Users\Public\Videos\Sample?Videos\PJxhJQ9yUDoBF1188y\notsuspicious.exe
Service Pack 1

Base                             Size          LoadCount Path
------------------ ------------------ ------------------ ----
0x0000000000ff0000            0x50000             0xffff C:\Users\Jacob\AppData\Local\Drpbx\drpbx.exe
0x0000000077680000           0x19f000             0xffff C:\Windows\SYSTEM32\ntdll.dll
0x000007feef7e0000            0x6f000             0xffff C:\Windows\SYSTEM32\MSCOREE.DLL
0x0000000077560000           0x11f000             0xffff C:\Windows\system32\KERNEL32.dll
0x000007fefd510000            0x6a000             0xffff C:\Windows\system32\KERNELBASE.dll
0x000007feff7c0000            0xdb000               0x10 C:\Windows\system32\ADVAPI32.dll
.....
```
This list shows 3 points of interest, the first is a strange executable file simulating dropbox - C:\Users\Jacob\AppData\Local\Drpbx\drpbx.exe - the other two points of interest are CRYPTBASE.dll and CRYPTSP.dll. Whilst these are standard Windows dll's, these two in combination are quite common among Windows ransomware.

![image](https://user-images.githubusercontent.com/62060867/134976032-5faebf1b-36f7-4233-90b2-31cea0e46799.png)

The weird string, with notsuspicious.exe hinting, seemed to be the origin folder.

> So we have originatingFolderName is : `PJxhJQ9yUDoBF1188y`

Checking for any persistence in the Software hive key, volatility shows 2 processes; out of which one is legit that is the parent process Discord.exe storing Update.exe for updating itself whenever there is an update, and other is firefox.exe but the directory is again named in the same convention we saw earlier.

```
/home/kali/Desktop/volatility/volatility -f JacobsPC.raw --profile=Win7SP0x64 printkey -K "Software\Microsoft\Windows\CurrentVersion\Run"
Volatility Foundation Volatility Framework 2.6
Legend: (S) = Stable   (V) = Volatile

----------------------------
Registry: \SystemRoot\System32\Config\DEFAULT
Key name: Run (S)
Last updated: 2021-09-13 10:41:47 UTC+0000

Subkeys:

Values:
----------------------------
Registry: \??\C:\Users\Jacob\ntuser.dat
Key name: Run (S)
Last updated: 2021-09-13 12:10:15 UTC+0000

Subkeys:

Values:
REG_SZ        Discord         : (S) C:\Users\Jacob\AppData\Local\Discord\Update.exe --processStart Discord.exe
REG_SZ        firefox.exe     : (S) C:\Users\Jacob\AppData\Roaming\Frfx\firefox.exe

```

> So we have persistenceName is : `firefox.exe`

Therefore, putting these findings together the flag is:

```
DUCTF{jigsaw_firefox.exe_PJxhJQ9yUDoBF1188y}
```










