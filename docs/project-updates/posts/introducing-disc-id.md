---
draft: false
date: 2023-11-30
authors: [hyattzer]
categories:
  - General
description: Learn more about the purpose, goals and other details of the Disc ID Project 🥏
---

# Introducing the Disc ID Project

Thank you for coming to see what is happening with Disc ID! This project is just getting started and I am excited to finally have some of these details out in the open after thinking about them for so long. In this update I will walk through various details and concepts around the project to help orient you a bit.

## Just give me the TL;DR
The Disc ID Project's main focus is developing standards for recording data about disc golf discs on NFC tags, which are small electronic chips that can be put on or embedded in the plastic of the disc itself. If you are looking for some quick basics on the project and links to further resources, head over to the [Home page](../../index.md) and you'll be up to speed.

For those of you wanting a bit more context around this whole thing, follow me further into the rabbit hole...

<!-- more -->

## Why make this?
If you search for details about RFID or NFC tag technology in relation to discs, you will find lots of questions and ideas around using it as a means of finding lost discs on the course. That is not the purpose of this project, nor is that a reasonable use of this technology (see [FAQs](../../index.md#faqs)).

Instead, the tags will be used to hold data about the discs themselves. Think about the manufacturer, model name, etc. Most of the time these things are known or can be reasonably determined or measured (like weight), but sometimes they cannot.

See [this search on the r/discgolf subreddit for `id`](https://www.reddit.com/r/discgolf/search/?q=id&sort=new) and you will find many people posting pictures of discs asking for help identifying them (and interestingly quite a few actually have the term "Disc ID" in the title of their post).

Beyond helping solve that simple case, it also allows more exact data about a disc to be included. Ever find that fairway driver with the perfect out-of-the-box flight you were looking for, only to struggle sourcing another one just like it after you inevitably shank it into a lake?

The details on the disc can help you more easily find it by looking at more than just a model name and weight. For instance, a unique "run" identifier and manufacture date can be added so you have better odds of finding plastic created at the same time with the highest chance of feeling and flying the same.

And exact data means the potential for having a unique identifier for each disc exists. Although this project is not currently focused on exploring this, there are interesting use cases for having that in place which may be discussed in the future.

## I'm convinced, now what
If you've read this far I assume you are convinced this should be explored, or at least are not against it. If so, there are a couple different paths to take to help the project out:

1. Learn more about the project by reading through some of the details on this site including the [Home page](../../index.md) and sharing the project with others you think might be interested too

2. If you have technical skills that could help with the specifications or software implementations, check out the [ Discussions threads](https://discussions.discid.org) and introduce yourself

3. If you like to play around with technology, see if there is a [Guide](../../guides-reference.md) you can follow to test out NFC tags (or help write a guide for others!)

4. For those who have contacts in the disc golf industry, especially with manufacturers, introducing them to the project or connecting them with [me](../../about.md#project-maintainer) would be very helpful

## What are the plans going forward?
Now that I've got a draft of some details for the [Disc ID Specification](../../specifications/disc-id.md) published I plan on working through some of the open questions (hopefully with some of y'all) that will be managed in the [Discussions threads](https://github.com/orgs/Disc-ID/discussions), eventually getting movement on an implementation via iOS to make this a reality.

I will be posting updates here at least monthly, so keep an eye out here or grab the [RSS feed](/feed_rss_created.xml). As part of these updates, I will also be higlighting important discussions going on:

!!! discussion "Highlighted Discussion"
    The key discussion now is around [how to encode the disc data within the payload of a NDEF Record](https://github.com/orgs/Disc-ID/discussions/2) so it can be as memory efficient as possible. This will probably branch into discussions around the fields to actually include in the data, since the specific fields and their design will impact that efficiency. 

Come join that discussion or just [introduce yourself](https://github.com/orgs/Disc-ID/discussions/1) over there!

---

Thank you for your time and I am looking forward to working alongside everyone to make this happen for the whole disc golf industry! 🥏