---
layout: post
title:  "Podcast: The Secret Diary of a Network Administrator - Episode 3"
date:   2018-03-05 22:00:00 +0000
categories: Podcast
tags: [podcast, configmgr, powershell, dfs]
---
Episode 3 of my podcast: ‘The Secret Diary of a Network Administrator‘ is now available!

In this episode I have the final word on DFS replication!  Sheesh – what a manic couple of weeks I’ve had.

Here is an accompaniment to the podcast: (I would listen to the podcast first and then return here to read this.)

I should clarify that DFS-r just wasn’t suitable for our large geographically dispersed environment with unstable WAN links.  At least, not without more administration.  In hindsight, if I were to implement this again, I would write a Powershell script that emailed out when the transaction queues grew too large.  I also noticed that although I had sized the staging areas correctly when it was first implemented; 12 months later the sizing was way out.  So lack of administration, coupled with a long outage of two DFS servers and unreliable WAN links meant this was probably doomed from the start.

On the plus side, we have learned from our failures and not only identified where our back-up and disaster recovery plans need revision for some of our offices, but also where our single point failures are and we will now be taking steps to remedy this so that if something similar happens again, we will at least be prepared.

The book I spoke about, “[Black Box Thinking: Why Most People Never Learn from Their Mistakes--But Some Do](https://www.amazon.com/gp/product/1591848229/ref=as_li_tl?ie=UTF8&camp=1789&creative=9325&creativeASIN=1591848229&linkCode=as2&tag=feathemon-20&linkId=f627bbf505cd274caa27742125d131f5), is by Matthew Syed and by pure coincidence is about learning from failure (so very apt) and I will give you my thoughts on it once I've finished reading it.


As usual, you can follow me on Twitter: [@OzThe2](https://twitter.com/ozthe2) and check out anything on My GitHub account: [https://github.com/OzThe2](https://github.com/OzThe2)

Available from all of your usual Podcast sources or play it right here...

The podcast is available from all good podcast apps, iTunes, Soundcloud, Stitcher, Blubrry etc or alternatively, listen to it right here:

<iframe width="100%" height="166" scrolling="no" frameborder="no" allow="autoplay" src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/394524876&color=%236e6e6e&auto_play=false&hide_related=false&show_comments=true&show_user=true&show_reposts=false&show_teaser=true"></iframe>