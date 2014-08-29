---
layout: post
status: publish
published: true
title: Seattle Startup Weekend 2012
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 204
wordpress_url: http://www.bold-it.com/wordpress/?p=204
date: '2012-05-20 18:20:26 -0700'
date_gmt: '2012-05-21 02:20:26 -0700'
categories:
- Node.JS
- Twilio
tags:
- node.js tablesurfing
comments:
- id: 22
  author: Sheikh
  author_email: sheikhshuvo@gmail.com
  author_url: ''
  date: '2012-05-22 08:56:12 -0700'
  date_gmt: '2012-05-22 16:56:12 -0700'
  content: Great post - thanks for recapping the weekend and posting video! I've been
    inspired to play around with Twilio myself and try to get a fun app up and running.
- id: 23
  author: One Epic Weekend in Seattle in May | Seattle Startup Weekend
  author_email: ''
  author_url: http://seattle.startupweekend.org/2012/05/22/one-epic-weekend-in-seattle-in-may/
  date: '2012-05-23 10:45:15 -0700'
  date_gmt: '2012-05-23 18:45:15 -0700'
  content: '[...] From Alex Swan (Dev) Seattle Startup Weekend 2012 [...]'
- id: 24
  author: Making the best of a startup weekend | Thoughts from the other side&#8230;
  author_email: ''
  author_url: http://umeshunni.com/2012/05/making-the-best-of-a-startup-weekend/
  date: '2012-05-26 15:16:47 -0700'
  date_gmt: '2012-05-26 23:16:47 -0700'
  content: '[...] a social video watching application (Shubz.TV) and most recently
    a re-imagined dining experience (TableSurfing). As with 99% of startups, all of
    these idea have failed to get any traction beyond the very busy [...]'
- id: 25
  author: CopterDude/Twistris - Sphero Hack Tour Seattle 2012 - Bold IT - PHP, Python,
    Node.JS Development
  author_email: ''
  author_url: http://www.bold-it.com/ios/copterdudetwistris-sphero-hack-tour-seattle-2012/
  date: '2012-09-03 19:07:13 -0700'
  date_gmt: '2012-09-04 03:07:13 -0700'
  content: '[...] won my Sphero from the Seattle Startup Weekend in May, and have
    been tinkering with it for a while.  I tried setting up an Android dev [...]'
- id: 26
  author: PictoSphero - Sphero Hack Tour Seattle 2012 - Bold IT - PHP, Python, Node.JS
    Development
  author_email: ''
  author_url: http://www.bold-it.com/ios/pictosphero-sphero-hack-tour-seattle-2012/
  date: '2012-09-03 19:35:35 -0700'
  date_gmt: '2012-09-04 03:35:35 -0700'
  content: '[...] I got a Sphero from the Seattle Startup Weekend in May, I brainstormed
    what this thing could do.  I thought of a cool behavior for a Sphero, where [...]'
---
<p>I used <a href="http://nodejs.org/" target="_blank">Node.JS</a>, <a href="http://expressjs.com/" target="_blank">Express</a> and <a href="http://www.mongodb.org/" target="_blank">MongoDB</a> to create the back end for Seattle Startup Weekend group <a href="http://www.tablesurfing.org" target="_blank">TableSurfing.org</a>.</p>
<p><img alt="" src="http://bold-it.com/wp-content/uploads/2012/05/458191_10100312138778413_23200732_43543274_326208815_o.jpeg" title="at seattle startup weekend" class="alignnone" width="600" /></p>
<p>On Friday night, Sheikh Shuvo presented the idea of building a tool that allows people to meet local chefs in their area as well as show off their own cooking skills.  The idea got a lot of support, and a ten person team formed out of it.  We ended up with three developers, two graphic designers, four business/marketing people and Sheikh.  We were warned of some of the issues with a big team having to do with the limited time of the event, but I didn't notice any of those issues arising in my work.  We all had a pretty tight focus on what was important and got done everything we could.</p>
<p>Saturday was a beast.  I got a development system going both on my own system and an EC2 Instance, then dove in.  I set up MongoDB and made some models to manipulate via <a href="https://www.learnboost.com/blog/mongoose/" target="_blank">Mongoose</a>.  I set up Express and made the routes for all the actions that will be happening (user profiles creation/viewing, event creation/viewing/searching).  My codevelopers Ash and <a href="http://twitter.com/umeshunni" target="_blank">Umesh</a> made some Jade templates and CSS styles to match our designers' mockups on the front end.  After we were kicked out at midnight, I plugged away at the <a href="http://everyauth.com/" target="_blank">Everyauth</a> plugin to implement Facebook connectivity.</p>
<p>Two hours of sleep later, I was back in on Sunday, fixing bugs and putting out fires and making a solid demo.  Our marketing side was doing all sorts of things, from emailing professional chefs to hitting the streets asking others about the idea.</p>
<p>Here is our presentation from Sunday night (thanks to <a href="http://twitter.com/SteveSeow" target="_blank">Steve Seow</a> for recording). My cameo is about two and a half minutes in:<br />
<iframe width="640" height="360" src="http://www.youtube-nocookie.com/embed/AxMTpOWQQ7c" frameborder="0" allowfullscreen></iframe></p>
<p>It's got a long way to be useful, from both a development and a marketing perspective, but I'm excited to carry this forward to a working product.  I spent Sunday night exhausted but unable to sleep due to the amount of awesome I had just experienced.</p>
<p>The hardest part of the event was getting all the bugs out to have a working demo by the end of Sunday.  I still prefer that to street contacting, which our business team did great at.</p>
<p>What brought me the most joy was the simplicity of adding Twilio to the project.  I had made a little snippet that sent a text message through the Twilio REST API earlier, and dropping it in brought almost instant results.  For the tech-types, here's the code:</p>
<p>[javascript title="twilio.js"]<br />
var https = require('https');</p>
<p>var accountSid = &quot;AC********************************&quot;;<br />
var authToken = &quot;********************************&quot;;<br />
var API_SERVER = 'api.twilio.com';<br />
var API_VERSION = '2010-04-01';<br />
var from = &quot;+18889990000&quot;; // Twilio Verified number</p>
<p>exports.sendText = function(to, body, cb){<br />
    var postData = &quot;To=&quot; + to + &quot;&amp;From=&quot; + from + &quot;&amp;Body=&quot; + body;<br />
	var options = {<br />
        host: API_SERVER,<br />
        port: 443,<br />
        path: '/' + API_VERSION +&quot;/Accounts/&quot; + accountSid + &quot;/SMS/Messages&quot;,<br />
        method: 'POST',<br />
        auth: accountSid + ':' + authToken,<br />
        headers: {&quot;Content-Type&quot;:&quot;application/x-www-form-urlencoded&quot;,<br />
					&quot;Content-Length&quot;:postData.length}<br />
	};</p>
<p>	var req = https.request(options, function(res) {</p>
<p>        res.on('data', function(d) {<br />
            return cb(null, d);<br />
        });<br />
	});</p>
<p>	req.write(postData); // Write the body<br />
	req.end();</p>
<p>	req.on('error', function(e) {<br />
        console.error(e);<br />
        return cb(e, null);<br />
	});</p>
<p>};<br />
[/javascript]</p>
<p>I think there's a node.js helper library out now, so I would recommend that if you want all the features.</p>
