---
layout: post
title: '#NoOps, #DevOps and the evolution from developer to multi skilled engineer'
image: /assets/img/noops-devops/devops.png
readtime: 18 minutes
tags: noops, devops, iaas, terraform, aws, engineer, 
---

*TLDR - Devops is awesome, and it looks like it will eventually replace a whole host of other business functions. DevOps is not scary, and using the right tools and patterns will allow you to easily transition*

First its worth having a look at the definiton of what devops is, bear in mind Devops is a term that still does not have a solid definitions, and a lot od people get confused as to what it is. Here is my understanding:

Devops combines creates the ability for companies to deliver applications with high velocity, by using tools, practices and cultural philosophies to improve and evolve faster than tradition software practices that rely on other siloed teams. Engineers work across the full application lifecycle, including (but not limited to) development, testing, deployment and infrastructure, even sometimes quality assurance and infosec. As much as possible is automated, which prevents leaving an individual holding all the knowledge, and also helps prevents bottlenecks.


<amp-img src="/assets/img/noops-devops/devopscycle.png"
  width="1000"
  height="567"
  layout="responsive">
</amp-img>


## The No Ops Movement

No ops focuses more on the fact that traditionally operations teams that manage and deploy to underlying infrastructure will eventually become obsolete, as the jobs that they would have performed traditionally have evolved, and when moved to the cloud, can and should be performed by multi skilled engineers, focused on the full application lifecycle.

## Is DevOps adoption growing?





# How to make the journey to NoOps easier?

## Normalising the tech stack

To reduce complexity, it is a good idea to normalise the technology stack. This will reduce the scope that engineers will need to know, although this shouldn't be normalised to the point where it limits tech choices.

### Reusable deployment patterns

For developers who traditionaly have never worked on deployments, or delivering software, DevOps can be daunting. Its important to create reusable deployment patterns, so the steep learning curve isnt so steep. 

At ditto music, one of the first patterns we worked on, was to create a reusable deployment pattern. We wanted to automate the provisioning of the instance, and have a platform where the code can just be deployed. There are many options for this, at the time we built the pattern we evaluated and decided on AWS Elastic Container Service.

Our deployment pattern took a built artifact, such as a dotnet dll, or node project, and built a docker image, pushed to our own Elastic Container Repository and used a templated service and task to be able to run the 'WebApp' in a predicatable and similar way across technology stacks. We use it for long running services, rest services, graphql, websites etc.

Because of the way ECS works, it was very simple to build secure permissions and apply this across the whole infra. Anything that needs more than just the basics, could apply it manually. Terraform modules really helped with this.

### Always improving the tech stack

Just because you have a great stack, doesn't mean you should continue to use it until the end of time! 

There are so many great things coming out all the time, for example at ditto music we use ECS, but that is because at the time fargate was not available in London. Now it is, we are evaluating moving our ECS web apps over to Fargate, as this serverless option will have many benefits with reducing complexity of deployments, cheaper to run and more scalable.

### Reusable testing patterns


# Maintainability and openness

- Logging
- Metrics gathering
- Success metrics for projects are visible
- Configuration managed by a tool
- Sharing knowledge, and source code

# Reliability 

- Test infrastructure changes before deploying to production
- CI/CD
- Automate infrastructure delivery
- Automated provisioning
- Automate security policy configuration
- Security teams are involved in technology design and deployment





2. DevOps adoption is growing
According to RightScale’s 2016 State of the Cloud Survey, more than 80 percent of enterprise companies and 70 percent of small businesses are in the process of adopting DevOps practices. Companies are investing in DevOps more heavily than ever before, and as Puppet’s 2016 State of DevOps Report demonstrates, the investment is paying off. High-performing IT organizations practicing DevOps have 2,555 times faster lead times (the time it takes to go from idea to working software in production), three times lower change failure rates, 24 times faster mean time to recovery (MTTR), and 10 percent less rework than their underperforming counterparts. Needless to say, your DevOps job is likely safe for the foreseeable future.

3. NoOps is not one-size-fits-all
If businesses see those kinds of gains from DevOps, why not skip DevOps and go directly to NoOps? For starters, NoOps is limited to applications that fit into existing PaaS solutions. Many enterprises still have monolithic legacy applications that would require massive upgrades or total rewrites to work in a PaaS environment. Furthermore, new technologies that have no suitable NoOps solution will emerge. As some claim, NoOps is really the next level of DevOps, and we should use DevOps principles and techniques to build NoOps nirvana into all new products.

4. NoOps fits within the three ways of DevOps
In The DevOps Handbooks, authors Gene Kim, et al. describe the three ways, which are the principles all DevOps patterns can be derived from. The first way is Flow: the movement of features from left to right through the CI pipeline. NoOps solutions remove friction and increase the flow of valuable features through the pipeline. In other words, NoOps is successful DevOps.

Thesecond way is fast feedback from right to left as features progress through the pipeline. Because NoOps allows us to ship defects as quickly as features, automated controls are necessary at every stage of the pipeline to ensure defects are caught and remediated early. At the scale of modern software applications, even a small defect could have damaging results for a business.

The third way is continuous learning and improvement. NoOps is exemplary for focused learning and improvement over many years to achieve an ideal of frictionless software deployment. NoOps is a culmination of new tools, techniques, and ideas developed through open and continuous collaboration. To say NoOps is the end of DevOps is to say we have nothing left to learn and nothing to improve.

5. Operations happens before production
With DevOps, much of the traditional IT operations work happens before code reaches production. Every release includes monitoring, logging, and A/B testing. CI/CD pipelines automatically run unit tests, security scanners, and policy checks on every commit. Deployments are automatic. Controls, tasks, and non-functional requirements are now implemented before release instead of during the frenzy and aftermath of a critical outage. Having sysadmins, auditors, security personnel, QA testers, and even key business stakeholders involved from the beginning ensures these automated tasks and controls are in-place, correct, and effective before it’s too late.

6. DevOps is people
More important than any particular tool or technique is the culture of DevOps. You can’t practice DevOps in a vacuum and expect to succeed. DevOps began when developers and system administrators met at a conference to share ideas and experiences and work toward a common goal. Over time, the community realized it could build better software faster by including members from all areas of business, including QA, security, marketing, and finance. And the community continues to learn and evolve by sharing ideas at meetups, in online forums, on blogs, and through open source software. No matter how many advancements we make, the law of entropy will take over and erode them all if we forget the importance of DevOps culture.

7. DevOps requires continuous learning and improvement
A major pillar of DevOps is the spirit of continuous learning and improvement. When failures happen, a strong safety culture that practices blameless post mortems is vital for learning from mistakes. Rather than punish and assign blame, which destroys team morale and doesn’t solve the underlying issue, we must understand and improve the systems and processes that allowed the failure to happen in the first place.

Learning and improvement shouldn’t happen only when things go wrong. Everyone should strive to improve their daily work, and organizations should provide incentives for individuals to share their discoveries with the wider organization. With modern IT being a key driver of business success, companies must recognize that turning 10 1x developers into 10 2x developers is twice as effective, and much more realistic, than finding the elusive 10x engineer.



In conclusion, DevOps is forever
Despite the cries of DevOps demise, NoOps is not the end of DevOps. In fact, NoOps is only the beginning of the innovations we can achieve together with DevOps. The movement started long before DevOps had a name, and the core principles will live on as long as businesses require software to succeed in a fast-paced, rapidly changing technological landscape. In a few years, the name may fade away in favor of a new buzzword, but the culture and the contributions of the DevOps community will live on.
