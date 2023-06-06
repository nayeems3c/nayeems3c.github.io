---
title: How I hacked Dutch Government
date: 2023-06-06 10:00:00 +600
catagories: [Bug Bounty]
tags: [file upload bypass,rce,bug bounty,dutch government] #Tag names should always be in lower case.
---

## Introduction

Hello! This is Nayeem Islam. I am a Cyber Security Researcher from Bangladesh. This is my first write up and I will share how I found RCE on one of the Dutch Government websites in details.

## Background

I started my bug bounty journey back in September of 2021. I saw few people sharing cool Black T-Shirt on Twitter. I wanted that swag very badly so I gathered some medium article of hacking the Dutch Government to get an initial idea about the process.

![Desktop View](https://pbs.twimg.com/media/FpO9LpGaYAAeEx1?format=jpg){: width="300" height="300" }

## My Journey

I tried finding bugs for almost 7 months and found nothing real. So, I took a long break then started again with this repository. I found a website related to Health and Medicine. I didn't knew much recon techniques except basic subdomain discovery using `crt.sh`. 

I found only one subdomain using `crt.sh` and it was an e-learning platform. Anyone can sign-up on e-learning portal. Right? So, I chose this as my target because more functionalities increases the possibility of finding more bugs. I also noticed the e-learning portal was using PHP Laravel framework then my instinct said I might find bug here.


## File Upload Bypass

I will call my target as `elearning.example.nl`. I quickly created an account and navigated to my profile then tested for XSS, HTMLi, CSRF and got notihng. 

Later I started testing profile picture upload feature. I tried uploading a `my-image.txt` file & the upload was successful. At first I was very happy then I opened the image url and found out my `.txt` file has been renamed and converted to jpg. 😥 The URL looked like this.

[url](https://postimg.cc/zHjHNyzN)




