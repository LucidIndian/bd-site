---
layout: post
title:  "Shopify Apps on Rails: A Beginner's Journey Through Confusion"
categories: rails coding
# permalink: /2024/11/01/rails-world-2024-recap.html
tags:
image: /assets/bd_logo500pxsquare.png
#   path: 
#   height: 300
#   width: 
#   alt: 
---
# Shopify Apps on Rails: A Beginner's Journey Through Confusion

I’m a newcomer. My perspective is naïve, and I’m uninformed and ignorant in many ways. Yet, in my ignorance, I’ve encountered a great confusion—a puzzle about Rails and Shopify I’ve become determined to solve. 

I’ve never worked at Shopify, I've built 0 Shopify apps, and I’ve only been inside their building once. I might have this all wrong, but this post is the perspective of a curious outside observer. Hopefully, it’s at least interesting or entertaining! ;)

---

## My Programming Roots and Rails Beginnings

My first experience with programming (Matlab) was in 2010 and my first web dev introduction (HTML and CSS) was in 2012. I started learning Rails 6 in 2019.

From my very first exposure to Rails, I noticed Rails’ connection to its biggest adopters. GitHub, Basecamp, and, most notably, Shopify are often cited as the giants who’ve thrived with Rails, the examples of what is possible.

At Rails World 2024, Shopify devs shared an incredible statistic: **hundreds of Rails apps power Shopify**. While this number has decreased from what it once was, it’s still amazing. These apps seem to form a hidden network of interconnected systems, each managing a slice of the Shopify experience. 

Shopify emphasized that managing large codebases is less about the language or framework and more about organizational culture, decision-making, and communication. It was a refreshing perspective that showed Rails remains deeply integrated into Shopify's DNA.

---

## Shopify’s Commitment to Rails

Shopify’s investment in Rails is clear:

- Shopify sponsors **Rails World**, showcasing its dedication to the framework's future
- The company hires some of the most talented Ruby and Rails developers, solving problems at the highest scale  
- Rails users, like me, benefit immensely from Shopify’s innovations trickling down into the open-source framework

Even Shopify’s CEO, Tobi Lütke, is a Rails enthusiast. A former core contributor to the framework, his admiration for Rails was evident during the [Rails World 2024 fireside chat](https://www.youtube.com/watch?v=zPBbHu-BKpQ) with DHH (David Heinemeier Hansson) and Matz (Yukihiro Matsumoto).

From the outside, it feels like Shopify, Ruby, and Rails are deeply intertwined and thriving together.

---

## The Seed of My Confusion

My strong interest in Shopify stems from my work with [SellerSmile](https://sellersmile.com), the customer service agency I co-founded nearly a decade ago. We’ve supported dozens of Shopify merchants and will continue to do so for years to come.

I wanted to deepen this connection by building a Shopify app with Rails. My goal was to create something useful for my team, like an app that helps merchants automate their shipping policies—a feature I noticed was missing from Shopify’s admin tools.

But when I began exploring how to create a Shopify app, that’s when the discouraged confusion started.

---

## Where’s Rails in Shopify’s App Ecosystem?

Shopify has excellent [developer documentation](https://shopify.dev/docs). However, after spending many hours reading it, it became obvious that while Rails is mentioned and supported, **it’s clearly not the preferred path**. Instead, Shopify heavily prefers **[Remix](https://remix.run/)**.

At Rails World 2024, I finally learned why. Remix became a Shopify-owned framework in 2022, so it makes sense they’d highlight their own tool. But as a new Rails developer, I had never even heard of Remix before diving into Shopify’s ecosystem.

---

## The Rails Tools Are Helpful… But

Shopify provides several Rails tools, including:

- The official[ Ruby app template](https://github.com/Shopify/shopify-app-template-ruby)
- The [shopify_app gem](https://github.com/Shopify/shopify_app)
- The [shopify_api gem](https://github.com/Shopify/shopify-api-ruby)

As great as they may be, today, some are outdated. For example, the official Ruby app template is still for Rails 7.1, while Rails 7.2 and then 8.0 came out. 

In February 2024, a helpful dev submitted an issue about this, "[Rails 8, Hotwire, Stimulus, no react](https://github.com/Shopify/shopify-app-template-ruby/issues/122)" leading to Shopify to create a wiki, "[Replacing React frontend with Stimulus](https://github.com/Shopify/shopify-app-template-ruby/wiki/Replacing-React-frontend-with-Stimulus)". I tested this approach and, after some initial confusion and errors, managed to get my app working de-React-ed. Still, it was clear that Rails apps, and especially Rails apps without React are treated as second-class options compared to Remix in Shopify’s ecosystem.

---

## My Hope for Rails and Shopify

Here’s what I hope to see: modern, standard Ruby on Rails apps treated as first-class options alongside Remix. Specifically, I’d love to see:

1. **Parity in Documentation and Support**  
   Shopify’s Remix documentation is top-notch. If Rails had the same level of depth, quality, and examples, it could lower the barrier for Rails developers to create Shopify apps.

2. **Stronger Recruitment for Rails Developers**  
   Since Shopify is built on many Rails apps, supporting the framework helps the company in the long run. By enhancing the Rails developer experience for building Shopify apps, they could inspire more devs to create Shopify apps with Rails. Eventually, these apps will need to hire. These Rails devs might eventually join a Shopify app or Shopify itself to work on its Rails codebase.

---

## Why This Matters to (People Like) Me

As a Rails learner, I don’t want to juggle too many frameworks like Remix or React. It already feels like a steep on-ramp for someone like me, an advanced beginner trying to make a real-world app.

Beyond my personal struggles, this is more about alignment. 

Like Rails, Shopify seems to advocate for **less complexity**.

In, [General best practices for app performance](https://shopify.dev/docs/apps/build/performance/general-best-practices#reduce-your-dependency-on-external-frameworks-and-libraries), Shopify clearly states what I believe Rails is saying as well:   
- "If you need to use JavaScript, consider avoiding introducing third-party frameworks, libraries, and dependencies"
- "...use native browser features and modern DOM APIs whenever possible."
- "Frameworks such as React, Angular,... Vue,... jQuery have significant performance costs" 

The updated Rails way—less JavaScript, less complexity—could be a fantastic match for Shopify’s ethos.

---

## A Beginner’s Journey to the Outer Edge

This path into Shopify apps represents my first attempt into the “outer edge” of development. For years, I followed rigid tutorials with definitive outcomes. Now, I’m navigating the unknown, trying to solve problems that aren’t predefined. 

Rails and Shopify have inspired me to embrace this mystery, share my findings, and grow as a developer. My hope is that by voicing these experiences, we can collectively improve the Rails developer journey for Shopify apps.

The next focus is to build, design, and launch a standard Rails app that is compatible as a Shopify app on the app store. More to come soon!
