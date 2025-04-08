---
layout: post
title:  "Bots Almost Spammed my New Rails App to Death - What I Did to Stop Them"
date:   2025-4-7 00:00:00 -0700
categories: rails coding
tags: slopecs rails coding bots spam
image: /assets/bd_logo500pxsquare.png
---

## My first Rails apps deployed

About a year ago I launched (deployed) my first two Rails apps, [GeoGardening](https://geogardening.app/) and [SlopeCS](https://slopecs.com/) with fly.io and everything was great. I was still building, testing - learning how to get "Hello World" out to the actual world for the very first time. Then, on New Years Eve 2024, all of that changed and I was thrust into a 4-month ongoing battle against the spam bots.

### Getting to the BOT-tom of suspicious sign ups

Shortly after upgrading my apps' servers in late 2024 to be "always on", they each received A TON of activity and I didn't find out until it was too late.

My apps send a welcome email after a User account is created; pretty basic stuff, right? - Nope... 

First, I found over 140 "Welcome" and "password reset" emails were sent from my Postmark account with a high percentage bounced and reported as spam, hurting my deliverability score, and immediately filling my monthly quota. What?! I didn't do that much testing this month? So I looked at the production database next...

I found over 1,400 user accounts with about 15 new accounts being created every day! 

"Wait, did I stumble upon a massive, unicorn success?!?" -- Nope... In fact, all users besides my test accounts were fake - bots - every single one. Major disappointment! 

I panicked -- will Postmark close my account and blacklist my domain?!

No, that's silly, this must happen all of the time, it's basic stuff, just gotta fix it; the Rails Way. 

## What are "bots"?

In the context of the internet and web apps, bots (robots) are automated programs that perform tasks on the web. Some bots are helpful (like search engine crawlers), while others can be disruptive or malicious (like spam bots). 

Bots can imitate human behavior to interact with websites and apps — sometimes so effectively that it’s hard to tell them apart from real users.

My bots are trying to post links that will get clicks. Don't let them!

## Fixing bots the Rails Way

I'm using Rails 8 and Devise for authentication, see [Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html). 

This is the timeline of discovering bot activity and then resolving it without making it too expensive and complicated for me nor too cumbersome for my eventual authentic human users!

Near the end I share my own anti-bot checklist I'm building, many tactics I have yet to try.

## My anti-bot timeline 

With two apps deployed for months, I'm feeling good about life, then the bots arrived...

#### December, 2024 
- 31st - Bot activity first discovered from Postmark alerting me to my monthly email quota!
#### January, 2025 
- 1st - Start studying security and anti-bot tactics. Require email confirmation to access account. 
- 3rd - Disable sign ups and sessions. Add Rails-native rate limiting and paranoid Devise messaging.
- 11th - Add DMARC management in Cloudflare
- 14th - Improve email validation with Ruby's email REGEXP
- 15th - Enable Bot Fight Mode, DNSSEC. Finalize registrar transfer to Cloudflare.
- 20th - Start transfer of all 10 of my domains to Cloudflare
- 24th - Destroy manually all unconfirmed (fake) user accounts 
- 26th - Fly production console machines configuration optimization
#### February 
- 7th - Add Rails rate limiting to password reset
- 18th - Add honeypot to sign up form. Send Welcome email only after user is confirmed. Destroy Stale User Accounts with Solidqueue recurring task. Update Ruby, All gems, and Dockerfile-Related Stuff
- 19th - Reopened sign ups and logins
#### March 
- 12th - Bot attacks re-start!
- 18th - New attack found, re-disable sign ups and sessions
- 22nd - Add hidden timestamp validation
- 23rd - Add two unique honeypot fields
- 30th - Fix SSL Cert issue
#### April 
- 5th - Implement real_ip rate limiting to compensate for Cloudflare's proxy IP defense
- 6th - Re-open for sign-ups and re-enable email sending! 

## My Anti-BOT Checklist for web app form spam prevention

Here's my own way to organize different anti-bot measures, from top to bottom. Which tactics am I missing?

### My app's DNS
1. DDoS protection
2. DNSSEC
3. Privacy for your contact details
4. Bot Fight Mode with JavaScript Detections 
5. Record proxying
6. Email authentication records: SPF, DKIM, and DMARC

### My app's host (Fly.io)
1. TLS, or Transport Layer Security - a cryptographic protocol that provides secure communication over a computer network
2. Memory-Safe Rust Proxy
3. Autostop/ Autostart

### My app's code 
1. IP-based activity
    - Rate limiting actions on IP or other attribute to reduce brute force attacks 
2. Authentication
    1. Paid only! $$ - Bots are usually thwarted by payments. Accepting payment before user creation is a bot filter.
    2. Oauth with Google, Facebook, Github, etc.
    3. Email authentication with Devise, Rails Auth, etc. 
        1. Limit sign in attempts
        2. Limit password reset emails
        3. Email validation (prove it's well-formed)
        4. Email verification (prove it can receive mail)
        5. Email confirmation (prove user has access)
        7. Generic error messages - Devise's paranoid mode
        7. [CAPTCHAs](https://edgeguides.rubyonrails.org/security.html#captchas)
            1. Google Recaptcha gem (Positive)
            2. Honeypot - hidden form field (Negative)

## Other Thoughts

### Visibility into bot activity

I'm sending myself an email with data about the deterred registrant  when the honeypot gets triggered. I review to see patterns to know how to adjust.

### App server availability and spam

Using Fly.io, I had each on the smallest possible configuration that would still run the apps while keeping costs as low as possible. This entailed the app servers shutting down with inactivity, the result was a slower/cold start but it was great because I had no users yet. 

My theory is that in this relatively "unavailable" state, my aps were protected from spam bots. Since the cold startup issue, perhaps bots would not wait around long enough fro my slow site to load? Why else would the bots suddenly attack both my apps? Seems like more than just a coincidence.

## Summary

When my new Rails 8 apps were exposed to the world wide web, the incessant spam bot bullies to tried and knock my app's doors down. I responded with an app made of ruby-colored bricks. 

## Resources

1. [Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html) 
2. "[Stopping spambots with hashes and honeypots](https://nedbatchelder.com/text/stopbots.html)" by Ned Batchelder - More sophisticated negative CAPTCHAs. 
