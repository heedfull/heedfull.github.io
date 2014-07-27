---
layout: post
title: "Getting Started, creating a scaffold"
date: 2014-07-14 19:56:32 +0100
comments: true
categories: FeedToShare
---
This is a continuation of the the [first post][FirstPost] on the building of a FeedToShare. In that post we created the app and installed some gems that we are going to need for testing it.

In this post we are going to create or first entity and all the accompaning files including our tests.

What we need to decide on first is our data model. Whilst I have a very specific problem in mind I'm trying to develop this web app so that it is generic enough that it could be used for other feeds, or even multiple feeds. The best starting place is that we will need a feed object.

[FirstPost]: [{% post_url 2014-07-05-introducing-feedtoshare %}]