# Reversing: Magic Tricks

**Description**

I was given a magic box by a gopher and it tricked me to put in my flag! I only have garbage now... can you help me?

[chall](/magic_tricks/chall) \
[output.txt](/magic_tricks/output.txt)

author: jp

---

Running the `chall` gives the following output:

```

          _____________
          |           |
          |           |
          |           |
      ____|___________|____
        ,_---~~~~~----._
  _,,_,*^____      _____\˴ᐠ*g*\"*,
 / __/ /'     ^.  /      \ ^@q   f
[  @f | @))    |  | @))   l  0 _/
 \ᐠ/   \~____ / __ \_____/    \
  |           _l__l_           I
  }          [______]           I
  ]            | | |            |
  ]             ~ ~             |
  |                            |
   |                           |
For my magic trick...
Enter any data you want and I put it into my mysterious black box and you get out stuff into a file (wow magic)
Enter data:
```

The hexdump of `output.txt` is:

```
00000000  c2 a8 c3 88 c2 a2 c3 90  c2 a8 c3 89 c2 af c3 98  |................|
00000010  c3 89 71 6a c2 a0 c3 87  c3 8a c2 bf 6a 4a c2 a0  |..qj........jJ..|
00000020  62 c3 87 6a c2 a0 50 71  48 c2 a0 c2 b8 48 c3 92  |b..j..PqH....H..|
00000030  c2 a0 50 c2 80 c2 a0 c3  89 c2 b1 48 c2 a0 70 41  |..P........H..pA|
00000040  c3 81 c2 b1 48 c3 87 4a  c2 a0 c2 ba 62 52 42 68  |....H..J....bRBh|
00000050  c3 9a                                             |..|
00000052
```

After entering data, the output is given in `output.txt`. So make sure to make a copy of content of the original `output.txt`.

My first thought was that `output.txt` is the flag encoded using "magic". I tested this theory by inputing "csawctf{}" as the data. The resulting hexdump:

```
00000000  c2 a8 c3 88 c2 a2 c3 90  c2 a8 c3 89 c2 af c3 98  |................|
00000010  c3 9a                                             |..|
00000012
```

We see the first line and last line match the original `output.txt`. Knowing the flag consists of alphanumeric characters, I made a dictionary mapping each character to its encoded data.

```py
from pwn import *
from time import sleep

d = {}

with context.quiet:
    for i in range(33,126):
        p = process("./chall")
        p.send(p8(i)+b"\n")
        p.clean()
        sleep(1)
        f = open("output.txt", "rb")
        s = f.read()
        d[s] = p8(i)
        print(f"{p8(i)} = {s}")
```

After many trials, I found that opening `output.txt` too quickly results in faulty encoding. Sleeping for 1 second fixed that, but I do not know why. Now we have the encoding for every alphanumeric character. Decode the original output and get the flag. I did this by hand. 

Some characters have two byte encodings and some have one. All two byte encodings begin with `c2` or `c3`.

Flag: `csawctf{}`
