---
title: How I hacked Dutch Government
date: 2023-06-06 10:00:00 +600
catagories: [Bug Bounty]
tags: [file upload bypass,rce,bug bounty,dutch government] #Tag names should always be in lower case.
---

## Introduction

Hello! This is Nayeem Islam. I am a Cyber Security Researcher from Bangladesh. This is my first write up and I will share how I found RCE on one of the Dutch Government websites in details. You can skip my background story and navigate to exploitation part ##File upload bypass

## Background

I started my bug bounty journey back in September, 2021. That time I saw few researchers sharing a picture of cool Black T-Shirt on Twitter feed. Since then it was my dream to achieve Dutch Govt. swag. I started with low hangig bugs and getting informative or Not Applicable on platforms like HackerOne. I kept trying and finally found my first valid bug on April 2022. That valid bug was a motivation booster for me. So, I decided to give it a try on Dutch Government websites. ![Desktop View](https://pbs.twimg.com/media/FpO9LpGaYAAeEx1?format=jpg){: width="300" height="300" }

## My Journey

Gathered some medium article of hacking the Dutch Government to get an initial idea about the process. Reading the article, I learnt that they only offer swags for impactful bugs meaning no low hanging fruits. Googled for scopes and found this [repository](https://gist.github.com/testerzs/cf3085ec0bad6b1d661887d4f44e3574). Found a site related to Health and Medicine. I didn't know much recon techniques except basic subdomain enumeration.

I found only one live subdomain using `crt.sh` and it was an e-learning platform. Anyone can sign-up on e-learning portal. Right? So, I chose this as my target because more functionalities increases the possibility of finding more bugs. I also noticed the e-learning portal was using PHP Laravel framework then my instinct said I might find bug here.


## File Upload Bypass

So my target was `elearning.example.nl`. I created an account and navigated to my profile then tested for XSS, HTMLi, CSRF and got notihng. 

Later I started testing profile picture upload feature. I tried uploading a `txt` file & the upload was successful. At first I was very happy then I opened the image url and found out the error `There is an error with this image file` also you can see below my `txt` file has been renamed and converted to `jpg`. 😥 

![Cyber Grabs CTF 2022](https://i.postimg.cc/fk4cxd1V/url.png "Cyber Grabs CTF Junior Edition") 

I tried IDOR on `/storage/2762` because this number was user identifier & sequential. It didn't work. I took a break for an hour. Then started looking into it again.

This time I noticed the sub directory `conversion`. I asked myself what the hell is this directory doing here? Maybe they are converting my original file then saving it to `conversion` folder.

So I tried accessing my `text` file by replacing `/conversions/my-image-thumb.jpg` with ```https://elearning.exaple.nl/storage/2762/my-image.txt``` and it worked.

I uploaded a oneliner php shell. 



