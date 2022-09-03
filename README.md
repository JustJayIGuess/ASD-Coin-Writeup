# ASD-Coin-Writeup
My Writeup of the ASD Coin Cipher Challenge Thingo

I started by just running the strings of text through quipqiup, but that wasn't really getting anywhere.
Then I tried the same thing, but only with bolded letters/unbolded letters, but that wasn't really getting me anywhere either.
Eventually I just put the strings into a multi-cipher thingo that just checks a bunch of common ciphers, and found that Atbash worked.
I'd never heard of this cipher before, but it looks like its similar to a caeser cipher but with the letters reversed instead of shifted.
This gave:
```
=> WEAREAUDACIOUSINCONCEPTANDMETICULOUSINEXECUTION.FINDCLARITYIN7WIDTHX5DEPTH
=> WE ARE AUDACIOUS IN CONCEPT AND METICULOUS IN EXECUTION. FIND CLARITY IN 7 WIDTH X 5 DEPTH
```

I'm not going to lie, I got stuck here for a but longer than I probably should have.
I was convinced that the 7 and 5 had something to do with a cipher involving a grid, like a rail-fence, but nothing seemed to be working on any of the strings/string subsets (based on bolding). At some point I just wrote the letters down in a grid to try some things by hand, and then realised that I could read plaintext by reading down the columns.

