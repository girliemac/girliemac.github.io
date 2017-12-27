---
title: Developer Experience Matters
author: Tomomi Imura
layout: post
description: A summary of my talk I gave at DevRel Summit in Seattle
images:
  - /assets/images/articles/2016/08/dx-jamie-comic.jpg
categories:
  - DevRel
  - Developer
  - DevTools
  - API
  - DX
---

*I am writing this article based on the short talk I gave at [DevRel Summit](http://www.devrelsummit.com/) in Seattle, and it is aimed for my fellow developer advocates, platform engineers, product managers, and CTOs, who work for companies that provide developer platforms, APIs etc. also anybody who advocate their own software / libraries / frameworks*

---
![Developer Experience Matters](/assets/images/articles/2016/08/dx-jamie-comic.jpg)

Let’s say, you are working for a company that provides public APIs, or you are an open-source JavaScript library author, who want to attract developers out there to use your products.

When your potential developers, who are in search for a solution for a new project- this can be a large-scale commercial project, or it could be to compete at a hackathon, see your shiny website but has very poorly-designed developer portal (or your open-source project on GitHub may have some stars, but with no README), how does the developer feel? Do they still want to try it out anyway, or keep searching something else and end up choosing your competitor?

I have been working as a developer evangelist, or related positions in Developer Relations for about six years for three (technically four, including acquisition) different companies, to advocate both proprietary and open technologies. From the experiences, what I've seen is that developers (including myself) tend to shy away when the API (or platform, services, etc.) is poorly designed, lacks good docs, Get Started guide, or code samples.

This **Developer Experience** is one of the biggest key factors for developers to decide if they use certain technologies to use.

## User Experience and Developer Experience

Before becoming a developer evangelist, I was working as a developer in Human Interface team for **Palm webOS** mobile platform. Although we didn't successfully dominate the market, what the team has designed has been inherited to present-era iOS and Android. For example, non-intrusive visual notification system, card views, universal search bar, etc.

My then-teammates has influenced me so much, and it has affected my career and the way of thinking. Since then, I care **usability** and **user-experiences (UX)** for everything - not only software and hardware interface designs, but for coding styles, APIs, and documentations, because I believe UX is also applied to developers, when your *users* are developers.

According to [usabilty.gov](https://usability.org),

> User-Experience (UX) focuses on having a deep understanding of users, what they need, what they value, their abilities, and also their limitations.

and I think the statement is still true, when you swap out the word, *user* to *developer*:

> Developer-Experience (DX) focuses on having a deep understanding of developers, what they need, what they value, their abilities, and also their limitations.

Yes, I am suggesting Developer Experience *is* a type of User Experience!

### Bad Developer Experience and Frustrations

This is a good example of how not to design- At a gas station, you've got a gas pump looks like this, how do you react?

![Local Gas Pump by Jared Spool](/assets/images/articles/2016/08/gas-pump.jpg)

*(Photo credit: https://flic.kr/p/5ckBZq by Jared Spool. CC-BY-SA)*

Typically, when a user face such bad user experience, the reactions would be:

1. Get confused
2. Make a good guess and fail
3. Frustrated
4. Repeat 2 - 3
5. Totally pissed off

How about if you provide very enigmatic API, sans proper documentations or tutorial, and a developer is trying to figure out how to use the API- How does the developer react?

I think the reactions would be the same as above! The difference is that if you are at a gas station, you are more likely to try again or ask somebody to get your car filled up, while developers are more likely to google around (or ask Twitter followers) then ditch your service for use your competitor's over the bad developer experiences.


## Developer-Centric Products

So, what kinds of products have users who are developers? I tried to come up with a list of "products" that we need to care about developer experience-

- Platforms
- SDKs & tools
- APIs
- Developer website UI/UX, and contents
- Docs, tutorials, and “Get started” guides
- Samples on GitHub - code & README

While developer evangelists have works including developer trainings including workshops and conferences, and events like hackathons, here, I only try to define products, and excluding all the direct actions and interaction with developers.

### API Designing

API providers do also need to provide SDKs for common / high-demand languages, and sometimes for frameworks. You are losing developers when either SDK or API, as user-interface for developers, are missing.

Also, good API should be intuitive and easy to use, and bad API includes bad naming conventions, bad error messages, inconsistencies, etc. [In his talk, Joshua Bloch stated](https://www.youtube.com/watch?v=aAb7hSCtvGw) that:

- API can be among a company's greatest assets
- Can also be among company's greatest liabilities
- Public APIs are forever

He also tells us to *document religiously*- good API must have good design and documentation. I am not going to summarize all his talks here, so I recommend you should watch the [video]((https://www.youtube.com/watch?v=aAb7hSCtvGw)) by yourself.

### API Documentations

When we are talking about API docs, actually we need to provide more than just API references. Developers expect:

- Reference documentations
- Getting Started guide
- Tutorials

While API reference explains every call in the API and parameter, values, etc., other types of docs often provides step-by-step instructions, and copy-and-pasteable code samples, including *Hello World*.

A rule of thumb of writing these docs is keep everything simple in plain English. Complex docs don't impress your fellow engineers, but rather repel them. The basic tutorial should be short and simple too, but if you want to explore your creativity like I do, you should provide supplemental tutorials beyond your API docs- Blog, Demo, Showcase, etc.

### Creative Contents for Developers

My expertise is providing interesting use cases with code samples and demos. (You can browse my articles on this blog and many other sites!) What I knew and what I've learned from my own experiences are that developer experience is good when a doc has these:

#### Meaningful Diagrams

A picture is worth a thousand words - a simple diagram can explain complex idea far better. When I was writing about push notifications gateway for GCM and APNs, I decided to create a diagram to show how it works, rather than writing the whole explanations, and it turns out my readers (and coworkers) really did understand what the device registration meant, and how it works with push notification.

This is an actual screenshot of the blog I wrote for my previous employer, PubNub:

![screenshot of my blog](/assets/images/articles/2016/08/screenshot-gcm.png)

#### Screen Captures

A step-by-step instruction in a bullet list helps your developers for sure, but I found they love when the steps are described with actual screenshots. And devs love even more when they are in a single gif animation, which I think is a great example of the *TL;DR* principal!

This example below is what I created to show hoe to use Chrome DevTools Device Mode. I created for [my own blog](http://www.girliemac.com/blog/2014/07/28/devicemode/), and, later adopted by Google's Chrome team, and stayed on the official doc for a while.

![screenshot of devtools](/assets/images/articles/2014/07/devtools-device-mode-2.gif)

#### Video Tutorials

Especially, when you are targeting the first-timers, I found video tutorials are quite effective, because N00bs may have no idea where to get started. I don't blame on them because there is always a first time for everybody.

I created [this Johnny-Five video](https://www.youtube.com/watch?v=sC72DCxQrcU) because I was asked by enough numbers of people where to get started with hardware. The tutorial is tageting Node.js engineers who has no prior experiences with hardware engineering. I show electrical parts and explain what they are and how to wire. A cool thing is that the tutorial was introduced on [Arduino](https://arduino.cc) official blog, and got a lot of good feedbacks on social media.

#### More Improvement for Better DX

There are more things I try to keep in mind for good DX-

- Publish date should be included, especially because a dev year is like a dog year, where things get outdated pretty quick.
- No pushy marketing- obnoxious "Sign up now!!!" buttons and popups annoy devs away.
- Docs and tuts need to have good browsing experiences just like web pages. Always link to references and related pages.
- Don't PDF everything. Docs and tuts for developers are not white papers.
- Provide a place for feedbacks- my last company's marketing peeps refused to add a comment section on blog, or set up a forum, so in the results, I got comments and questions on random social media everywhere, and my email addresses (work, personal, and wrongly-guessed work email address that eventually forwarded to me.)
- Cut the BS- if your API is not ready or buggy, state so honestly.

## Developer-Friendliness

I stumbled upon this tweet about user-friendliness on the other day-

![screenshot of devtools](/assets/images/articles/2016/08/kaz-tweet.png)

It is interesting to see how the two companies describe the same errors in such different languages.

I was curious how these companies differ in Developer Experience, so I took a look at their API docs, and the results were not surprising. I am pretty sure the product peeps (who worked on the messages) at JIRA and Slack don't work for the API docs, however the the friendliness of these docs reflect exactly like-

These are documentations for their OAuth authentication-

[JIRA](https://developer.atlassian.com/jiradev/jira-apis/jira-rest-apis/jira-rest-api-tutorials/jira-rest-api-example-oauth-authentication):

![JIRA OAuth Doc](/assets/images/articles/2016/08/jira-doc.png)

[Slack](https://api.slack.com/docs/oauth):

![Slack OAuth Doc](/assets/images/articles/2016/08/slack-doc.png)

This is pretty clear that Slack docs is far more developer-friendly, not because of the cute robot, but the non-authoritative tone, and the way they introduce OAuth (what it is, and how it works) and the diagram, while JIRA doc doesn't even bother explaining what OAuth is, as if newbie developers are not welcomed.

I wonder if it is more "appropriate" for enterprise companies to be unfriednly to both user and developer...



## Knowing Your Developers

If you interact directly with developers on chat or forum, or work with community managers who do, you probably already have good idea about your developer community.

Another method I adopted from Human Interface team was defining **[persona](https://en.wikipedia.org/wiki/Persona_(user_experience))** during product development process. In my case, of course it is developer personas. I gather information from registrations, surveys, Stackoverflow, and support team (e.g. What language/SDK a developer use? What kinds of apps they develop?) Also, I get info from sales reps and business development team about actual customer (e.g. size of a client's company, industry, location, etc.)

I sometimes conduct brainstormings. This is quite effective to generate creative ideas and solutions, as well as team building. I combine the persona and brainstorming to figure our what our developers want.

![brainstorming](/assets/images/articles/2016/08/dx-brainstorm.jpg)

This photo was taken right after the first brainstorming session was done at my previous work. After the session, we sorted the ideas in category and feasibility.

Sure, this does not look like your typical Developer Relations meeting, but I have successfully delivered a lot of good use-cases and tutorials and articles around them. After social media has picked up, the awareness of the virtually unknown company and the products went up.

## Diversity and Inclusiveness

The majority of developers may be male and understand English, but if you are targeting only the majority, you are still missing out large numbers developers out there.

Inclusivity typically means not to exclude any groups of gender (expression), race, ethnicity, disability, sexual orientation, etc. I am not going to talk too much about the importance of diversity in a workplace in this article, however, I strongly believe when you work at a diverse team, you can definitely reach out more developers, especially because people in general tend to trust somebody who they feel related to. In fact, many of my "fans" are minorities- women, immigrants, speaking English as a second language, etc. (It is very flattering when people tell/tweet/email me they are fan of my works!)

Especially when somebody in your team speak/write something other than English, it would be a huge advantage. I do speak and write Japanese fluently, and in numerous occasions, I have helped sales and other teams when the companies have Japanese clients. I have written blog posts, and spoken at conferences in Tokyo as well. My conference videos and slides on [Slideshare](https://slideshare.net) have reached out far larger audiences. I can clearly tell you that it's not easy for you to get into Asian markets without somebody who knows the languages and cultures well!

Even if your team has no other multi-lingual people or simple has no time to translate, when your organization has successfully support international developers, the community helps you.

For example, [Dev.Opera](https://dev.opera.com) publishes their tech blog under Creative Commons, and open-sourced the contents on [GitHub](https://github.com/operasoftware/devopera), where their community can contribute. I have written [an article in English](https://dev.opera.com/articles/web-notifications-pubnub/) for Dev.Opera, and the community member has translated it [in Russian](https://dev.opera.com/articles/ru/web-notifications-pubnub/)! How awesome is it!

![translated in Russian](/assets/images/articles/2016/08/devopera-russian.png)

It is not easy to acquire fans worldwide, but having a diverse team makes it far easier.

## Conclusion

Developer Experiences *really* matters!

Here's the slide deck from [DevRel Summit](http://www.devrelsummit.com/) :

<iframe src="//www.slideshare.net/slideshow/embed_code/key/CdP2J9ci1BP5Gq" width="595" height="485" frameborder="0" marginwidth="0" marginheight="0" scrolling="no" style="border:1px solid #CCC; border-width:1px; margin-bottom:5px; max-width: 100%;" allowfullscreen> </iframe>

## Epilogue

Despite my tireless efforts and successful outcomes, my principles of developer evangelism did not align with my former employer's marketing department that controls the team. When somebody doesn't care about developers, you have no job there. Well, it has been fun leading the team for a while!

I am joining a company who truly embraces developer experience, so you will hear from me about my new gig pretty soon!
