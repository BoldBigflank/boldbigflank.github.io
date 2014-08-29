---
layout: post
status: publish
published: true
title: CopterDude/Twistris - Sphero Hack Tour Seattle 2012
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 262
wordpress_url: http://www.bold-it.com/?p=262
date: '2012-09-03 19:07:11 -0700'
date_gmt: '2012-09-04 03:07:11 -0700'
categories:
- iOS
- Sphero
- Game
tags:
- Sphero
comments: []
---
<p><strong>Update 9/29/2012:</strong> Twistris has been named Disc Groove and is on <a href="http://itunes.apple.com/us/app/disc-groove/id561722255?ls=1&mt=8" target="_blank">iTunes</a> and <a href="https://play.google.com/store/apps/details?id=com.bold_it.discgroove" target="_blank">Google Play</a></p>
<p>Using Cocos2d-iphone, Objective-C and Sphero, I made a casual game which I find myself playing during short breaks.</p>
<p>I was a small part of the <a href="http://www.bold-it.com/?p=204">Sphero Hack Tour</a> in Seattle.  Oddly this project doesn't overlap with any of my previous projects.  I chose to make a game based on <a href="https://play.google.com/store/apps/details?id=com.throttlecopter&amp;hl=en">one</a> that I liked playing on Android.  I thought it would make a good Sphero-controlled game.</p>
<p>I won my Sphero from the <a href="http://www.bold-it.com/twilio/seattle-startup-weekend/">Seattle Startup Weekend</a> in May, and have been tinkering with it for a while.  I tried setting up an Android dev environment to connect to Sphero, but kept hitting snags.  Then I tried iOS and set everything up super quick.</p>
<p>I chose to make my game using <a href="http://www.cocos2d-iphone.org/">Cocos2d-iphone</a> because a former coworker had introduced me to it.  Once I got the basic gameplay down, I had a pretty fun game going.  In this game, you were pulled down by gravity constantly, and your only action was to pull up (reversing gravity while your finger was pressing the screen).  You therefore wiggled your way forward and avoided obstacles.</p>
<p><a href="http://bold-it.com/wp-content/uploads/2012/09/photo.png"><img class="alignnone  wp-image-263" title="CopterDude" src="http://bold-it.com/wp-content/uploads/2012/09/photo.png" alt="" width="576" height="384" /></a></p>
<p>Then I put the Sphero control in, and it was horrible.  I thought it would be great to just slowly rotate the ball counter-clockwise to go straight, but it didn't feel good at all.  It was time to change the style.  Instead of one person, you controlled three (or five).  The things to avoid (which I called beeDudes) were more spread out, and there were four of them at a time.  I created a space theme and had at it.</p>
<p><a href="http://bold-it.com/wp-content/uploads/2012/09/photo-1.png"><img class="alignnone  wp-image-264" title="Twistris" src="http://bold-it.com/wp-content/uploads/2012/09/photo-1.png" alt="" width="576" height="384" /></a></p>
<p>I worked on this at a leisurely pace over the two weeks that the competition allotted.  A second player can control meteors spawning by pressing the right quarter of the screen.</p>
<p>Programmers resources:</p>
<p><a href="https://github.com/BoldBigflank/twistris/" target="_blank">GitHub</a></p>
<p><iframe src="http://www.youtube-nocookie.com/embed/I6T9NOWuT5M" frameborder="0" width="560" height="315"></iframe></p>
