---
layout: post
title:  "Doors and Corners"
date:   2021-05-29 17:00:00 +0100
categories: software testing development
---

This week, we bought a new WiFi router for the house. Our internet has been dropping in and out, and the ISP provided router is pretty terrible regardless - so it was time to invest in a nice solid mesh network. Expecting to encounter trouble in the setup, it wasn't surprising that the living room was rapidly filled by cables, boxes, laptops and devices, trying to get the internet even working again. At first, the assumption was (and those who work in development will already be suspicious), that the issue was my ISP modem trying to connect to the WiFi router. Plenty of angry people online had the same issue, so a great deal of time was spent factory-resetting and restarting the two devices. 

After a while of banging my head against this particular wall, it was time to take a more methodical approach to testing the setup. I quickly established that:
- The ISP modem was definitely connecting to the internet
- The WiFi router was definitely being connected to this internet connection
- The issue was somewhere in the WiFi network setup via the app

Having established this, the offending phone was switched out for an older model - instant success. WiFi was setup first try, and could even connect to the management account using the original, more up to date phone. Somewhere there was an issue preventing my phone from completing the setup. If there hadn't been a bad assumption made at the start of the process, instead rigorously testing everything end-to-end, it would have been a much more relaxing Friday night. Hence, this blog post - the importance of testing as a software developer.

## Why you need to test

There is an incorrect idea that testing is somehow easier than software development - when in reality, it's just a different set of skills. Certainly I'm not about to claim to be an expert software tester - but you pick up enough if you pay attention to at least have some confidence in the software you ship. The key principle to follow, for me anyway, is really simple - never trust yourself. Writing code is significantly easier than reading code, so reading and *understanding* everything about the code just based on the text seems like madness. Even just a quick runthrough a set of code with a debugger can be illuminating - to say nothing of being able to end-to-end test the solution that is utilising what you've written.

> Never trust yourself

Ultimately, computers do what you program them to do - or the person whose package you've included programmed them to do. Which by extension you told the computer to use. They don't magically break, or suddenly decide that they don't want to work - things go wrong when things change. This is either code changes, in which case you've caused a regression, or a change in inputs - in which case, you potentially missed something the first time round. It's important to have ownership of defects - whilst blame is toxic, trying to hand-wringingly avoid responsibility for the software shipped can be even worse.

## Not just the happy path

One of the classic mistakes in testing as a developer is being too restrictive in your testing. It can feel like a chore, trying to expand the scope of testing outside of the exact changes you've made, especially in a really knotty environment. This isn't even talking about expanding automated testing - which I'll come to in a moment - but doing a few extra tests against that new feature you've implemented. Attacking the codebase as if you're trying to break it, rather than with the knowledge of how the system works. Making an attempt to divorce your knowledge of the code from the interface itself is key here. You should treat testing the software and fixing the software as two separate tasks - even if you're rapidly alternating between the two. It's easy to fall back into just churning out code again after fixing that first bug, when there might be more just next door to the initial defect that you've missed.

This also includes the fixing of bugs in itself. It can be tempting to only test the case in which the bug appears - a red/green test, automated or not, showing that you've fixed the problem. This can leave you blind to huge areas of regression though - in fact, the issue becomes worse when the bug is really small. Large bugs are often the consequence of multiple, smaller issues coming together. Small bugs, in comparison, run the risk of creating more bugs in the fixing of them. The classic would be fixing an input form that fails all the time - sure, now it's succeeding, but what if someone now uses that working form with different inputs to the default ones? Or maybe even tries some SQL injection?

## You can probably automate it if you really try

Automated testing is often painted as being a chore rather than something really useful. Doing it by rote certainly can be - the idea of aiming for a certain percentage of code coverage example, kind of misses the point. Instead, a focus on testing what is important is key. This will change from domain to domain, but a classic to fall back on is testing decisions - if there is an ```if``` statement somewhere, you can do worse things than wrapping the two conditions in unit tests, even if it's super simple.

Something that has become more meaningful to me recently, with unit testing especially, is automated testing's value as proof-of-work. You should be able to trust your colleagues when they tell you that they've tested the software they've written - same as they would trust you. Automated tests show what you did to test the software that you've written - whether that's a quick console app for integration/e2e testing or a unit testing project, it almost doesn't matter. It can help spot material weaknesses in the testing as well - the classic "what about x?" question.

## It's not the thing that breaks you...

The closing note on this is that testing isn't about the thing that you know is going to break. When you know a library has a tendency to be flakey, or a particular section of code is a bit ropey, you'll naturally give it more attention. What will trip you up is the "innocuous" change that takes out a big chunk of the system, usually through an unintended side effect elsewhere. There [have been](https://www.theregister.com/2021/04/27/teams_down/) a string of [string of](https://www.theregister.com/2021/05/20/microsoft_azure_outage/) high-profile incidents recently, and not from [small companies](https://www.theregister.com/2021/05/19/salesforce_root_cause/). No one is immune to production deficiencies, the key is having a quick turnaround for getting a fix in place - rather than having to scratch around in the dirt for a week trying to find the problem.

Much like the routers from the start of this post - the modem and the router were expected to not play nice. The phone was never even in the equation. Because of that blind spot, what should have been a simple case of trying things end to end, turned into hours of frustration.