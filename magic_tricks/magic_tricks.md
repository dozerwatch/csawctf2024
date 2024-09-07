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
0000000 a8c2 88c3 a2c2 90c3 a8c2 89c3 afc2 98c3
0000010 89c3 6a71 a0c2 87c3 8ac3 bfc2 4a6a a0c2
0000020 c362 6a87 a0c2 7150 c248 c2a0 48b8 92c3
0000030 a0c2 c250 c280 c3a0 c289 48b1 a0c2 4170
0000040 81c3 b1c2 c348 4a87 a0c2 bac2 5262 6842
0000050 9ac3                                   
0000052
```

After entering data, the output is given in `output.txt`. So make sure to make a copy of content of the original `output.txt`.

My first thought was that `output.txt` is the flag encoded using "magic". I tested this theory by inputing "csawctf{}" as the data.



