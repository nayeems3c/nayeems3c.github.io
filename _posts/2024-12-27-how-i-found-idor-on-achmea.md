---
layout: post
title: "How I found an IDOR on Achmea"
date: 2024-12-27 10:00:00 +0600
categories: [Bug Bounty]
tags: [bugbounty, idor, api, swag]
description: I exploited an IDOR to get cool swag from Achmea.
image: https://miro.medium.com/v2/resize:fit:1100/format:webp/1*VLNnkzoShOfFnBg9E3GHow.jpeg
---

Assalamu Alaikum and greetings to everyone. This is nayeems3c. I am back with another short write-up. Let's get into it.

I was hunting on a subsidiary of Achmea. Let’s call our target `example.com`. I found a subdomain of example.com which allows users to create an account but a user can not see other users profile.

I created an account and while logging into my profile, I noticed an interesting API call like the one below

```text
GET /api/users/me HTTP/1.1
Host: site.example.com
```

I intercepted the request and checked the response and found my test account’s Id, email, full name, address, date of birth in JSON format. There was an Id number but I was not sure what kind of Id it was.

```json
{
  "id": 24,
  "email": "testaccount@example.com",
  "full_name": "Test User",
  "address": "123 Test Street, Test City, Test Country",
  "date_of_birth": "1990-01-01"
}
```

To confirm whether 24 is my profile number, I forwarded the request mentioned above to repeater and replaced `me` with my account id `24` and it still gave me the same response. Created another test account and found the profile id is 25 meaning its sequential. 

Now it’s time to test Insecure Direct Object Reference (IDOR) vulnerability on that parameter.

So, I replaced id no. 24 with 23 on the API request and it looked like below.

```text
GET /api/users/23 HTTP/1.1
Host: site.example.com
```
In response it disclosed other user’s information. I tried all sequential numbers on intruder and it disclosed every users personally identifiable information.

I immediately reported it to Achmea and after a few months I was awarded cool Hacker T-shirt.

I hope you enjoyed this write-up. If you have any questions please let me know.