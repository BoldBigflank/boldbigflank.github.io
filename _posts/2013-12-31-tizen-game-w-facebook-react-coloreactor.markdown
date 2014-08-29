---
layout: post
status: publish
published: true
title: Tizen Game w/ Facebook React - ColoReactor
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 411
wordpress_url: http://bold-it.com/?p=411
date: '2013-12-31 22:57:29 -0800'
date_gmt: '2013-12-31 22:57:29 -0800'
categories:
- Javascript
- Node.JS
- Socket.IO
- Game
tags: []
comments: []
---
<p><a href="http://bold-it.com/wp-content/uploads/2013/12/2013-12-07-16.51.33.jpg"><img src="http://bold-it.com/wp-content/uploads/2013/12/2013-12-07-16.51.33.jpg" alt="2013-12-07 16.51.33" width=320px class="alignnone size-full wp-image-412" /></a></p>
<p>Using Facebook React UI Library and Socket.io, I created a game for the web, then ported it to the Tizen OS, which was pretty straight forward.  If you've set up a PhoneGap project or an Android application, Tizen won't be much different.</p>
<p>The ByMyApp Team organized a <a href="http://www.flickr.com/photos/bemyapp/sets/72157638454298046" title="Photos of the event" target="_blank">Tizen Devlab and Hackathon</a> at the SURF Incubator from December 6-7.  I pitched the idea of a multiplayer reaction game to get people excited about the event.  The concept is simple, when the button's color is the same as the border, hit the button first.  The winner gets a point.  Every device is connected to the same game.</p>
<p>I teamed up with an amazing designer named Jojo who created a great interface for the game.  After a long night, the game was set up, and the second day was spent making it pretty.</p>
<p>The back end was Node.js using <a href="http://socket.io/" target="_blank">Socket.io</a> and hosted on Heroku.  The UI is updated using <a href="http://facebook.github.io/react/" target="_blank">Facebook React</a>.</p>
<p>Check out the source on <a href="https://github.com/BoldBigflank/coloreact" title="ColoReact" target="_blank">Github</a></p>
<p><a href="http://coloreact.herokuapp.com" target="_blank">Play the Game</a></p>
<p>The Tizen game won Runner up for the event.</p>
<blockquote class="twitter-tweet" lang="en"><p>Jojo Wang and <a href="https://twitter.com/BoldBigflank">@BoldBigflank</a> won Runner Up with Coloreactor - sticky &amp; fun multiplayer game. <a href="https://twitter.com/search?q=%23FTW&amp;src=hash">#FTW</a> <a href="https://twitter.com/search?q=%23TizenSEA&amp;src=hash">#TizenSEA</a></p>
<p>&mdash; BeMyApp (@bemyapp) <a href="https://twitter.com/bemyapp/statuses/409569373456592897">December 8, 2013</a></p></blockquote>
<p><script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script></p>
