---
title: Cyber Grabs CTF 2022 writeups
date: 2022-02-15 14:00:00 +600
catagories: [CTF,Osint]
tags: [cyber grabs junior edition,ctf,cyber grabs 2022] #Tag names should always be in lower case.
---

# Welcome to the first post

So in this post I will share a challenge walkthrough we solved at the Cyber Grabs CTF 2022's Junior edition.

![Cyber Grabs CTF 2022](https://ctftime.org/media/cache/68/f0/68f0b0a7777fa1a4e0b8c090da362e1a.png "Cyber Grabs CTF Junior Edition")

## Wayback 1

Some answers are hidden in the past, Whose website theme did we “cyberange.io” used when we first went public.

Flag Format: flag{firstname_lastname}

### Solution

They have told us that the answer is hidden in the past. It's a hint to use wayback machine. So I went to archive.org and searched for cyberange.io

In the search result, I saw that the site is live since 2016.

I have checked every screenshot starting from 2016 one by one and found the flag on a screenshot of 28th April, 2018.

I was looking for the theme owner and found this

```plaintext
#Flatfy Theme by Andrea Galanti
```
at the bottom of the page.

So, our flag is: 
*flag{andrea_galanti}*

Important: You have to submit the name in lowercase.

Thanks