![IMG_20220903_143158](https://user-images.githubusercontent.com/40308162/188255971-d21ecbc5-d30f-4052-8890-94a2ef0c551c.jpg)

Being a programmer, I ended up spending 10 minutes trying to remember how to use python to code this monstrosity instead of just typing it in by hand in two minutes:
```py
    "".join(["".join([("".join([enc[i * 7 + j + k * 35] for i in range(5)])) for j in range(7)]) for k in range(2)])
```

After a few typos, this eventually output:
```
=> BELONGINGTOAGREATTEAMSTRIVINGFOREXCELLENCEWEMAKEADIFFERENCEXORHEXA5D75
=> BELONGING TO A GREAT TEAM STRIVING FOR EXCELLENCE WE MAKE A DIFFERENCE XOR HEX A5D75
```

Finally, something I'm familiar with!
I quickly openned up python3 in WSL, imported pwntools and Crypto.Util.number.long_to_bytes, and just repeated the key so it was the right length and XOR'd, before converting it to bytes (*yes I know I need to `sudo apt-get update; sudo apt-get upgrade`, but I usually use a dual booted linux system instead of WSL anyway*):
```py
bpcygs@Jays-Laptop:/mnt/c/Users/jaidy/Downloads$ python3
Python 3.8.10 (default, Mar 15 2022, 12:22:08)
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from Crypto.Util.number import long_to_bytes
>>> long_to_bytes(10)
b'\n'
>>> enc = 0xE3B8287D4290F7233814D7A47A291DC0F71B2806D1A53B311CC4B97A0E1CC2B93B31068593332F10C6A3352F14D1B27A3514D6F7382F1AD0B0322955D1B83D3801CDB2287D05C0B82A311085A033291D85A3323855D6BC333119D6FB7A3C11C4A72E3C17CCBB33290C85B6343955CCBA3B3A1CCBB62E341ACBF72E3255CAA73F2F14D1B27A341B85A3323855D6BB333055C4A53F3C55C7B22E2A10C0B97A291DC0F73E3413C3BE392819D1F73B331185A3323855CCBA2A3206D6BE3831108B
>>> from pwn import *
[*] Checking for new versions of pwntools
    To disable this functionality, set the contents of /home/bpcygs/.cache/.pwntools-cache-3.8/update to 'never' (old way).
    Or add the following lines to ~/.pwn.conf or ~/.config/pwn.conf (or /etc/pwn.conf system-wide):
        [update]
        interval=never
[*] A newer version of pwntools is available on pypi (4.7.0 --> 4.8.0).
    Update with: $ pip install -U pwntools
>>> len(hex(enc))
384
>>> 384/5
76.8
>>> from Crypto.Util.number import bytes_to_long
>>> key = 0xa5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5
>>> enc^key
2590502375179979262775950543765471783242729734048908211036924275896130340680869586177826201135364390054351446701668244750977148949605566165907766609675468490291318628662506113736833115503797808253195641742100218946106859385657391801273226338941483439016202082363829516951189506019686886157792448979567546486544378392717339149525923920301685506310630093010643090403456702502907337446423775769679499655051508108204069741873107635749979576986203736713367210714414
>>> long_to_bytes(enc^key)
b'For 75 years the Australian Signals Directorate has brought together people with the skills, adaptability and imagination to operate in the slim area between the difficult and the impossible.'
>>>
```
Eureka!

...If only that was it

As a fun aside, after this I thought the next step was to figure out what the dots around Queen Elizabeth's head were, but after I realised they were braille letters and arranged them with the big letters they were next to in alphabetical order, it just gave `ATBASH`, so... I guess I was meant to do that first.


Anyway, after this, I spent hours trying different combinations of treating full bold letters as 1's and half bold letters as 0's, regular letters as 0's and full bold letters as 1's, etc., but just *couldn't find anything*. Eventually, I found that the half-bolded letters in the outer ring made a Baconian cipher, which I put through dcode.fr.

Have I finally got it!?

```
=> RIECBSCCIILFBEI
```

Nope.
I ended up trying a bunch of different monoalphabetic ciphers on the mysterious `RIECBSCCIILFBEI`, but nothing came of it.

Eventually I went back to the 1's and 0's and started to try that again.

I ended up making a plaintext doc with all of the binary string I could derive from the letter rings, along with bit flipped version of them, then started to CTRL+F for binary letters in them. Initially, I hadn't really tried to hard with decoding the strings as ascii, since they were all either 70 or 75 characters long, which isn't a multiple of 8 (8 bits in a byte). After actually looking at an ascii chart, though, I realised that most of the codes started with a 0. After a bit of research, I found out that the original ascii seemed to be based off 7 bit bytes anyway. 7 divides the 70 characters in the inner wheel, so i split it up into 7 bit bytes and tried the string with bolded letters as 1's and regular letters as 0's, along with it's bitflipped version, in dcode.fr:

```
1000001101001110001001000011110001011100100110010011000001100100110010
=> ASDCbr2022
```

Very reminiscent of CTFs. ASD should absolutely run a CTF.

I actually realised afterwards that dcode.fr automatically tries both 8bit and 7bit binary, so I would've found this sooner if I'd just tried the binary strings in dcode.fr originally.


Anyway, this now only leaves the outer ring.


I started off doing the same as what I had done for the previous layer - try heaps of different obscure ciphers and weird things. Needless to say, this got me nowhere.


Eventually I took some inspiration from the way I showed the bolded and half-bolded letters in my plaintext doc in vscode:
```
 Outer:
    .DVZIVZFWZXRLFHRMXLMXVKGZMWNVGRXFOLFHRMVCVXFGRLM.URMWXOZIRGBRM7DRWGSC5WVKGS
    _     _     _     _     __   _   _    _  _    _    _ _   _ _    _  _   _   

    .ZLLZMGOMVLMXRBRSV
     _         _ ____    ___   __ ___  ___ _  _ __  ___ _ _ _   _  _ _  _ _  _ 
    DRFHRMVKGNVRXFFHRVXGR.URWOIRDWCWG
    [WEAREAUDACIOUSINCONCEPTANDMETICULOUSINEXECUTION.FINDCLARITYIN7WIDTHX5DEPTH] -> atbash (spent so long on quipqiup woops - ended up putting the code into a thingo to check a whole bunch of different ciphers at the same time)
    WE ARE AUDACIOUS IN CONCEPT AND METICULOUS IN EXECUTION. FIND CLARITY IN 7 WIDTH X 5 DEPTH
```

The underscores at the top represent the half-bolded letters, and the ones at the bottom represent the fully bolded ones. Looks kind of like morse code, doesn't it?
Anyway, I decided to try using the top ones as dashes and the bottom ones as dots, and got...

```
=> NCILATELLENTSTI
```

Welp.

Fast forward some switching around and trying a bunch of variations of what I already had, then trying non-morse-code things, and I was still stuck on this.
After a bit though, I realised that the half-bolded letters were only ever by themself or two-in-a-row. Maybe these are the spaces between letters?
I ended up dumping the underscore things into a new document and making the half-bolded letters spaces, and the bolded/unbolded letters the dashes and dots.
Finally I plugged this into dcode.fr:

```
    _     _     _     _     __   _   _    _  _    _    _ _   _ _    _  _   _    (spaces)
     _         _ ____    ___   __ ___  ___ _  _ __  ___ _ _ _   _  _ _  _ _  _  (dots/0)
      ____ ____      _ __     _       _     _  _   _       _  _  __   _  _  _ _ (dashes/1)
     01111 11110 00001 11000  100 000 1000 01 0100 1000 0 010 1 0110 01 010 101    
=> 1947DSBALBERTPARK
```

Bingo!

## Takeaway
This was super fun, and I learned a lot more than I would have if I'd just spent this time doing maths homework (though specialist maths problems are certainly a fun challenge sometimes). After doing all this, I've found out that a bunch of other tools exist out there, like cyberchef. Also got a much better intuition for different types of ciphers, such as that ciphers containing lots of V's and G's are probably Atbash, and ascii isn't necessarily just a bunch of bytes.
Overall, a very fun experience, and I hope that ASD continues to do puzzles like this.
