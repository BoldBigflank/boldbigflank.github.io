---
layout: post
status: publish
published: true
title: Cocos2d-x Example Game - Runner Groove
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 401
wordpress_url: http://bold-it.com/?p=401
date: '2013-11-02 02:25:24 -0700'
date_gmt: '2013-11-02 02:25:24 -0700'
categories:
- Cocos2d-x
- Game
tags: []
comments: []
---
<p>I participated in AT&T's Hackathon during SIC 2013, and was invited to present at Seattle Interactive Conference 2013.  Alex Donn, the organizer of the event, has posted a <a href="http://developerboards.att.lithium.com/t5/AT-T-Developer-Program-Blogs/SIC-AT-amp-T-Wearables-Hackathon-Seattle-Event-Recap/ba-p/37117" target="_blank">recap of the event</a>.</p>
<p>  I used a <a href="http://www.plantronics.com/us/" target="_blank">Plantronics</a> headset to control a character.  Turning your head left/right controlled where the player moved, and tilting in one direction caused him to jump that way.  Tapping on the headset reset the orientation.  The level is created by arranging map segments one after the other, loading and unloading them as they are needed.  Plantronics gave me second place for their own category.  They also recorded me showing a demo of the game:</p>
<p><iframe width="560" height="315" src="//www.youtube.com/embed/mG_a3QnJs5k" frameborder="0" allowfullscreen></iframe></p>
<p>My dude was my first creation using Spine by <a href="http://esotericsoftware.com/" target="_blank">Esoteric Software</a>, a small operation based in Seattle.  I've done a few skins and animations for the 'dude', but used only one of each for the game.  Check this guy out</p>
<p><img src="http://bold-it.com/wp-content/uploads/2013/11/dude-walk.gif" alt="dude-walk" /></p>
<p>Lastly, the code I used is open to the public.  You can check out <a href="https://github.com/BoldBigflank/attsic" target="_blank">source on GitHub</a>.  Unfortunately, if you don't have a Plantronics Concept 1 headset, you won't have much control.  There are plenty of other concepts to see though, such as loading a TMX tilemap, aligning the viewport, checking for collisions and loading a Spine skeleton.</p>
