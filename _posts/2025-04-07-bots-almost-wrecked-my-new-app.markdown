---
layout: post
title:  "Spam Bots Almost Wrecked my New Rails App - What I Did to Stop Them"
date:   2025-4-7 00:00:00 -0700
categories: rails coding
tags: slopecs rails coding bots spam
image: /assets/honeypot_bots_blue_drumlin.png
---

## My first Rails apps deployed

About a year ago I launched (deployed) my first two Rails apps, [GeoGardening](https://geogardening.app/) and [SlopeCS](https://slopecs.com/) with fly.io and everything was great. I was still building, testing - learning how to get "Hello World" out to the actual world for the very first time. Then, on New Years Eve 2024, all of that changed and I was thrust into a 4-month ongoing battle against the spambots. 

Further below, I share my timeline and my own Anti-BOT Checklist. Some tactics implemented and others I have yet to try.

### Getting to the BOT-tom of suspicious sign ups

Shortly after upgrading my apps' servers in late 2024 to be "always on" or not suspended, they each suddenly received A TON of activity and I didn't find out until it was too late.

My apps use email-based authentication, password reset, and send a welcome message after a User account is created; pretty basic stuff, right?

That was until that one day I received an email from Postmark, my email service provider, noting that I had surpassed my monthly quota of 100 emails on their free plan. 

"Wait, what?! I didn't do THAT much testing this month. Maybe these are real users?" 

I logged into Postmark to find over 140 "Welcome" and "Password reset" emails were sent with a very high bounce and spam rate, hurting my deliverability score, and immediately filling my monthly quota by + 40%! Many of the emails looked legit, @gmail domains, but the usernames were suspicious: like `kdsjc67df(at)gmail.com`

Next, I logged into the production console and looked at the User table in my production database...

Over 1,400 user accounts had been created with about 15 new ones coming in every day! 

"Wait - did I stumble upon a massive, unicorn success?!"  

No... In fact, it turned out all users besides my few test accounts were fake - all created by bots - every single one. Big disappointment! 

I started to worry - will Postmark penalize me or close my account and blacklist my domain?!

No, this must happen all of the time, it's basic stuff, just gotta fix it; the Rails Way. 

## Fixing bots, the Rails Way

I'm using Rails 8 and Devise for authentication. After Googling, asking AI, and the X community for tips on how to mitigate these bots, I turned to the authoritative Rails Guides to see what they had to say, see [Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html).

### CAPTCHAs, positive and negative

Particularly interesting is Section [6.3. CAPTCHAs](https://edgeguides.rubyonrails.org/security.html#captchas) from the Guides. It describes different types of bots and common ways to combat them with two methods of differentiating bots from humans, positive and negative CAPTCHAs.

#### Positive CAPTCHA

A user proves they are human with a test and the bot fails. 

Example: A user completes a test to submit the form, usually an image-related quiz, which validates the submission. 

#### Negative CAPTCHA

A bot proves they are not human with a test and the human passes. 

Example: A bot completes the invisible honeypot form fields which discards the submission. 

## First, what are "bots"?

In the context of the internet and websites, bots (robots) are automated programs that perform tasks on the web. 

Some bots are helpful (like search engine crawlers), while others can be disruptive or malicious (like spam bots). 

Bots can imitate human behavior to interact with websites and apps — sometimes so effectively that it’s hard to tell them apart from real users.

Some bots are trying to post links that will get clicks. Don't let them!

## My anti-bot timeline 

With two apps deployed for almost a year, I was feeling good about life and coding, then the bots arrived...

Below is my timeline of discovering bot activity and resolving it for free while keeping a nice experience for my eventual authentic human users.

#### December, 2024 
- 31st - Bot activity first discovered from Postmark alerting me to my monthly email quota!

#### January, 2025 
- 1st - Start studying security and anti-bot tactics
    - Require email confirmation to access account
    - Ask the Rails community on X for advice. Special thanks to those who replied to help build by tactic list: @bchecketts, @MichaelDChaney, @yarotheslav, @tomcnle, and @paraxialio:
<blockquote class="twitter-tweet"><p lang="en" dir="ltr">Soon after deploying my Rails 8 app with Devise, it got bombarded by bots causing the app to send 100 Welcome and PW reset emails to basically nobody! <br><br>After adding the Confirmable module, what’s the best way to avoid sending tons of confirmation emails to fake addresses?</p>&mdash; Tygh Walters (@TyghWalters) <a href="https://twitter.com/TyghWalters/status/1874702583962705953?ref_src=twsrc%5Etfw">January 2, 2025</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script>

- 3rd - Disable new sign ups, sessions, and email-sending
    - Add Rails rate limiting to registration form
    - Add paranoid messaging for Devise authentication
- 11th - Add DMARC management in Cloudflare
- 14th - Improve email validation with Ruby's email REGEXP
- 15th - Enable Bot Fight Mode, DNSSEC. 
    - Finalize registrar transfer to Cloudflare
- 20th - Start transfer of all 10 of my domains to Cloudflare
- 24th - Destroy manually all unconfirmed (fake) user accounts 
- 26th - Fly production console machines configuration optimization

#### February 
- 7th - Add Rails rate limiting to password reset
- 18th 
    - Add honeypot to sign up form
    - Send Welcome email only after user is confirmed
    - Destroy stale User accounts with Solid Queue recurring task
    - Update Ruby, all gems, and Dockerfile stuff
- 19th - Reopened sign ups and logins

#### March 
- 12th - Bot attacks re-start and again, I surpass my monthly email quota!
- 18th - New attack found
    - Re-disable sign ups and sessions until fixed
- 22nd - Add hidden timestamp validation
- 23rd - Add two unique honeypot fields
- 30th - Fix TLS cert expiration issue

#### April 
- 5th - Implement real_ip rate limiting to compensate for Cloudflare's proxy IP defense
- 6th - Re-enable sign-ups, logins, and email sending! 

Since early April, so far so good!

## My anti-bot checklist for web app form spam prevention

Here's my way to organize the various anti-bot measures I found, from top to bottom. What am I missing?

1. Domain Name System (DNS) Management
    1. DNSSEC - a set of cryptographic protocols that enhance the security of the DNS.
    2. Privacy for contact details
    3. Email authentication records: SPF, DKIM, and DMARC
    4. [Bot Fight Mode](https://developers.cloudflare.com/bots/get-started/bot-fight-mode/) with JavaScript Detections (Cloudflare)
    5. Record proxying - optimize, cache, and protect all requests to an app
        - DDoS (Distributed Denial of Service) protection
2. App Host
    1. TLS, or Transport Layer Security - a cryptographic protocol that provides secure communication over a computer network
    2. Autostop/ Autostart
3. App code
    1. IP-based activity
        - Rate limiting actions on the IP address (location) of the request or other to reduce brute force attacks. See "[Brute-Forcing Accounts](https://edgeguides.rubyonrails.org/security.html#brute-forcing-accounts)" for more.
    2. Authentication
        1. Oauth with Google, Facebook, Github, etc.
            - Let a large organization with massive resources worry about the bots. 
        2. Email authentication with Devise, Rails Auth, etc. 
            1. Limit sign in attempts
            2. Limit password reset emails
            3. Email validation (prove address is well-formed)
            4. Email verification (prove address can receive mail)
            5. Email confirmation (prove user has access to email)
            7. Generic error messages - Devise's paranoid mode. This prevents attempts to "guess" accounts, or account enumeration, by avoiding sharing identifiable or revealing data to the user.
    3. Authorization
        1.  Paid only - Bots are usually thwarted by payments. Accepting payment before User creation may be a better bot filter.
    4. [CAPTCHAs](https://edgeguides.rubyonrails.org/security.html#captchas)
        1. Google Recaptcha gem (Positive)
        2. Honeypot - hidden form field (Negative)
            - See, "[Stopping spambots with hashes and honeypots](https://nedbatchelder.com/text/stopbots.html)"

## App server availability and spam

Using Fly.io, I had each on the smallest possible machines configuration that would still run the apps while keeping costs as low as possible. This entailed the app servers shutting down with inactivity, the result was a slower/cold start but it was great because I had no users yet. 

My theory is that y aps were protected from spam bots while in this relatively "unavailable" state. Perhaps bots would not wait around long enough for my slower site to load? Why else would the bots suddenly attack both my apps at the same time? Seems like more than just a coincidence.

## Visibility into bot activity

I'm sending myself an email with data about the deterred bot whenever the honeypot catches one. The email includes the IP, duration to sign up, etc. I review for patterns to know how and if to adjust my honeypot.

## What worked against the bots?

### An advanced honeypot

By far, the most effective tactic was the honeypot, especially once it was made to be more than just a single text field. 

I experienced consistent bot sign ups until the honeypot was installed. Bots were initially thwarted, then able to outsmart my simple honeypot. 

Making it more complicated with a timestamp validation and several different honeypot fields made the largest difference. 

### Email confirmation

I have some evidence of bot registrations that were able to confirm the email, but maybe 95% do not. I found this when sign ups were open for a period and did not require confirmation. 

## What didn't work against the bots?

### Cloudflare

Surprisingly, I thought moving to Cloudflare for DNS and enabling their Bot Fight Mode would have been enough to stop the fraudulent sign ups.

In their defense: 
- I'm on the free plan and perhaps paid is REALLY better for this
- Maybe better configuration of other settings would help
- My sites benefit in other ways from their anti-spam features, I'm grateful for that.

### A simple honeypot

A single honeypot field was not enough. After a few weeks bots seemed to "figure it out" or get lucky by avoiding that field upon registration. I had to go back to study and push a more sophisticated honeypot.

### Email address validation

Upon my non-expert manual visual review, most if not all of the thousands of bot sign ups seem to be associated with well-formed emails, I do not even see many "disposable" emails. Enhancing this slightly, as I did, or even more does not seem to matter much. 

## What's next?

### Better rate limiting with Solid Cache

Right now, I'm using MemoryStore as my production cache which I've read has drawbacks, especially for rate limiting IPs. 

If I understand correctly, a user could theoretically duplicate their abuse on each active Ruby process, since each process does not have access to the others cache. A database-backed system avoids that by having a source of truth to reference that is durable and consistent.

### Positive CAPTCHa?

I wonder if my sophisticated honeypot will fail to be enough one day. The reCAPTCHA from Google is on my list if more advanced form defense is needed but I'd rather not.

### Paid only or freemium?

Using a paywall to inhibit account creation seems like a win but aren't there benefits of a free plan? Maybe a limited free plan with credit card validation as an additional measure? 

### Email address verification?

Proving an email address actually exists and can receive mail before accepting it is different and feels more promising to help avoid nonexistent registrants (phony emails). 

## Summary

When my new Rails 8 apps were exposed to the world wide web and made readily available, the spam bot bullies attacked and incessantly tried to knock my apps' doors down. 

I responded by learning their tricks, implementing simple and effective counter measures to avoid filling my database and email servers with their gibberish. 

The result; an app made of glimmering ruby-colored bricks made much less-penetrable by the evil robots of the web.

## Resources for anti-bot security

1. "[Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html)" from the Ruby on Rails Guides.
2. "[Stopping spambots with hashes and honeypots](https://nedbatchelder.com/text/stopbots.html)" by Ned Batchelder - A more sophisticated negative CAPTCHA. 
3. "[How To: Add :confirmable to Users](https://github.com/heartcombo/devise/wiki/How-To:-Add-:confirmable-to-Users)" from heartcombo / devise.
4. "[Brute-Forcing Accounts](https://edgeguides.rubyonrails.org/security.html#brute-forcing-accounts)" from the Ruby on Rails Guides, reviews the built-in rate-limiter to protect your registration and session forms.
