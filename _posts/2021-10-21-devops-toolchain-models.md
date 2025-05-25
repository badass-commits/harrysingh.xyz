---
layout: post
title: "DevOps Toolchain Models: Centralised vs. Decentralised"
date: 2021-10-21 12:56:42 -0600
---

To centralise or decentralise, that's the question. When enterprises adopt DevOps, one of the most important considerations is how internal teams consume a toolchain supporting the DevOps mindset.

In this article, I want to focus on the big question around how DevOps should (or could) be delivered within an enterprise. Should companies enable complete freedom and decentralisation of their toolchain and process? This lets teams put their own flavour on the core principles of DevOps. Or, do companies go for a more centralised route? This means more standardisation & consistency across the enterprise and an easier adoption avenue due to central capabilities. Let's discuss the pros and cons of each and come up with a recommendation.

## What does centralisation mean?

Centralisation of DevOps tooling means offering a single toolchain and process for teams to follow across an enterprise. When you centralise, you provide multiple teams with a single avenue to adopt a DevOps mindset. There are many advantages to centralisation, some examples being:
- **Adoption:** Whenever you centralise, you usually have a higher adoption percentage off the bat. This is mainly due to teams who are new to DevOps, more specifically, the tools that come as part of the DevOps toolchain, have a place to start and consume something as a Service. If you rely on teams standing up their own tooling, the time to adoption is generally longer as there is more setup time.
- **Consistency:** If you centralise a process, an expected outcome of that is consistency. This means that if a developer is working on team X, and then moves to team Y; there is less "getting up to speed" time, as the processes would be the same for Team X and Team Y. This is a massive win if your company promotes rotation of developers and engineers across teams.
- **Time to Value:** Application teams new to DevOps will find it quicker and easier to deploy something to production if you centralise. Teams spread across an enterprise can always ask questions to the central team owning DevOps, so someone is around to help out and ask questions. There is short term success here and a quicker time to value.

As you can tell, there is a theme to the above. The newer your enterprise is to DevOps, the more value you will see from centralisation. However, there are some disadvantages or considerations to keep in mind.

- **Slow turnaround of Change:** If only one team are allowed to own and maintain tools, and a customer puts in a feature request, that request may be one request often already in the backlog. As that customer who logged that bug, you may have to wait a month, even longer to see that feature request in production. Whereas if you had control of the tools in your application DevOps toolchain, you make the decisions, so the power is in your hands.
- **Reliance & Excuses:** If you centralise, it is easy for application teams to rely heavily on the team's who own the central tools. Especially if there is something the application team is waiting on. There is an excuse to why they are behind or not moving at the pace they should be, "I can't do this, just waiting for the central team to deliver something". Too much reliance on one team means you don't move at the pace that you may want to move at.

There are lots of advantages to centralisation, especially for larger & legacy enterprises. Now let us discuss what decentralisation means.

## What does decentralisation mean?
Decentralisation of DevOps tooling is the opposite of centralisation. It's where there is not central tooling, there is no central process, and you allow your enterprise to embrace the principles of DevOps themselves. There is a trust that they will see the value in DevOps, and have the creative and learning agile mindset to read, up-skill and apply. Some advantages of decentralisation are:

- **Embracing Diverse DevOps Models:** There isn't one way to adopt DevOps, and there most certainly isn't one way to use a DevOps Toolchain. If you centralise too much, you will find people "doing the same thing" and not getting the most out of the tools that they are using.
- **Learning Agility:** The value of decentralisation is that you are equipping your enterprise for learning success. Change has been, and always will be happening, especially within IT. If you fully decentralise, you are asking and almost enforcing your enterprise to upskill themselves. What this leads to is a longer-term success. If employees are used to changing and are used to learning new tools & processes, anything new that comes up in the future should require less time to adopt as employees are used to a changing environment.
- **Innovation:** This is a pivotal point to understand. You want your employees to be innovative and apply learnings to their working model. For some reason, there is a preconception that the centralised team knows best and what they say should go. This is not always the case. Just because the central team think they know what's right for the enterprise, doesn't mean they do. If you decentralise your DevOps process and toolchain, you are letting your employees innovate and think differently without the central team's restrictions. A different way of thinking about this is - would you rather a central team of 40 people making decisions, or would you like 1000 people (or everyone in your company) learning and deciding what's best. One thousand minds are better than 40.

However, for all these advantages, there are possible disadvantages to think about:

- **Can be slow to get enterprise-wide adoption:** Normally, leadership within an enterprise want quick results and want to see success straight away. If you have a highly skilled and learning agile company, this may not be so much of a problem. But companies who have been around a while may struggle with getting results quickly.
- **You may not see shared learnings:** There is a reality to decentralisation: some teams will get it quicker than others. As there is no central team, there may not be an easy way to share learnings across teams. This will lead to some teams racing ahead of others, with the high likelihood some teams will never get it and will be left behind. At the end of the day you are one company, so the success shouldn't be perceived as team success, it should be company success.

Similar to the centralisation section, there is a theme appearing. A newer company or a company with a highly agile culture is likely going to suit decentralisation more. I believe following this model will set yourself up for success longer-term; when done right.

