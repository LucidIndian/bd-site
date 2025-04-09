---
layout: post
title:  "Spam Bots Almost Wrecked my New Rails App - What I Did to Stop Them"
date:   2025-4-7 00:00:00 -0700
categories: rails coding
tags: slopecs rails coding bots spam
image: /assets/honeypot_bots_blue_drumlin.png
---

## My first Rails apps deployed

About a year ago I launched (deployed) my first two Rails apps, [GeoGardening](https://geogardening.app/) and [SlopeCS](https://slopecs.com/) with fly.io and everything was great. I was still building, testing - learning how to get "Hello World" out to the actual world for the very first time. Then, on New Years Eve 2024, all of that changed and I was thrust into a 4-month ongoing battle against the spam bots.

### Getting to the BOT-tom of suspicious sign ups

Shortly after upgrading my apps' servers in late 2024 to be "always on", they each suddenly received A TON of activity and I didn't find out until it was too late.

My apps have email authentication, password reset, and send a welcome email after a User account is created; pretty basic stuff, right?

One day I received an email from Postmark, my email service provider, noting that I had reached my monthly quota of 100 emails on the free plan. 

"Wait, what?! I didn't do that much testing this month? Maybe it's real users?" 

I logged into Postmark to find over 140 "Welcome" and "password reset" emails were sent with a very high bounce and spam rate, hurting my deliverability score, and immediately filling my monthly quota by + 40%! Many of the emails looked legit, @gmail domains, but the usernames were suspicious: like kdsjc67df(at)gmail.com

Next, I logged into the production console and looked at the User table in my production database...

Over 1,400 user accounts had been created with about 15 new ones coming in every day! 

"Wait -- did I stumble upon a massive, unicorn success?!"  No... In fact, it turned out all users besides my few test accounts were fake - all created by bots - every single one. Major disappointment! 

I started to panic - will Postmark close my account and blacklist my domain?!

No, this must happen all of the time, it's basic stuff, just gotta fix it; the Rails Way. 

## Fixing bots, the Rails Way

I'm using Rails 8 and Devise for authentication. After Googling and asking AI for tips on how to mitigate these bots, I turned to the Rails Guides to see what they had to say, see [Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html).

### CAPTCHAs, positive and negative

Section [6.3. CAPTCHAs](https://edgeguides.rubyonrails.org/security.html#captchas) from tbe Guides mentions different types of bots and common ways to combat them with two methods of differentiating bots from humans, positive and negative:

#### Positive CAPTCHA

A user proves they are human and the bot fails the test. 

Example: A user completes a test, usually an image-related quiz. 

#### Negative CAPTCHA

A bot proves they are not human and the human passes the test. 

Example: A bot fills the honeypot fields that are invisible to the human. 


I share my own My Anti-BOT Checklist below; in progress, some tactics implemented and others I have yet to try.

## First, what are "bots"?

In the context of the internet and web apps, bots (robots) are automated programs that perform tasks on the web. 

Some bots are helpful (like search engine crawlers), while others can be disruptive or malicious (like spam bots). 

Bots can imitate human behavior to interact with websites and apps — sometimes so effectively that it’s hard to tell them apart from real users.

Some bots are trying to post links that will get clicks. Don't let them!

## My anti-bot timeline 

With two apps deployed for almost a year, I was feeling good about life and coding, then the bots arrived...

Below is my timeline of discovering bot activity and resolving it for free while keeping a nice experience for my eventual authentic human users.

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
- 18th 
    - Add honeypot to sign up form. 
    - Send Welcome email only after user is confirmed. 
    - Destroy Stale User Accounts with Solidqueue recurring task. 
    - Update Ruby, All gems, and Dockerfile-Related Stuff
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

1. My app's DNS (Cloudflare)
    1. DDoS protection
    2. DNSSEC
    3. Privacy for your contact details
    4. Bot Fight Mode with JavaScript Detections 
    5. Record proxying
    6. Email authentication records: SPF, DKIM, and DMARC
2. My app's host (Fly.io)
    1. TLS, or Transport Layer Security - a cryptographic protocol that provides secure communication over a computer network
    2. Memory-Safe Rust Proxy
    3. Autostop/ Autostart
3. My app's code (Ruby on Rails)
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
    3. [CAPTCHAs](https://edgeguides.rubyonrails.org/security.html#captchas)
        1. Google Recaptcha gem (Positive)
        2. Honeypot - hidden form field (Negative)

## Other Thoughts

### App server availability and spam

Using Fly.io, I had each on the smallest possible configuration that would still run the apps while keeping costs as low as possible. This entailed the app servers shutting down with inactivity, the result was a slower/cold start but it was great because I had no users yet. 

My theory is that in this relatively "unavailable" state, my aps were protected from spam bots. Since the cold startup issue, perhaps bots would not wait around long enough for my slower site to load? Why else would the bots suddenly attack both my apps? Seems like more than just a coincidence.

### Visibility into bot activity

I'm sending myself an email with data about the deterred registrant whenever the honeypot gets triggered. The email includes the user's IP, duration to sign up, etc. I review for patterns to know how to adjust my honeypot.

### What worked against the bots?

#### An advanced honeypot

By far, the most effective tactic was the honeypot, or negative CAPTCHA, especially once it was made to be more complicated than just a single field. 

I experienced consistent bot sign ups until the honeypot was installed. Bots were initially thwarted, then able to outsmart my simple honeypot. Making it more complicated with a timestamp validation and several different honeypot fields made the largest difference. 

#### Email confirmation

I have some evidence of bot sign ups that were able to confirm the email, but maybe 95% do not. I found this when sign ups were open for a period and did not require confirmation. 

### What didn't work against the bots?

#### Cloudflare

Surprisingly, I thought moving to Cloudflare for DNS and enabling their Bot Fight Mode would have been enough to stop the fraudulent sign ups.

In their defense: 
- I'm on the free plan and perhaps paid is REALLY better for this
- Maybe better configuration of other settings would help
- My sites benefit in other ways from their anti-spam features, I'm grateful for that.

#### A simple honeypot

A single honeypot field was not enough. After a few weeks bots seemed to "figure it out" or get lucky by avoiding that field upon registration. I had to go back to study and push a more sophisticated honeypot.

#### Email validation

Upon my non-expert manual visual review, most if not all of the thousands of bot sign ups seem to be associated with well-formed emails, I do not even see many "disposable" emails. Enhancing this slightly, as I did, or even more does not seem matter much. 

## What's next?

### Positive CAPTCHa?

I wonder if my sophisticated honeypot will fail to be enough one day. A Turnstile by Cloudflare or the reCAPTCHA from Google are on my to-do list.

### Paid only or Freemium?

Using a pay wall to inhibit account creation seems like a win-win but aren't there benefits of a free plan? Maybe a free plan with credit card validation as an additional measure?

### Email verification?

Proving an email address actually exists and can receive mail through verification before accepting it is different and feels more promising to help avoid nonexistent registrants (fake emails).

## Summary

When my new Rails 8 apps were exposed to the world wide web and made readily available, the spam bot bullies attacked and incessantly to tried and knock my app's doors down. 

I responded by learning their tricks, implementing simple and well-advocated counter measures to avoid filling my database and email quota with their gibberish. 

The result; an app made of glimmering ruby-colored bricks that is now much less-penetrable by the evil robots of the web. 

## Resources for anti-bot security 

1. "[Securing Rails Applications](https://edgeguides.rubyonrails.org/security.html)" from the Ruby on Rails Guides.
2. "[Stopping spambots with hashes and honeypots](https://nedbatchelder.com/text/stopbots.html)" by Ned Batchelder - A more sophisticated negative CAPTCHA. 
3. "[How To: Add :confirmable to Users](https://github.com/heartcombo/devise/wiki/How-To:-Add-:confirmable-to-Users)" from heartcombo / devise.
4. "[Brute-Forcing Accounts](https://edgeguides.rubyonrails.org/security.html#brute-forcing-accounts)" from the Ruby on Rails Guides, reviews the built-in rate-limiter to protect your registration and session forms.
