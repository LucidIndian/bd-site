# Shopify Apps on Rails: A Beginner's Journey Through Confusion

I’m a newcomer. My perspective is naïve, and I’m uninformed and ignorant in many ways. Yet, in my ignorance, I’ve encountered a great confusion—a puzzle I’ve become determined to solve.

I’ve never worked at Shopify, and I’ve only been inside their building once. So, I might have this all wrong, but here’s the perspective of a curious outside observer. Hopefully, it’s at least interesting or entertaining.

---

## My Programming Roots and Rails Beginnings

I had my first experience with programming around 2010 and my first web development introduction in 2012. I started learning Rails 6 in 2019.

From my very first exposure to Rails, I noticed a recurring theme: Rails’ connection to its biggest adopters. Companies like GitHub, Basecamp, and, most notably, Shopify are often cited as the giants who’ve thrived with Rails.

At Rails World 2024, Shopify developers shared an incredible statistic: **hundreds of Rails apps power Shopify**. While this number has decreased from what it once was, it’s still astounding. These apps form a network of interconnected systems, each managing a slice of the Shopify experience. 

Shopify emphasized that managing large codebases is less about the language or framework and more about organizational culture, decision-making, and communication. It was a refreshing perspective that showed Rails remains deeply integrated into Shopify's DNA.

---

## Shopify’s Commitment to Rails

Shopify’s investment in Rails is clear:

- Shopify sponsors **Rails World**, showcasing its dedication to the framework's future.  
- The company hires some of the most talented Ruby and Rails developers in the world, solving problems at an unparalleled scale.  
- Open-source Rails users, like me, benefit immensely from Shopify’s innovations trickling down into the framework.  

Even Shopify’s CEO, Tobi Lütke, is a Rails enthusiast. A former core contributor to the framework, Tobi’s admiration for Rails was evident during his fireside chat with DHH (David Heinemeier Hansson) and Matz (Yukihiro Matsumoto).

From the outside, it feels like Shopify and Rails are deeply intertwined and thriving together.

---

## The Seed of My Confusion

My strong interest in Shopify stems from my work with [SellerSmile](https://sellersmile.com), the customer service agency I co-founded nearly a decade ago. We’ve supported dozens of Shopify merchants and will continue to do so for years to come.

I wanted to deepen this connection by building a Shopify app with Rails. My goal was to create something useful for my team, like an app that helps merchants automate their shipping policies—a feature I noticed was missing from Shopify’s admin tools.

But when I began exploring how to create a Shopify app, that’s when the discouraged confusion started.

---

## Where’s Rails in Shopify’s App Ecosystem?

Shopify has excellent developer documentation. However, after spending many hours reading it, it became obvious that while Rails is mentioned and supported, **it’s clearly not the preferred path**. Instead, Shopify heavily promotes **[Remix](https://remix.run/)**.

At Rails World 2024, I finally understood why. Remix is a Shopify-owned framework, so it makes sense they’d highlight their own tool. But as a new Rails developer, I had never even heard of Remix before diving into Shopify’s ecosystem.

---

## The Rails Tools Are Helpful… But Outdated

Shopify provides several Rails tools, including:

- The **official[ Ruby app template](https://github.com/Shopify/shopify-app-template-ruby)**
- The **[shopify_app gem](https://github.com/Shopify/shopify_app)**
- The **[shopify_api gem](https://github.com/Shopify/shopify-api-ruby)**

As great as they may be, today, these resources are outdated. For example, the official Rails template is still designed for Rails 7.1, while Rails 7.2 and then 8.0 came out. A helpful developer submitted an issue about this, leading to Shopify to create a wiki on replacing React with Stimulus for a modern Rails 8 app.

I tested this approach and, after some initial confusion and errors, managed to get my app working de-React-ed. Still, it was clear that **Rails apps, and especially Rails apps without React are treated as second-class options compared to Remix** in Shopify’s ecosystem.

---

## My Hope for Rails and Shopify

Here’s what I hope to see: modern, standard ruby on Rails apps treated as first-class options alongside Remix. Specifically, I’d love to see:

1. **Parity in Documentation and Support**  
   Shopify’s Remix documentation is top-notch. If Rails had the same level of depth, quality, and examples, it could lower the barrier for Rails developers to create Shopify apps.

2. **Stronger Recruitment for Rails Developers**  
   Shopify is built on many Rails apps, so supporting the framework helps the company in the long run. By enhancing the Rails developer experience, Shopify could inspire more Rails developers to create Shopify apps. Some of these developers might eventually join Shopify to work on its Rails codebase.

---

## Why This Matters to (People Like) Me

As a Rails learner, I don’t want to juggle new frameworks like Remix or React. It’s a steep on-ramp for someone like me, an advanced beginner trying to make a real-world app. But beyond my personal struggles, this is about alignment. 

Shopify advocates for **less complexity**, and modern Rails aligns perfectly with that vision. The updated Rails way—less JavaScript, less complexity—could be a fantastic match for Shopify’s ethos.

In, [Reduce your dependency on external frameworks and libraries](https://shopify.dev/docs/apps/build/performance/general-best-practices#reduce-your-dependency-on-external-frameworks-and-libraries), Shopify clearly states what I believe Rails is saying,  
- "If you need to use JavaScript, consider avoiding introducing third-party frameworks, libraries, and dependencies"
- "...use native browser features and modern DOM APIs whenever possible."
- "Frameworks such as React, Angular,... Vue,... jQuery have significant performance costs" 

---

## A Beginner’s Journey to the Outer Edge

This journey into Shopify apps represents my first foray into the “outer edge” of development. For years, I followed rigid tutorials. Now, I’m navigating the unknown, trying to solve problems that aren’t predefined. 

Shopify’s ecosystem has inspired me to embrace this mystery, share my findings, and grow as a developer. My hope is that by voicing these experiences, we can collectively improve the Rails developer journey for Shopify apps.
