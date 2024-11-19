---
layout: post
title:  "Shopify Apps on Rails?"
categories: rails coding
# permalink: /2024/11/01/rails-world-2024-recap.html
tags:
image: /assets/bd_logo500pxsquare.png
#   path: 
#   height: 300
#   width: 
#   alt: 
---

I’m a newcomer to Rails. My perspective is naïve. I’m uninformed and ignorant. Yet, in my ignorance, I’ve encountered a peculiar confusion about Rails and Shopify I’ve become determined to understand. 

After attending my first web dev conference and writing my [Rails World 2024 Recap](https://bluedrumlin.com/2024/10/01/rails-world-2024-recap.html), I wanted to share more on what I've learned trying to build a Shopify app with Ruby on Rails 8, and especially, why it is not easier to do so.

I’ve never worked at Shopify and I’ve only been inside their building once. I could have this all backwards, but this is the current perspective of a curious, interested outside observer. Hopefully, it’s at least entertaining! ;)

---

## My Programming and Rails Context

My first experience with programming (Matlab) was in 2010. My first web intro (HTML and CSS) happened in 2012. I started learning JavaScript and Rails 6 in 2019.

From my very first exposure to Rails, the connection between Rails and its biggest adopters, Basecamp, GitHub, and, most notably, Shopify, were obvious. These companies are often cited as the big and successful examples that succeed, an demonstration of what is possible with the framework.

At Rails World 2024, I heard a Shopify dev share an incredible fact: **hundreds of Rails apps power Shopify**. While this number has decreased from what it once was, it’s still shocking to me. These hundreds of Rails apps seem to form a hidden network of interconnected systems, each managing a slice of the Shopify experience for shoppers and users. 

---

## Shopify’s Commitment to Rails Appear Strong

Shopify’s investment in Rails is clear:

- Shopify sponsors **Rails World**, showcasing its dedication to the framework's future
- The company hires some of the most talented Ruby and Rails developers, solving problems at the highest scale  
- Rails users, like me, benefit immensely from Shopify’s innovations trickling down into the open-source framework

Even Shopify’s co-founder & CEO, Tobi Lütke, is a Rails enthusiast. A former core contributor to the framework, his admiration for Rails was evident during the [Rails World 2024 fireside chat](https://www.youtube.com/watch?v=zPBbHu-BKpQ) with DHH (David Heinemeier Hansson) and Matz (Yukihiro Matsumoto).

Further, Shopify emphasized at RW24 that struggles with managing large codebases is less about the language or framework and more about organizational culture, decision-making, and communication. This refreshing perspective hints that Shopify remains dedicated to Rails and they're not convinced that "scalability" is an insurmountable, inherent weaknesses of Rails itself.

From the outside, it feels like Shopify, Ruby, and Rails are deeply intertwined, thriving together.

---

## The Seed of My Confusion

My interest in Shopify stems from my work with [SellerSmile](https://sellersmile.com), the customer service agency I co-founded nearly a decade ago. We’ve supported dozens of Shopify merchants and will continue to do so for years to come.

I wanted to build a Shopify app in the only way I knew, Rails. My goal was to create something useful for my customer service team.

When I began studying how to create a Shopify app, Rails was there but hard to find, and that’s when the discouraged confusion set in.

- Do I have to learn React in order to use Rails to build a Shopify App?
- What is Remix and should I learn that instead of React?
- Am I making this too hard on myself by trying to do it "the simple way" (without React) in Rails?

---

## Where’s Rails in Shopify’s App Ecosystem?

Shopify has excellent [developer documentation](https://shopify.dev/docs). However, it's obvious that while Rails is mentioned and technically supported, **it’s clearly not the preferred path**. Instead, Shopify heavily prefers **[Remix](https://remix.run/)**, a JavaScript framework.

I finally learned why at Rails World 2024. Remix became owned by Shopify in 2022, it makes sense they’d highlight their own tool, but as a new Rails dev, I'd never even heard of Remix before diving into Shopify’s app ecosystem.

---

## The Rails Tools Are Helpful… But

Shopify provides several tools for Rails devs, including:

- The [Ruby Shopify app template](https://github.com/Shopify/shopify-app-template-ruby)
- The [shopify_app gem](https://github.com/Shopify/shopify_app)
- The [shopify_api gem](https://github.com/Shopify/shopify-api-ruby)

As great as these may be, today, some are outdated. For example, the official Ruby app template is still for Rails 7.1, while Rails 7.2 and then 8.0 have been released. 

In February 2024, a helpful dev submitted an issue about this, "[Rails 8, Hotwire, Stimulus, no react](https://github.com/Shopify/shopify-app-template-ruby/issues/122)" leading to Shopify to create a wiki, "[Replacing React frontend with Stimulus](https://github.com/Shopify/shopify-app-template-ruby/wiki/Replacing-React-frontend-with-Stimulus)". I tested this approach and, after some initial confusion and errors, managed to get my app working de-React-ed. Still, it was clear that Rails apps, and especially Rails apps without React are treated as second-class options compared to Remix in Shopify’s ecosystem.

---

## My Hope for Rails and Shopify

Here’s what I hope to see: modern, standard Ruby on Rails apps treated as first-class options alongside Remix. Specifically, I’d like:

1. **Parity in Documentation and Support**  
   Shopify’s Remix documentation is top-notch. If Rails had the same level of depth, quality, and app examples, it could further lower the barrier for developers to create Shopify apps using Rails.

2. **Stronger Recruitment for Rails Developers**  
   Since Shopify is built on hundreds of Rails apps, supporting the framework has to help themselves in the long run. By enhancing the Rails developer experience for building Shopify apps, they could inspire more devs to create Shopify apps with Rails, to become Rails developers,etc. Eventually, the successful Rails apps will need to hire. Many Rails devs could eventually join a Shopify app or Shopify itself to work on its expanding Rails codebase.

---

## Why This Matters to (People Like) Me

As a Rails learner, it already feels like a steep on-ramp. I don’t want to learn and juggle more frameworks like Remix or React. 

Beyond my personal struggles, this is more about philosophical alignment. 

Like Rails, Shopify seems to advocate for **less complexity**.

In their article, [General best practices for app performance](https://shopify.dev/docs/apps/build/performance/general-best-practices#reduce-your-dependency-on-external-frameworks-and-libraries), Shopify clearly states what I believe Rails is also saying:   
- "If you need to use JavaScript, consider avoiding introducing third-party frameworks, libraries, and dependencies"
- "...use native browser features and modern DOM APIs whenever possible."
- "Frameworks such as React, Angular,... Vue,... jQuery have significant performance costs" 

Rails 8 could be a fantastic match for Shopify’s ethos, requiring/relying on fewer third-party frameworks.

---

## A Beginner’s Journey to the Outer Edge

This mission into Shopify apps represents my first attempt into the “outer edge” of development. For years, I followed rigid tutorials with definitive outcomes. Now, I’m navigating the unknown, trying to solve problems that aren’t predefined. 

Rails and Shopify have inspired me to embrace this mystery, share my findings, and grow as a developer. My hope is that sharing these experiences will collectively improve the Rails developer journey for Shopify apps.

My next focus is to build, design, then launch a standard Rails app that is compatible as an embedded Shopify app and available on the app store. More to come soon!
