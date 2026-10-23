
A core strategy of compression algorithms is to reduce redundancy. For instance, the string `pwncollegepwncollegf` can be compressed by identifying the repeating string `pwncolleg` and creating a shorter symbol to represent it (here we use `X` for example), which gets placed in a dictionary.

The data would end up something like:

```
{X:pwncolleg} XeXf
```

If we instead have the string `pwncollegepwncollege`, now `pwncollege` repeats, and the data would be one byte shorter:

```
{X:pwncollege} XX
```

In this challenge, your input is appended to the flag, compressed, and encrypted with AES-CTR. While we don't know the whole flag, we do know that flags begin with `pwn.college{` and stream ciphers like AES-CTR give us exactly the length of the encrypted data.

Let's say the flag is `pwn.college{foobar}`. We can guess the flag one character at a time and check the length:

```
pwn.college{a
pwn.college{b
pwn.college{c
pwn.college{d
pwn.college{e
pwn.college{f
```

Once we try `f`, we find that the length of the output is one character shorter, which tells us the data compressed better, which indicates that the first character of the flag is `f`. We can repeat this process for all the characters of the flag until we've recovered the whole thing.
