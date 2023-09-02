---
title: How I hacked Dutch Government
date: 2023-08-31 10:00:00 +600
catagories: [Bug Bounty]
tags: [file upload bypass,rce,bug bounty,dutch government] #Tag names should always be in lower case.
---

## Introduction

Assalamu Alaikum! This is Nayeem Islam. I'm a cyber security learner from Bangladesh. This is my first write-up, and I will share in detail how I found RCE on one of the Dutch government websites. You can skip my background story and navigate to the exploitation part.

## Background

I started my bug bounty journey in September 2021. That time, I saw a few researchers sharing a picture of a cool black T-shirt on Twitter. Since then, it's been my dream to achieve Dutch government swag.

I started with low-hanging fruits and got informative or not applicable on platforms like HackerOne. I kept trying and finally found my first valid bug in April 2022. That valid bug was a motivation booster for me. So, I decided to give it a try on Dutch government websites.

## My Journey

I gathered some articles about hacking the Dutch government to get an initial idea of the process. Reading those articles, I learned that they only offer swags for impactful bugs, meaning no low-hanging fruits. 

Googled for scopes and found this [repository](https://gist.github.com/testerzs/cf3085ec0bad6b1d661887d4f44e3574). I found a site related to health and medicine. That time I didn't know much recon techniques except for basic subdomain enumeration.

I found only one live subdomain using `crt.sh`. It was an e-learning platform. Anyone can sign-up on an e-learning portal. Right? 

So, I chose this as my target because more functionalities increase the possibility of finding more bugs. I also noticed the e-learning portal was using the PHP Laravel framework then my instinct said I might find a bug here.

## File Upload Bypass

So my target was `elearning.example.nl`. I created an account and navigated to my profile then tested for XSS, HTMLi, CSRF and got nothing.

Later I started testing profile picture upload feature. I tried uploading a simple `test.txt` file & the upload was successful. At first I was very happy then I opened the image url and found this error.
```
There is an error with this image file
``` 
also you can see below my `txt` file has been renamed and converted to `jpg`. 😥 

![Dutch Government bug bounty](https://i.postimg.cc/J0VMKYL7/url1.png "Dutch Responsible Disclosure")

I tried IDOR on this endpoint `/storage/528` because this number was user identifier & sequential. It didn't work. I took a break for a few hours then started looking into it again.

This time I noticed the sub directory `conversion`. I asked myself what the hell is this directory doing here? Maybe they are storing my original text file in the `/528/` directory then converting it to jpg and saving it to `conversion`.

I tried accessing the uploaded `text` file from `/528/` directly. So, the URL looked like this. 

 ```
 https://elearning.example.nl/storage/528/my-image.txt
 ``` 

My assumption was right. The `txt & html` file executed! Wrote a good report with PoC and submitted it.

Later I learned about File Upload to RCE. Then uploaded this simple one liner php shell to see whether RCE is achievable.

```
<?php system($_GET['cmd']); ?>
``` 
Opened profile image in a new tab and modified the URL like this.
```
https://elearning.example.nl/storage/528/shell.php?cmd=id
```
and voilaaaa!!! Got RCE 😎

![Dutch Government bug bounty](https://i.postimg.cc/TYfffc6F/rce-1.png "Dutch Responsible Disclosure")

Send additional report to prove impact.

## End Story

I was happy and hopeless at the same time cause this was easy to find so it might be a duplicate. 

Guess what? My report was triaged! NCSC-NL also advised me not to upload shell on their system! 😜

![Dutch Government bug bounty](https://i.postimg.cc/wT3FyZv1/fixed.png "Dutch Responsible Disclosure")

This issue was resolved within a month and I was awarded the Dream Swag! It was my first critical finding on a real target as well as my first ever bug submission on the Dutch Government. I thought I was lucky but I was wrong. My swag got lost in the shipment. 😞

Before this finding, I had never completed a single Portswigger lab on File Uploads or Command Execution except basic tryhackme rooms.

I learned a lot of things while finding this bug. They say, Enjoy the journey, not the destination. Right?

### Timeline 

18-06-2022 - Reported the vulnerabilty.

19-06-2022 - Got first response.

20-06-2022 - Confirmed and triaged.

18-07-2022 - Bug Resolved.


I would like to thank all from the [Bug Bounty Community of Bangladesh](https://twitter.com/bbcbd_official) for mentoring me and infosec community of [Twitter](https://twitter.com/hashtag/bugbounty) for sharing their valuable research and tips.

That's it. Thanks for reading such a lengthy blog.

