---
layout: category-post
title:  "Building Nia"
date:   2026-06-20
categories: writing
---
# Building Nia - Discovering the powers of RP2354

## Hey there Wanderer
This blog was supposed to be a year earlier but here we are. I just finsihed the development of the first prototype (not really the first lol) for the Nia pendant. I demo'ed it at the Open Source Summit India this week in Mumbai. Honestly building a badge from scratch and interacting with people interested in it was something special. We need more of these badge hacking and building enthusiasts in these conferences (especially in India).

Keeping the rant aside lets get into the hacking 🤘.

## The inspiration
An year ago I saw this video by mitxela showcasing his fluid sim pendant. It caught my attetion and I wanted to make something like that of my own. I started with the physics first. Getting a hold of whats moving and whats not in a simulation was really important.

<img src="/blog/assets/nia.jpg" width="250" align="centre">


I then researched I hardware I wante to work with. STM is great but I have a soft edge for Raspberry. This edge led me to choosing RP2354A for this project. We'll discover later why. This uses Bma400 accelerometer, TPS3839A09DQNR, TPS7A0215PDQNR and MCP73832-2-MC for charging the rechargable cell.

Now that we have the basic hardware used listed, lets checkout some physics resources that helped me in my research. 10 Minutes Physics was a great help. His videos on Euler fluid simulation and FLIP simulations are self explanatory and quite sufficient. While these were enough I took some time to also look at the Flui Simulation by Robert Bridson.

I suggest going through his tutorials and the JavaScript code he has written once while trying your shot at it. He's done a great job with both the tutorials and the code.

## Getting started with the PCB
This first thing I did was get started with the schematic. I needed to figure out how to get this charliplexing done and create a prototype so that I am sure that it actually works.

I ordered some LEDs and started soldering them. The initial assembly wasn't a problem. But before actually soldering the LEDs to the board I made a schematic. THIS WAS A VERY IMPORTANT STEP.

I wired up a 10x9 version of the matrix for the prototype. This started with building a schematic for the same.

![Prototype Schematic](<../assets/proto_schematic.png>)

The schematic seems convoluted and messy at a first glance but it is rather simple. you just need to focus on and look for patterns.
A good friend of mine said this to me that, "90% of engineering is identifying patterns". I agree to him. If we zoom in a little and look at the little repeating patterns then we see the following.

![atomic_piece](../assets/repeating_segment.png)

You just need to replicate this piece and wire these segments together to make yourself a nice charliplexed schematic. When I started, I thought it would be difficult to wrap my head around this. It was rather just a matter of time and practise. I just had to start implementing the schematic. So I did. Interestingly as soon as I started implementing the design, everything starged coming along piece by piece.

You can start with a simpler and smaller grids like a 4X3 or 5X3 and so on. Once you are confident with the pattern, you can scale it up by adding the atomic pieces. I started with a an even simpler design which looked something like this.

TODO - Add a simpler Charliplexed matrix schematic.

This is a rather simpler design and gives you a basic idea of charliplexing wihtout the complex wiring. It is really a blessing to be abled to wire n(n-1) LEDs onver n GPIOs, thanks to Charliplexing. This also comes with its own constraints, as being able to manage these many LEDs through a matrix increases RAM overhead. This pushes does affect your MCU selection. We'll talk about MCU selection later in the article.

## Prototyping

After this was handwiring a prototype. which was fairly fun. I ordered a spool of 0.1mm enamel coated copper wire. (The best decision ever). Then I lost it somewhere in my living room the next day lol. I picked up some single core aluminum wires, which I had lying around. peeled off the unwanted cover and started soldering. Even with the simpler schematic the wiring was a little tricky. Firstly because of the thickness of the wire and scondly because of the messy matrix. Couldn't do anything about the wire (I tried looking but couldn't find it) but I sure could work around with the wiring.

TODO - Add an image of the route selection tool

Here KiCAD came in handly alot, especially the route/ path highlighter tool. The tool helped see the schematic in a more layer by layer approach. One GPIO string at a time. The process was slow but relaxing. I started with cutting and stripping the wire first and made strands of them ready to be soldered. Then was the fun part, soldering. 

TODO - add the high on solder fumes meme

I was not sure how this would look in the end. Turns out it started looking pretty cool. Not the very best soldering job but it does the trick.

TODO - ADD the wiring soldering image.

I miscalculated initially about how many LEDs I'd need. Once my first set of white LEDs were over, I had to bring in the green LEDs I had lying around. Not very pleasing to look but it does the job. 