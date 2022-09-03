# ASD-Coin-Writeup
My Writeup of the ASD Coin Cipher Challenge Thingo

###Note: formatting of this is really bad since its a direct copy and paste of my notes doc that I've been using - will format it nicely later.

Inner:
    BGOAMVOEIATSIRLNGTTNEOGRERGXNTEAIFCECAIEOALEKFNR5LWEFCHDEEAEEE7NMDRXX5
    bGOAMVoeIaTSirlNGTtNEoGRERgxntEAIfCecaIEoALekFNr5LweFCHDEeaEEe7NmdRXx5
    PINSOMNATSKYTEBHIKKHANIEAEILHKASTCJAJSTANSBAUCHE5BRACJFWAASAAA7HOWELL5
     _____  _ __   ___ __ ____    ___ _   __ __  __ __  _____  __ __  __ _
    b     oe a  irl   t  o    gxnt   f eca  o  ek  r  we     ea  e  md  x
    1,5,2,1,1,2,3,3,1,2,1,4,4,3,1,1,3,2,1,2,2,2,1,2,2,5,2,2,1,2,2,2,1,1                                                                      
     _____  _ __   ___ __ ____    ___ _   __ __  __ __  _____  __ __  __ _
    GOAMVITSNGTNEGREREAICIEALFN5LFCHDEEE7NRX5
    GOAMV -> ously (bold)

 Outer:
    .DVZIVZFWZXRLFHRMXLMXVKGZMWNVGRXFOLFHRMVCVXFGRLM.URMWXOZIRGBRM7DRWGSC5WVKGS
    _     _     _     _     __   _   _    _  _    _    _ _   _ _    _  _   _   

    .ZLLZMGOMVLMXRBRSV -> [ission for some year?]
     _         _ ____    ___   __ ___  ___ _  _ __  ___ _ _ _   _  _ _  _ _  _ 
    DRFHRMVKGNVRXFFHRVXGR.URWOIRDWCWG
    [WEAREAUDACIOUSINCONCEPTANDMETICULOUSINEXECUTION.FINDCLARITYIN7WIDTHX5DEPTH] -> atbash (spent so long on quipqiup woops - ended up putting the code into a thingo to check a whole bunch of different ciphers at the same time)
    WE ARE AUDACIOUS IN CONCEPT AND METICULOUS IN EXECUTION. FIND CLARITY IN 7 WIDTH X 5 DEPTH
    


    Won't lie, didn't realise that the dots around the Queen were braille numbers for ages and didn't figure out that the letters in the orders of the numbers under them spelt out atbash until after :|
    
ngl, this took longer than it should have.
Arranging inner ring letters into a 7x5 grid, realised that there was text down the columns.
Used this monstrosity of a python line to concatenate everything together:
    "".join(["".join([("".join([enc[i * 7 + j + k * 35] for i in range(5)])) for j in range(7)]) for k in range(2)])
This gave: BELONGINGTOAGREATTEAMSTRIVINGFOREXCELLENCEWEMAKEADIFFERENCEXORHEXA5D75
BELONGING TO A GREAT TEAM STRIVING FOR EXCELLENCE WE MAKE A DIFFERENCE XOR HEX A5D75

Then used Crypto.Util and pwntools to xor the hex on the coin with 0xa5d75 (padded to be the same length).
Just did Crypto.Util.number.long_to_bytes(enc ^ key) and it worked!
This gave: For 75 years the Australian Signals Directorate has brought together people with the skills, adaptability and imagination to operate in the slim area between the difficult and the impossible.
    

---begin-log---


bpcygs@Jays-Laptop:/mnt/c/Users/jaidy/Downloads$ python3
Python 3.8.10 (default, Mar 15 2022, 12:22:08)
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from Crypto.Util.number import long_to_bytes
>>> long_to_bytes(10)
b'\n'
>>> enc = "E3B"
>>> 8287D4
  File "<stdin>", line 1
    8287D4
        ^
SyntaxError: invalid syntax
>>> 290F723381
  File "<stdin>", line 1
    290F723381
       ^
SyntaxError: invalid syntax
>>> 4D7A47A291DC
  File "<stdin>", line 1
    4D7A47A291DC
     ^
SyntaxError: invalid syntax
>>> 0F71B2806D1A53B
  File "<stdin>", line 1
    0F71B2806D1A53B
     ^
SyntaxError: invalid syntax
>>> 311CC4B97A0E1CC2B9
  File "<stdin>", line 1
    311CC4B97A0E1CC2B9
       ^
SyntaxError: invalid syntax
>>> 3B31068593332F10C6A335
  File "<stdin>", line 1
    3B31068593332F10C6A335
     ^
