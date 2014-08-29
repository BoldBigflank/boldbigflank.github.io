---
layout: post
status: publish
published: true
title: Cards Against Humanity - Comparison game
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 252
wordpress_url: http://www.bold-it.com/?p=252
date: '2012-08-07 18:50:03 -0700'
date_gmt: '2012-08-08 02:50:03 -0700'
categories:
- Javascript
- Knockout.JS
- Node.JS
- Socket.IO
- Game
tags: []
comments: []
---
<p>Using Node.JS, Socket.IO and Knockout.JS, I created a comparison game using the rules of open source card game Cards Against Humanity.</p>
<p><a href="http://cardsagainsthumanity.com/">Cards Against Humanity</a> is a card game for horrible people.  The premise of the game is like Apples to Apples.  Every round, a judge draws a category card.  Players pick from their hand the white card that fits best with the category (by their own judgement).  After all have picked, the judge chooses their favorite entry and the player whose card is picked gets a point.</p>
<p>This game uses Socket.io to send messages to clients.  The client side uses Knockout.JS to update the interface.</p>
<p>The demo is up at <a href="http://meta4.herokuapp.com">http://meta4.herokuapp.com</a>.  Check out the code yourself at <a href="https://github.com/BoldBigflank/meta4">Github</a>.</p>
