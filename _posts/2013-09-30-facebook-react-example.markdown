---
layout: post
status: publish
published: true
title: Facebook React Example - QuizTime
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 397
wordpress_url: http://bold-it.com/?p=397
date: '2013-09-30 23:55:29 -0700'
date_gmt: '2013-09-30 23:55:29 -0700'
categories:
- Javascript
- Node.JS
- Game
tags: []
comments: []
---
<p>Here is an example <a href="http://facebook.github.io/react/" target="_blank">Facebook React</a> web app I created at Facebook Seattle's hackathon.  I had the idea a little while before and React was the perfect way to update the DOM in a quick and responsive manner.  You can check out the source code on <a href="https://github.com/BoldBigflank/qtserver/tree/trivia" target="_blank">GitHub</a>.</p>
<p><img src="http://bold-it.com/wp-content/uploads/2013/09/Screen-Shot-2013-09-30-at-4.24.28-PM.png" alt="The game interface" /></p>
<h2>The Game</h2>
<p>The game itself is pretty simple. People join the "room" by going to <a href="http://qu.izti.me" target="_blank">http://qu.izti.me</a> on their device.  Large displays will show a leaderboard along with the game, and small displays (such as phones) will act as personal gamepads.  Users will see questions and a choice of answers.  The faster you answer, the more points you earn. Earn the most points to make it to the top of the leaderboard.  You can see how quickly others are answering because their name is highlighted on the leaderboard when they've put an answer in.  After every round you can see who got the answer right or wrong also by their color.  The winner is the one who has the highest score.</p>
<h2>Creation</h2>
<p>I created the game server in Node.js from a different game I had made previously (you can check that out in the master branch).  This is where the game state is stored along with questions and placeholder names.  The first thing I did was create the game rules.  When users enter the site, they start with a basic index.html.  They load socket.js, which loads the React components and connects to the server using Socket.io.  When any player makes a change to the game, the server broadcasts the relevant information along the "game" channel, which React picks up and updates the DOM accordingly.  Before, I would take the data and reprocess all the information using jQuery.  React fixed that, so all the code that's necessary is <code>self.setState(data);</code>.  I put a coat of polish on it by taking a theme from <a href="http://bootswatch.com/" target="_blank">Bootswatch</a> and updating the layout I created to Bootstrap 3.0.0.  I threw the game up onto the Heroku server I used before and it was ready to demo to the public.</p>
<h2>Conclusion</h2>
<p>At the end of the day, I presented Qu.izti.me with along with 14 other teams.  I got to demonstrate the game's ability to be played with or without a large second screen when the podium automatically shut off at 9:00pm.  I was lucky to win Best Overall App that night.  In my opinion, Socket.io and React go together like chocolate and peanut butter.  The page was always an accurate representation of the game object.<br />
<img src="https://pbs.twimg.com/media/BVTlexfCEAAMr66.jpg" alt="The Facebook React group photo" /></p>
