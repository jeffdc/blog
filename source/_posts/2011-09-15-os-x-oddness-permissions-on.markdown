---
layout: post
title: "OS X Oddness - Permissions On TMPDIR"
date: 2011-09-15 22:15
comments: true
categories: osx
---

I recently bought a new Mac. My first non-laptop Mac in fact. It is a gorgeously awesome 27" iMac. It replaces my old and mostly trusty MacBook Pro that I have had since late 2008. Right before I updated to the new machine I upgraded the old one to OS X 10.7, Lion. Overall it was pretty decent though I did have some issues (Flash was even worse than with Snow Leopard and Safari has become unusable). One other issue I had was with various applications not being able to save new documents. I poked around trying to figure it out and was given the advice to Repair Permissions from the Disk Utility. I did this and the problem persisted. I then forgot about the problem as my shiny new iMac had arrived.

I decided that it was time to do a clean install. The old MacBook Pro had been upgraded from Tiger to Leopard to Snow Leopard to Lion. There was much cruft and even some flakiness, due I am sure to the long life and many upgrades of the OS. So, I started over with the new machine. A fresh factory install of Lion. Liberating. I have been installing things as I need them and manually moved over my documents, music, and such. Good riddance to the cruft! Today I needed to create an OmniOutlier document. I installed the application, added my license, and off I went.

After a minute or so I faced the same damn error message that I was having on my old laptop. Lion telling me that it can not save my 'Untitled' document! Uggghh. I ran the repair permissions task from Disk Utility, it fixed a few things but it made no difference, still no luck saving any new documents from OmniOutliner. I then tried OmniGraffle, same thing. BBEdit, no problems. TextEdit, no problems. iWork, same problems as the Omni products. What is going on here?

After some googling and poking about I discover that the TemporaryItems directory in my $TMPDIR does not have group write permissions. A quick `sudo chmod g+w $TMPDIR/TemporaryItems` later and all is well. Why the hell is this happening? And why did it happen twice to me on two totally separate installs (with no migration between them) of Lion. And finally, why if this is such a seemingly common problem is google not aflame with others having this same issue? 

I never saw this pre-Lion. I had at first thought that it was an issue with Lion's file versioning feature, but this does not seem to be the case since TextEdit did not exhibit the behavior. Upon figuring out the permissions issue it is even odder since the inability to write to the TemporaryItems directory would seem to affect all applications that allow document creation, but yet it didn't. I am fairly sure that applications do not ever deal with the writing of the file to the TemporaryItems directory before it is moved to the place that they user has chosen to save. So it does not make much sense that some applications worked and others not.

A mystery...