## So, what one should we pick?

The reality of this question is that there is no right answer. But there is a recommendation:
**Centralise the DevOps Toolchain's foundations, whilst decentralising the journey on "how" teams adopt & consume the centralised tools, patterns, and processes.**

So, what does this mean? Let's break down that sentence into two:

 **"Centralise the DevOps Toolchain's foundations".**

It isn't time effective, or cost-effective to have multiple of the same tools, or similar tools spread across an enterprise. An example being source code management. Stand up a single source code management tool and offer it out to the enterprise as a Service. This will reduce operational overhead because instead of multiple teams managing that tool; it will be supported and maintained centrally. Additionally, it's typically cheaper contractually if multiple licences are purchased centrally vs distributed across numerous contracts. For centralisation to be a success, automation and end-user autonomy needs to be a core principle. Staying with the source code management example mentioned above, you should allow customers to create repositories themselves without putting a request in and waiting. Allow teams to create teams themselves, as well as administer their own repository. Ensure there is no friction in the way of the customer of the tool. The more "red tape" and "friction" in the way of the customer and the centralised tool, the less chance of success. If you're thinking, "I can't give administration access and full autonomy in my company, we have quality process and regulations we need to meet." Just because you give autonomy and allow self-service, doesn't mean you can't wrap process and rigour around the tool, ensuring quality and security compliance. Use API's to build the needed quality processes to ensure the centralised tool is "in compliance" of any in-company procedures. Then publish documentation of any processes, so customers know what to expect. Mimic this for every tool within your toolchain.

Additionally, understand that you will have different teams at different skill levels, so centralising foundational blueprints and patterns for teams to get started with makes sense. For example, within GitHub, create [repository templates](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/creating-a-template-repository) which follow best practice (locked branches, pull requests enforced, turned on security tools). This means teams new to GitHub have a place to start "out of the box" with everything needed pre-created. The same goes for your CI/CD tool. Build reusable workflows/pipelines with standard testing & deployment patterns across your enterprise. For example, you may be a predominately JavaScript shop, so building a single pipeline that does JavaScript testing/linting/security means teams new to CI/CD have a place to start (additionally teams with CI/CD experience may not want to build their own so will reuse what is on offer centrally). Thirdly, and finally, is the hosting platform chosen (AWS, Azure, GCP). Build central patterns for common software application architectures. e.g. if many of your software products built are web assets, creating a SPA template that comes with the needed infrastructure as code to deploy to AWS S3 & Cloud-front. This means teams have a place to start, especially people new to cloud-native. The same for API's would apply, an OpenAPI template that comes with AWS API Gateway & Lambda would be a great starter kit.

Okay, so now you may be thinking wow this is a lot of centralisation, let's shift to the second part of the above phrase which is:

**"Whilst decentralising the journey on "how" teams adopt & consume the centralised tools, patterns, and processes."**

You are not the police. You cannot dictate and enforce how teams use your tools. If you lock everything down to a single way of doing things, you will slow down teams. This will fail. Your company may have adopted a "DevOps Toolchain", but your teams won't be moving fast and won't be adopting the principles of DevOps. Past standing up the tools and foundational patterns/starter kits, let teams decide how they want to use the tools you have stood up.

An example being your hosting platform. Stand up an underlying hosting service that meets the needed quality & security processes for the enterprise, but then get out the application teams way. Do not centralise manual gates and reviews to one team as that team "they know best".

Doing this will massively slow down not just deployment time, but learning time. Give autonomy for teams to deploy from Dev -> Q.A. -> Prod. If teams fail, that's okay, let them learn from that failure and apply that learning for next time.

The same goes for CI/CD. In the above paragraph, I explained building example pipelines/workflows. Do not dictate this is the only way for teams to use CI/CD. Allow teams to see these as examples, and then customise to suit their needs. Teams may not even use these pre-built pipelines/workflows, and that's okay. They are there for reference and use if desired.

The main point to be conveyed here is that there is no one way of doing things. Do not centralise the process, just the foundations and tools. Doing this will set teams up for success by themselves. Additionally, the more centralisation you do and the more is done for teams, the less they will learn themselves. This puts enterprises at a further disadvantage because if centralised tools change, or there is an update in a procedure that requires a change on the application team, teams will be foreign to doing things themselves, leading to slower change adoption.

## Conclusion
There is a misconception that DevOps should be a specific role, and only people who's job title includes "DevOps" needs to focus on DevOps. In my opinion, this isn't, and shouldn't be the case. DevOps is a mindset (process) which teams need to adopt when building and deploying software products. Everyone part of that software team somewhat contributes to the DevOps process. As mentioned above, there is no right answer when it comes to centralisation or decentralisation, it depends on the company and most importantly, the people. In most enterprises, a mixture, or somewhere in-between centralisation/decentralisation, will give the best experience for different teams. To conclude, centralisation will get you quicker success but can be short term thinking. Decentralisation will take longer to get there but in the long term can see more significant benefits.

The key takeaway though is centralisation works, but only when done at the correct level, and autonomy is vital.