---
title: Disc ID Project
description: Central knowledge base for the Disc ID Project
---


# Disc ID

Welcome to the central knowledge base for the Disc ID Project. If you aren't familiar with the project, the details on this page should help orient you with some of the related goals, structures and activities. If you are familiar and are just looking for the latest updates, see [Project Updates](project-updates/index.md) and/or connect in the [GitHub Discussions](https://discussions.discid.org).

Otherwise, feel free to explore other resources in the top navigation - thanks for your interest!

---

## The Goal
The Disc ID Project has a primary goal of developing standards for recording data about a disc golf disc onto a Near Field Communication (NFC) tag on the disc. We are unaware of any existing standards and are working to align efforts around a single, open source standard. Hopefully this will avoid the confusion and ineffeciency that comes with too many standards, so succinctly explained by [this XKCD comic](https://xkcd.com/927/){ target=_blank }.

Although there are many interesting use cases for these tags being attached to the outside of a disc, the specification will take into consideration potential limitations and costs related to embedding the tags directly into the disc in the future by manufacturers.

Of course having a data standard isn't very helpful unless there are also tools that help use that standard. With that in mind, the project will also be developing software for reading and writing the tags within the data standard, primarily on iOS and Android due to the built-in NFC tag readers the devices running those platforms typically have.

## Key Resources

### [Project Updates](project-updates/index.md)
An area for more structured updates about the project, helping to gather key details from other collaboration areas (GitHub, etc.). There is a [RSS feed](feed_rss_created.xml) of this available as well.

### [Specification](specifications/disc-id.md)
Where the standards for the tag data will be documented including field formats, acceptable values, encoding requirements, etc. By providing a precise definition for the data, any parties interested in developing tools to read, write and manage the data will produce something interoperable with rest of the industry.

### [Implementations](implementations.md)
Information about software implementations which conform to the Disc ID standard will be managed here. This includes any SDKs developed by the Disc ID Project, along with any other community developed approaches.

### [Guides & Reference](guides-reference.md)
A home for practical guides on how to utilize the data standard and/or just experiment yourself with NFC tag reading and writing. There are also links to various reference material helpful to the project in general.

---

## Getting Involved
Projects like this thrive through the involvement of many parties. To give it the best chance of gaining support from the broader disc golf community, as well as those inside the many companies and organizations driving the disc golf industry forward, it will be operated openly. The resources it produces will primarily be published under the [MIT License](https://choosealicense.com/licenses/mit/) to be permissive in commercial use.

To help improve collaboration, [GitHub Discussions](https://discussions.discid.org) will be used to host threads about various topics in the project.

!!! discussion "Come introduce yourself!"
	Join the discussions by posting a short note about who you are and why you are interested in the project in the [Introductions thread](https://github.com/orgs/Disc-ID/discussions/1).

Other GitHub services are likely to be used to help track the efforts, including Issues and Projects.

## Who is doing this?
This site was setup by Zach Hyatt, PDGA #27534, just a fellow disc golfer trying to help the sport. You can reach him at zach📧discid.org.

## FAQs

??? question "Can these tags be used to find lost discs on the course?"
	No, the specifications call for the use of Near Field Communications (NFC) tags and are only readable from a couple inches away.

??? question "Are discs with NFC tag stickers attached legal for play in PDGA sanctioned tournaments?"
	No, the PDGA does not allow the addition of any material to a disc which has a "detectable thickness such as paint" (see [rule 813.01.C.4 Illegal Disc](https://www.pdga.com/rules/official-rules-disc-golf/81301){ target=_blank }) and given NFC tags have a detectable thickness, they would fall under this rule making the disc illegal for play.