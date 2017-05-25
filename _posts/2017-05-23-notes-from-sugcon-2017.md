---
layout: post
title: Notes from SUGCON 2017
date: 2017-05-23
categories: sitecore sugcon
---
I've been intending to start blogging my adventures in Sitecore for far too long now. Attending this year’s SUGCON Europe event in Amsterdam has finally given me the motivation needed to get something up and running.

I attended the two-day conference with a couple of developer friends & colleagues from Mando. With there being a number of "switch" sessions of talks running in parallel we adopted a divide and conquer approach so that we cound attend as many individual talks as we could and share our finding. 

There were quite a few talks that I would have loved to have attended but didn't make it t (sorry Roslyn). Here are some of my thoughts and observations from the some of the more interesting ones. 

## Omni-Channel Showcase 

Bas Litjen & Rob Habraken presented a project they'd been working on for the last five months - an awesome experiment involving Microsoft Cognitive Services, Sitecore's xDb and a Raspberry Pi-powered robot named Robbie. 

It was great seeing Robbie identify the speaker as an xDb contact and then engage in a personalized chat. At one point he identified both speakers simultaneously, effectively running two xDb sessions at once. Bas & Rob had created pattern cards in Sitecore to enable Robbie to ask different questions based on their facial expressions. 

It was a shame that the live-demo gremlins struck in the form of unreliable conference Wi-Fi, making it difficult for Ben & Rob to show us the end to end experience but it was still a fascinating demo and a great illustration of how Sitecore can engage with customers outside of conventional website channels.

Robbie is an ongoing project and one I'll definitely be following.

## Publishing Service 2.0

The core Sitecore publishing service is long-overdue an update as it is quite primitive compared to other enterprise CMS systems. Aside from being generally slow and un-optimized, the lack of feedback given to CMS users during publishing is also an issue. I'm sure at some point we've all become frustrated and restarted a publishing operation thinking it has become "stuck", which only results in flooding the publish queue with even more requests and grinding things to a halt.

The new publishing service is a separate module developed by Sitecore, built on .NET Core and they've now just released version 2.0, available as a free module. 

The publishing service replaces the standard publish options with a more editor-friendly interface and also includes a publishing queue dialog so users can find out exactly what publishing operations are in progress. It also hides the concept of smart and incremental publishing (are editors really expected to understand what those concepts mean?) and replaces them with a simple publish operation. The "republish all content" option is restricted to admin's only. 

The publishing UI changes alone would make this a big improvement but the team have also taken steps to improve every aspect of the publishing services performance. Stephen presented some benchmark results using SQL Azure which were pretty impressive:

| Region           | Azure network latency | Total latency using old publishing | Total latency using new publishing |
| ---------------- | --------------------- | ---------------------------------- | ---------------------------------- |
| South UK         | 18ms                  | 00:19:00                           | 00:00:02                           |
| Japan East       | 250ms                 | 4:26:59                            | 00:00:27                           |
| North Central US | 114ms                 | 2:01:45                            | 00:00:07                           |
| West US          | 162ms                 | 2:53:00                            | 00:00:17                           |

The publishing service will one day be part of the core Sitecore product and until then is available as a free module. As the service is so lightweight (part of Sitecore's move away from a monolithic platform towards micro-services) most of the early adopters are running it on either the CM or database server.

The announcement that the module is free elicited the biggest cheer of the day, so if you are running a dedicated publishing sever take a look at this and save yourself a license!

## Things I wish I'd Documented in Glass

Mike Edwards of Glass Mapper fame talked about the common anti-patterns he often sees in Glass implementations, and also talked about some of the lesser known features:

* The performance implications of using a Glass base class particularly when not using type inference and template enforcement.
* Mapping data models vs view models. I must admit I'm often guilty of simply building up Glass models that follow the template structure in Sitecore, whereas it can sometimes be a more performant approach to build and map rendering-specific view models instead. This approach will probably be a more natural fit for Helix-based implementations too.
* Fluent mappings. I've always used attribute-based mappings - not sure why as I normally gravitate towards fluent mapping in for example, nHibernate. I think I tried using the fluent mapping API back in Glass v3 and didn't get on with it. The changes to the API have persuaded me to re-evaluate it although Mike did admit at the end that he still uses attribute-mappings himself...

It was a great talk. I went along unconvinced it would be of much benefit as I've been using Glass for a few years now but I came away feeling like I'd learned something.

## Tooling for Helix – With Docker Focus

I was really looking forward to this talk by Thomas Stern and Emil Klein as anyone whose attempted it will testify, following the Habitat solution structure and principles is quite time-consuming without tooling support. 

The first part of the talk focused on using Yeoman to scaffold Helix projects - from setting up the initial solution to then adding feature, foundation, and project modules. The support for adding Unicorn serialization rules was a nice feature too. 

As the project / folder structure recommended by the Helix / Habitat guidelines is difficult to replicate manually without fighting against Visual Studio, some additional tooling is needed and this looks to be the best approach I've seen. It's easy to assume Yeoman is a front-end tool but the ability to scaffold .NET projects shows how platform-agnostic it is.

The second half of the talk focused on using Docker containers to host the various moving parts that make up a Sitecore installation. At times is feels that every new Sitecore release takes on a new dependency so using Docker to spin up an entire Sitecore environment will be a huge huge productivity booster, as well as making it much easier to install Sitecore into other on-demand environments (e.g. sales laptops).

Unfortunately the live-demo didn't quite go to plan, but Thomas has since [recorded a video](https://www.youtube.com/watch?v=fGmiwvri8Rs) to show how quick it can be.

## Sitecore MVC Developers journey

Christian James Hansen gave an overview of his Sitecore MVC library - Propeller MVC, which is a light-weight ORM and set of HTML helpers.

I hadn't heard of Propeller before so will keep an eye on it. It will be interesting to see whether it can find a place alongside the other Sitecore libraries occupying the same space, especially the ubiquitous Glass Mapper. 

The source code is available on [GitHub](https://github.com/galtrold/propeller.mvc)

## Sitecore Experience Accelerator

To be honest I didn't actually attend any of the individual SXA talks, as we recently had a demo of it at Mando and it didn't overly excite me. It kept cropping up in various other talks though and it's obvious that it is something Sitecore are pushing and that we will hear more about.

The idea of SXA is sound - reduce time to market by providing a set of off the shelf components and modules. The UX wire-framing tool and facility for front-end developers to be able to export CSS and HTML (in both live and edit mode) is intended to provide an end-to-end design and development process.

It also has some very useful extensions to Sitecore, such as relative data-sourcing. However I would argue that any customization needed to follow Helix principles should have an implementation in the core product - such as dynamic placeholders, and the aforementioned relative data-sourcing.

I'll certainly be keeping an eye on it, as start-up time on new Sitecore builds _can_ be a problem however I'm still trying to understand how it will fit within our agency and UX / front-end development processes. 

[Official SUGCON site](http://www.sugcon.eu/)
