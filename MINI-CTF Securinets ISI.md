# MINI-CTF Securinets ISI

# ****DIGITAL FORENSICS & INCIDENT RESPONSE :****

## —Classics—

### Classics 1

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled.png)

For this task we were given this .rar :

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%201.png)

Trying to extract this rar we get this 

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%202.png)

seems like this is not a rar file …

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%203.png)

file command confirms that this file is corrupted.

Something that comes to mind is too look at the file signature or the “Magic Bytes”

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%204.png)

Now, .rar files should start with these bytes

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%205.png)

Let’s try fixing the signature using hexeditor

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%206.png)

Yes the file is fixed

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%207.png)

Now’s the time for volatility to answer the first question : give me the profile for the image ;)

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%208.png)

I’m using volatility 2.4 here

```
[vol.py](http://vol.py) -f /path/to/file kdbgscan
```

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%209.png)

Our answer is 

<aside>
💡 Secruinets{Win7SP1x64}

</aside>

---

### Classics 2

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2010.png)

My method is a bit unorthodoxed but I just ran filescan while grepping with “Users”

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2011.png)

```
vol.py -f /path/to/file --profile=Win7SP1x64 filescan | grep "Users"
```

Securinets{nadhir}

---

### Classics 3

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2012.png)

To find the Computer name i ran envars and grepped for “COMPUTERNAME”

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2013.png)

```
vol.py -f /path/to/file --profile=Win7SP1x64 envars | grep "COMPUTERNAME"
```

<aside>
💡 Securinets{NADHIR-PC}

</aside>

---

### Classics 3

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2014.png)

We start with filescan while grepping to “flag”

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2015.png)

```
vol.py -f /path/to/file --profile=Win7SP1x64 filescan | grep "flag"
```

Now we use dumpfiles to get the flag to our current directory

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2016.png)

```
vol.py -f /path/to/file --profile=Win7SP1x64 dumpfiles --dump-dir="./" -Q 0x000000007d09e600
```

We get this file 

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2017.png)

Let’s rename it to flag.txt.txt

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2018.png)

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2019.png)

<aside>
💡 Securinets{eeeeeh}

</aside>

---

### Classics 4

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2020.png)

Let’s check the registry with hivelist

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2021.png)

Now using printkey we check every hive until we get to the SOFTWARE hive

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2022.png)

Hmmm passsy and passy look unusual and out of place let’s check them with the option -K “passy”

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2023.png)

Boom there’s our flag 

<aside>
💡 Securinets{elnkabrtfgoghbg}

</aside>

---

### Classics 6

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2024.png)

![Untitled](MINI-CTF%20Securinets%20ISI%20/Untitled%2025.png)

For this task we need the mimikatz plugin, for some reaon it wouldn’t work on kali o i had to resort to LosBuntu a Ubuntu ditro for forensic where i could use mimikatz, running thi command we can get the passwords and the final flag for our classics

```
python2 vol.py -f /path/to/file --profile=Win7SP1x64  mimikatz
```

<aside>
💡 Securinets{hawkdummy}

</aside>