SyntaxError: invalid syntax
>>> 2F14D1B27A3514D6F7382F1A
  File "<stdin>", line 1
    2F14D1B27A3514D6F7382F1A
     ^
SyntaxError: invalid syntax
>>> D0B0322955D1B83D3801CDB2
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'D0B0322955D1B83D3801CDB2' is not defined
>>> 287D05C0B82A311085A03329
  File "<stdin>", line 1
    287D05C0B82A311085A03329
       ^
SyntaxError: invalid syntax
>>> 1D85A3323855D6BC333119D
  File "<stdin>", line 1
    1D85A3323855D6BC333119D
     ^
SyntaxError: invalid syntax
>>> 6FB7A3C11C4A72E3C17CCB
  File "<stdin>", line 1
    6FB7A3C11C4A72E3C17CCB
     ^
SyntaxError: invalid syntax
>>> B33290C85B6343955CCBA3
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'B33290C85B6343955CCBA3' is not defined
>>> B3A1CCBB62E341ACBF72
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'B3A1CCBB62E341ACBF72' is not defined
>>> E3255CAA73F2F14D1B27A
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'E3255CAA73F2F14D1B27A' is not defined
>>> 341B85A3323855D6BB33
  File "<stdin>", line 1
    341B85A3323855D6BB33
       ^
SyntaxError: invalid syntax
>>> 3055C4A53F3C55C7B22
  File "<stdin>", line 1
    3055C4A53F3C55C7B22
        ^
SyntaxError: invalid syntax
>>> E2A10C0B97A291DC0F
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'E2A10C0B97A291DC0F' is not defined
>>> 73E3413C3BE392819
  File "<stdin>", line 1
    73E3413C3BE392819
           ^
SyntaxError: invalid syntax
>>> D1F73B331185A33
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'D1F73B331185A33' is not defined
>>> 23855CCBA2A3
  File "<stdin>", line 1
    23855CCBA2A3
         ^
SyntaxError: invalid syntax
>>> 206D6BE383
  File "<stdin>", line 1
    206D6BE383
       ^
SyntaxError: invalid syntax
>>> 1108B
KeyboardInterrupt
>>> enc = 0x77
>>> enc
119
>>> enc = 0xE3B8287D4290F7233814D7A47A291DC0F71B2806D1A53B311CC4B97A0E1CC2B93B31068593332F10C6A3352F14D1B27A3514D6F7382F1AD0B0322955D1B83D3801CDB2287D05C0B82A311085A033291D85A3323855D6BC333119D6FB7A3C11C4A72E3C17CCBB33290C85B6343955CCBA3B3A1CCBB62E341ACBF72E3255CAA73F2F14D1B27A341B85A3323855D6BB333055C4A53F3C55C7B22E2A10C0B97A291DC0F73E3413C3BE392819D1F73B331185A3323855CCBA2A3206D6BE3831108B
>>> long_to_bytes(enc)
b'\xe3\xb8(}B\x90\xf7#8\x14\xd7\xa4z)\x1d\xc0\xf7\x1b(\x06\xd1\xa5;1\x1c\xc4\xb9z\x0e\x1c\xc2\xb9;1\x06\x85\x933/\x10\xc6\xa35/\x14\xd1\xb2z5\x14\xd6\xf78/\x1a\xd0\xb02)U\xd1\xb8=8\x01\xcd\xb2(}\x05\xc0\xb8*1\x10\x85\xa03)\x1d\x85\xa328U\xd6\xbc31\x19\xd6\xfbz<\x11\xc4\xa7.<\x17\xcc\xbb3)\x0c\x85\xb649U\xcc\xba;:\x1c\xcb\xb6.4\x1a\xcb\xf7.2U\xca\xa7?/\x14\xd1\xb2z4\x1b\x85\xa328U\xd6\xbb30U\xc4\xa5?<U\xc7\xb2.*\x10\xc0\xb9z)\x1d\xc0\xf7>4\x13\xc3\xbe9(\x19\xd1\xf7;3\x11\x85\xa328U\xcc\xba*2\x06\xd6\xbe81\x10\x8b'
>>> from pwn import *
[*] Checking for new versions of pwntools
    To disable this functionality, set the contents of /home/bpcygs/.cache/.pwntools-cache-3.8/update to 'never' (old way).
    Or add the following lines to ~/.pwn.conf or ~/.config/pwn.conf (or /etc/pwn.conf system-wide):
        [update]
        interval=never
[*] A newer version of pwntools is available on pypi (4.7.0 --> 4.8.0).
    Update with: $ pip install -U pwntools
