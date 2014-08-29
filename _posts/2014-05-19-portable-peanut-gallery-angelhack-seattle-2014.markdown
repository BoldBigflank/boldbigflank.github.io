---
layout: post
status: publish
published: true
title: Portable Peanut Gallery - AngelHack Seattle 2014
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 451
wordpress_url: http://bold-it.com/?p=451
date: '2014-05-19 20:51:56 -0700'
date_gmt: '2014-05-19 20:51:56 -0700'
categories:
- iOS
- Node.JS
tags: []
comments: []
---
<p>Using Echoprint technology, I made a system to listen to what movie is playing and then automatically synchronize my Rifftrax audio files to the movie.  <a href="http://www.hackathon.io/portable1" target="_blank">This was my entry</a> into AngelHack Seattle Spring 2014<br />
<a href="http://bold-it.com/wp-content/uploads/2014/05/2014-05-17-16.00.57.jpg"><img src="http://bold-it.com/wp-content/uploads/2014/05/2014-05-17-16.00.57.jpg" alt="AngelHack SEA 2014" class="aligncenter size-full wp-image-455" /></a><br />
There are a few parts to this system.  First, I took a couple movie files and ran them through <a href="https://github.com/echonest/echoprint-codegen" target="_blank">Echoprint-codegen</a>, and stored that in an Amazon RDS instance.  I used <a href="https://github.com/jhurliman/node-echoprint-server" target="_blank">node-echoprint-server</a> and modified it to include rifftrax-specific synchronizing information.  Then, I modified the <a href="https://github.com/echonest/echoprint-ios-sample" target="_blank">echoprint-ios-sample</a> app to play the proper rifftrax file at the correct time.</p>
<p><iframe width="640" height="360" src="//www.youtube.com/embed/IbxblRfMIsg?rel=0" frameborder="0" allowfullscreen></iframe></p>
<p>If you can't tell, the phrase "...every couch cushion." was the app's addition to the movie.</p>
<p>I'm really excited about this technology, and I plan to keep working on this product until it's ready for production.  There are many ways to improve this technology for this particular use case.</p>
