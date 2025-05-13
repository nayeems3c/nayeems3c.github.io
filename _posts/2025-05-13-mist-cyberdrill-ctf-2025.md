---
layout: post
title: "Steganography Walkthrough of MIST Cyberdrill 2025 Qualifier"
date: 2025-05-13 10:15:00 +0600
categories: [CTF]
tags: [steganography, forensics, image forensics]
description: MIST Cyberdrill CTF 2025 qualifier round steganography walkthrough
image: https://miro.medium.com/v2/resize:fit:1100/format:webp/1*-M41WOm1D3QLcU4JNq2kMQ.jpeg
---

Hello! This is nayeems3c. I along with my team Cyb3r_W4rM0ng3rs participated in the qualifier round of MIST Cyberdrill 2025 and secured 44th place among 192 teams across Bangladesh.

![Steganorgraphy Challenges](/assets/img/mist25/mist-steg.png)

I was able to solve a few basic Steganography challenges from this event. So, let’s get started.


### 1. Beautiful Road (100 Points)

![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-beautiful-road.png)

They gave us a png image file. For quick test, I uploaded the given png file to `https://stylesuxx.github.io/steganography/`. Decoding that png immediately reavealed the hidden message which is a C programming Code snippet that contains the flag. 

```c
#include <stdio.h>

int main() {

    printf("Th15_1s_RC!");

    return 0;
}
```
So, our flag is `WSTID{Th15_1s_RC!}`


### 3. I Love Documents (100 Points)

In this challenge, we are given a MS Word file named `espionage.docx`.
![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-ilove-doc.png)

 When I opened the document, it showed a lot of gibberish text. Then I checked it with `file` and `hexeditor` command on terminal to identify exact file type but found nothing. Then I ran `strings` command piped with `grep` and saw something like this.

![Steganorgraphy Challenges](/assets/img/mist25/ilovedoc_strings.png)

From this point, i knew its a zip archive. I quickly changed the file extension from `docx` to `zip` and unzipped it then I navigated to the `word` directory and found the flag.

![Steganorgraphy Challenges](/assets/img/mist25/flag.png)


### 4. Robot Talks (150 Points)

![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-robotalks.png)

We were given 2 png files which is almost similar. I downloaded them and and checked it by changing color pane and zooming. Nothing worked then I ran diff command
```shell
$ diff suppyl.png dupply.png
Binary files supply.png and dupply.png differ
```
Lastly I tried `zsteg` command on both png files separately and it revealed the flag from `dupply.png`

![Steganorgraphy Challenges](/assets/img/mist25/robot-flag.png)

Lets move to the last one from this category.

### 5. Binary (150 Points)

It felt more like a Cryptography challenge rather than Steg.

![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-binary.png)

We were given a text file that contains a huge binary text. I Converted the Binary to text and found following text along with some base64 encoded data. 

```
Uh-oh, looks like we have another block of text, with some sort of special encoding. Can you figure out what this encoding is? (hint: if you look carefully, you'll notice that there only characters present are A-Z, a-z, 0-9, and sometimes / and +. See if you can find an encoding that looks like this one.)

TmV3IGNoYWxsZW5nZSEgQ2FuIHlvdSBmaWd1cmUgb3V0IHdoYXQncyBnb2luZyBvbiBoZXJlPyBJdCBsb29rcyBsaWtlIHRoZSBsZXR0ZXJzIGFyZSBzaGlmdGVkIGJ5IHNvbWUgY29uc3RhbnQuCm15eHFia2Rldmtkc3l4YyEgaXllIHJrZm8gcHN4c2Nyb24gZHJvIGxvcXN4eG9iIG1iaXpkeXFia3pyaSBtcmt2dm94cW8uIHJvYm8gc2MgayBwdmtxIHB5YiBrdnYgaXllYiBya2JuIG9wcHliZGM6IEdEU0NOe3dldmRzLW1zenJvYi1zYy14eWQtbGtufS4gaXllIGdzdnYgcHN4biBkcmtkIGsgdnlkIHlwIG1iaXpkeXFia3pyaSBzYyBsZXN2bnN4cSB5cHAgZHJzYyBjeWJkIHlwIGxrY3NtIHV4eWd2b25xbywga3huIHNkIGJva3Z2aSBzYyB4eWQgY3kgbGtuIGtwZG9iIGt2di4gcnl6byBpeWUgb3h0eWlvbiBkcm8gbXJrdnZveHFvIQ==
```
I decoded the base64 part and discovered more text encrypted with a different cipher. We also have a flag format like text.

```
New challenge! Can you figure out what's going on here? It looks like the letters are shifted by some constant.

myxqbkdevkdsyxc! iye rkfo psxscron dro loqsxxob mbizdyqbkzri mrkvvoxqo. robo sc k pvkq pyb kvv iyeb rkbn oppybdc: GDSCN{wevds-mszrob-sc-xyd-lkn}. iye gsvv psxn drkd k vyd yp mbizdyqbkzri sc lesvnsxq ypp drsc cybd yp lkcsm uxygvonqo, kxn sd bokvvi sc xyd cy lkn kpdob kvv. ryzo iye oxtyion dro mrkvvoxqo!
```

With the help of `decode.fr` cipher identifier, it turned out to be `Caeser` cipher. So, we decrypted it and That gives us the flag `WTISD{multi-cipher-is-not-bad}`

That wraps it up for today. Thanks.