>>> xor(enc, 0xa5d75)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/fiddling.py", line 325, in xor
    strs = [packing.flat(s, word_size = 8, sign = False, endianness = 'little') for s in args]
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/fiddling.py", line 325, in <listcomp>
    strs = [packing.flat(s, word_size = 8, sign = False, endianness = 'little') for s in args]
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/context/__init__.py", line 1544, in setter
    return function(*a, **kw)
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/packing.py", line 775, in flat
    out = _flat(args, preprocessor, make_packer(), filler, stacklevel + 2)
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/packing.py", line 596, in _flat
    val = packer(arg)
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/packing.py", line 438, in <lambda>
    return lambda number: pack(number, word_size, endianness, sign)
  File "/home/bpcygs/.local/lib/python3.8/site-packages/pwnlib/util/packing.py", line 149, in pack
    raise ValueError("pack(): number does not fit within word_size [%i, %r, %r]" % (0, number, limit))
ValueError: pack(): number does not fit within word_size [0, 8375165132163443087249397998469216739285753633371103178829599679148079657886887439655356015756610188542442497337622994167773227571340665930248359196215687405466805272521393076883351222187476697894338122256004765529833192481338401966338196063738316210855943799703237616285020531066527366998156730183186009860186040538773592415109713435421866254969005941685133391068783915729600435717362926483021143299450790141000901015489590116678951428313997139381024304730251, 256]
>>> enc
8375165132163443087249397998469216739285753633371103178829599679148079657886887439655356015756610188542442497337622994167773227571340665930248359196215687405466805272521393076883351222187476697894338122256004765529833192481338401966338196063738316210855943799703237616285020531066527366998156730183186009860186040538773592415109713435421866254969005941685133391068783915729600435717362926483021143299450790141000901015489590116678951428313997139381024304730251
>>> enc ^ 0xa5d75
8375165132163443087249397998469216739285753633371103178829599679148079657886887439655356015756610188542442497337622994167773227571340665930248359196215687405466805272521393076883351222187476697894338122256004765529833192481338401966338196063738316210855943799703237616285020531066527366998156730183186009860186040538773592415109713435421866254969005941685133391068783915729600435717362926483021143299450790141000901015489590116678951428313997139381024305401342
>>> len(enc)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: object of type 'int' has no len()
>>> len(hex(enc))
384
>>> 384 / 3
128.0
>>> 384/5
76.8
>>> "a5d75" * 77
'a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75'
>>> ("a5d75" * 77).decode("hex")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'str' object has no attribute 'decode'
>>> bytes.fromhex("a5d75")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ValueError: non-hexadecimal number found in fromhex() arg at position 5
>>> bytes.fromhex(b"a5d75")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fromhex() argument must be str, not bytes
>>> b"a5d75"
b'a5d75'
>>> from Crypto.Util.number import bytes_to_long
>>> "a5d75" * 77
'a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75'
>>> key = 0xa5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75
>>> enc ^ key
24984266657386351982017424609584480854776764721101549887144113376179961162944308250931476768935014451559784808120810388583041104256167255830512532361399107292086096230408288791149385278922383573036534872739586967171118844657805576929471737139994253038086234538357384156353166847863894716597776608727002879753510080926494453212546493997977528985649973996917925324290368322867584218542124462713676061032474517150414473494446078929808193460677914211043911738046762494
>>> len(hex(key))
387
>>> hex(key)
'0xa5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75'
>>> len(hex(enc))
384
>>> len(hex(key)[:384])
384
>>> hex(key)[:384]
'0xa5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5'
>>> key = 0xa5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5d75a5
>>> enc^key
2590502375179979262775950543765471783242729734048908211036924275896130340680869586177826201135364390054351446701668244750977148949605566165907766609675468490291318628662506113736833115503797808253195641742100218946106859385657391801273226338941483439016202082363829516951189506019686886157792448979567546486544378392717339149525923920301685506310630093010643090403456702502907337446423775769679499655051508108204069741873107635749979576986203736713367210714414
>>> long_to_bytes(enc^key)
b'For 75 years the Australian Signals Directorate has brought together people with the skills, adaptability and imagination to operate in the slim area between the difficult and the impossible.'
>>>

----end-log----

E3B8287D4290F7233814D7A47A291DC0F71B2806D1A53B311CC4B97A0E1CC2B93B31068593332F10C6A3352F14D1B27A3514D6F7382F1AD0B0322955D1B83D3801CDB2287D05C0B82A311085A033291D85A3323855D6BC333119D6FB7A3C11C4A72E3C17CCBB33290C85B6343955CCBA3B3A1CCBB62E341ACBF72E3255CAA73F2F14D1B27A341B85A3323855D6BB333055C4A53F3C55C7B22E2A10C0B97A291DC0F73E3413C3BE392819D1F73B331185A3323855CCBA2A3206D6BE3831108B
