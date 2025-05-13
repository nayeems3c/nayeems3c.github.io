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

I was able to solve some basic Steganography challenges and a single Networking challenge from this event. So, lets get started.


### 1. Beautiful Road (100 Points)

![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-beautiful-road.png)

So they provided a png image file. For quick check, I uploaded the given png file to `https://stylesuxx.github.io/steganography/`. Decoding that png immidiately reavealed the hidden message which is a C programming Code snippet that contains the flag. 

```
79:#include <stdio.h>

int main() {

    printf("Th15_1s_RC!");

    return 0;

}
```
So, our flag is `WSTID{Th15_1s_RC!}`


### 3. I Love Documents (100 Points)

In this challenge, we are given a MS Word file named `espionage.docx`.
![Steganorgraphy Challenges](/assets/img/mist25/mist-steg-ilove-doc.png)

 Opening the document displayed some gibberish text. Then I checked it with `file` & `hexeditor` command on terminal to identify exact file type but found nothing. Then I ran `strings` command piped with `grep` and saw something like this.

![Steganorgraphy Challenges](/assets/img/mist25/ilovedoc_strings.png)

From this point, i knew its a zip archive. I quickly changed the file extension from `docx` to `zip` and unzipped it then moved to `word` directory and found the flag.

![Steganorgraphy Challenges](/assets/img/mist25/flag.png)


### 4. Robot Talks (150 Points)


![Steganorgraphy Challenges](/assets/img/mist25/flag.png)