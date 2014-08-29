---
layout: post
status: publish
published: true
title: PubNub Acronym Game
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 242
wordpress_url: http://www.bold-it.com/?p=242
date: '2012-05-31 01:16:42 -0700'
date_gmt: '2012-05-31 09:16:42 -0700'
categories:
- PHP
- Twilio
- Game
tags: []
comments:
- id: 27
  author: Stephen Blum
  author_email: stephen@pubnub.com
  author_url: http://www.pubnub.com
  date: '2012-06-05 09:14:08 -0700'
  date_gmt: '2012-06-05 17:14:08 -0700'
  content: Alex, this is fantastic.  Really great job on the PubNub + Twilio mashup.  The
    future is here with technology accessibility via APIs on the web for Mobile devices.  Being
    able to tie together all devices on earth via PubNub and all telephony with Twilio
    is a powerful capability.  You have demonstrated this very well.
- id: 28
  author: BIlly
  author_email: pabfpb@gmail.com
  author_url: http://www.test.com/
  date: '2013-03-07 18:37:27 -0800'
  date_gmt: '2013-03-08 02:37:27 -0800'
  content: Great blog post thanks for posting
---
<p>Using Twilio, PubNub and PHP, I created a simple acronym creation and voting game.</p>
<p>See the demo <a href="http://dev.bold-it.com/Acro/game.php?acronym=PWN" target="_blank">in action</a>.</p>
<p>Check out the project on <a href="https://github.com/BoldBigflank/Acro" target="_blank">GitHub</a></p>
<p>Another of my childhood games was Acrophobia.  There are a few games like it nowadays, but none have the same audience or ambience as the original (ok, it was based on an IRC game, but I got hooked on this one first).</p>
<p>The words and entries are stored in a database.  Each acronym is its own <a href="http://www.pubnub.com" target="_blank">PubNub</a> channel, which enables users to receive updates instantly, without polling the server constantly.</p>
<p>I'm most proud of the SMS Simulator that allows people to try out the game without using their phones.  It is similar enough to a <a href="http://www.twilio.com" target="_blank">Twilio</a> webhook call that the game works just as if it had received a text message.</p>
<p>[php title="game.php"]<br />
&lt;?php<br />
// Connect to the database<br />
include_once(&quot;constants.php&quot;);</p>
<p>// Load the initial data from the database<br />
if(isset($_GET['acronym'])){<br />
	$acronym = strtoupper($_GET['acronym']);<br />
}<br />
else{// If there is no acronym, create one<br />
	// 3 - 7 characters<br />
	$size = rand(3, 7);<br />
	$acronym = &quot;&quot;;<br />
	$abc= array(&quot;a&quot;, &quot;b&quot;, &quot;c&quot;, &quot;d&quot;, &quot;e&quot;, &quot;f&quot;, &quot;g&quot;, &quot;h&quot;, &quot;i&quot;, &quot;j&quot;, &quot;k&quot;, &quot;l&quot;, &quot;m&quot;, &quot;n&quot;, &quot;o&quot;, &quot;p&quot;, &quot;q&quot;, &quot;r&quot;, &quot;s&quot;, &quot;t&quot;, &quot;u&quot;, &quot;v&quot;, &quot;w&quot;, &quot;x&quot;, &quot;y&quot;, &quot;z&quot;);<br />
	for($i = 1; $i &lt;= $size; $i++){<br />
		$acronym .= strtoupper($abc[rand(0,25)]);<br />
	}<br />
}</p>
<p>// Get phrases for that acronym<br />
$res = mysql_query(&quot;SELECT * FROM acro WHERE acronym = '$acronym'&quot;);</p>
<p>// Prepare the html for the list item<br />
$phrases = &quot;&quot;;<br />
while($phrase = mysql_fetch_assoc($res)){<br />
	$phrases .= &quot;&lt;tr&gt;&lt;td&gt;$phrase[id]&lt;/td&gt;&lt;td&gt;$phrase[body]&lt;/td&gt;&lt;td&gt;$phrase[votes]&lt;/td&gt;&lt;/tr&gt;&quot;;<br />
}</p>
<p>// Get previous rounds<br />
$res = mysql_query(&quot;SELECT acronym FROM acro GROUP BY acronym&quot;);<br />
$previousAcronyms = &quot;&quot;;<br />
while($a = mysql_fetch_assoc($res)){<br />
	$previousAcronyms .= &quot;&lt;a href='game.php?acronym=$a[acronym]'&gt;$a[acronym]&lt;/a&gt; &quot;;<br />
}</p>
<p>// Prepare the instructions<br />
if($twilio_number != &quot;XXX-XXX-XXXX&quot;)<br />
	$instructions = &quot;Text $twilio_number a phrase that matches this acronym,&lt;br&gt;then text the ID number of the best one to vote for it!&quot;;<br />
else<br />
	$instructions = &quot;Use the SMS Simulator to send a phrase that matches this acronym,&lt;br&gt;then send the ID number of the best one to vote for it!&quot;;</p>
<p>?&gt;&lt;html&gt;<br />
&lt;head&gt;<br />
	&lt;title&gt;Acro&lt;/title&gt;<br />
	&lt;link href='styles.css' rel='stylesheet' type='text/css'&gt;<br />
	&lt;script src=&quot;http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js&quot;&gt;&lt;/script&gt;<br />
&lt;/head&gt;<br />
&lt;body&gt;<br />
&lt;div id=&quot;header-bar&quot;&gt;&lt;span style=&quot;padding: 5px&quot;&gt;Acro (&lt;a href=&quot;https://github.com/BoldBigflank/Acro&quot;&gt;GitHub&lt;/a&gt;)&lt;/span&gt;&lt;/div&gt;<br />
	&lt;div id=&quot;page-wrapper&quot;&gt;<br />
		&lt;div class=&quot;acronym-wrapper&quot;&gt;<br />
			&lt;span align=&quot;center&quot; class=&quot;acronym&quot;&gt;&lt;?php echo $acronym; ?&gt;&lt;/span&gt;<br />
		&lt;/div&gt;<br />
		&lt;div class=&quot;instructions-wrapper&quot;&gt;<br />
			&lt;span class=&quot;instructions&quot;&gt;&lt;?php echo $instructions; ?&gt;&lt;/span&gt;<br />
		&lt;/div&gt;<br />
		&lt;div class=&quot;table-wrapper&quot;&gt;<br />
			&lt;table&gt;<br />
				&lt;thead class=&quot;grad&quot;&gt;&lt;tr&gt;&lt;th&gt;ID&lt;/th&gt;&lt;th&gt;Phrase&lt;/th&gt;&lt;th&gt;Votes&lt;/th&gt;&lt;/tr&gt;&lt;/thead&gt;<br />
				&lt;tbody id=&quot;phrases&quot;&gt;&lt;?php echo $phrases; ?&gt;&lt;/tbody&gt;<br />
			&lt;/table&gt;<br />
		&lt;/div&gt;<br />
		&lt;button onClick=&quot;var loc = window.location.href; window.location = loc.split('?')[0];&quot;&gt;New phrase&lt;/button&gt;<br />
		&lt;div class=&quot;previousAcronyms-wrapper&quot;&gt;<br />
			&lt;div class=&quot;previousAcronyms&quot;&gt;&lt;?php echo $previousAcronyms; ?&gt;&lt;/div&gt;<br />
		&lt;/div&gt;<br />
	&lt;/div&gt;<br />
	&lt;div class=&quot;smsBox&quot;&gt;<br />
		&lt;span id=&quot;smsTitle&quot;&gt;SMS Simulator&lt;/span&gt;&lt;br&gt;<br />
		&lt;input id=&quot;smsBody&quot; type=&quot;text&quot; /&gt;&lt;br&gt;<br />
		&lt;button id=&quot;smsSubmit&quot; onClick=&quot;sendSMS()&quot;&gt;Send SMS&lt;/button&gt;&lt;br&gt;<br />
		&lt;span id=&quot;smsResponse&quot;&gt;&lt;/span&gt;<br />
	&lt;/div&gt;<br />
	&lt;script&gt;<br />
	function sendSMS(){<br />
		var Body = $(&quot;#smsBody&quot;).val();<br />
		var From = &quot;web&quot; + Math.floor(Math.random()*100);<br />
		$.ajax({<br />
		  url: &quot;sms.php?From=&quot; + From + &quot;&amp;Body=&quot; + encodeURIComponent(Body),<br />
		  context: document.body,<br />
		  success: function(data){<br />
			  console.log(data);<br />
			  $(&quot;#smsBody&quot;).val(&quot;&quot;)<br />
			  $(&quot;#smsResponse&quot;).html(data)<br />
		  }<br />
		});<br />
	}<br />
	function getParameterByName(name) {<br />
		var match = RegExp('[?&amp;]' + name + '=([^&amp;]*)')<br />
                    .exec(window.location.search);<br />
    	return match &amp;&amp; decodeURIComponent(match[1].replace(/+/g, ' '));<br />
	}</p>
<p>	&lt;/script&gt;<br />
	&lt;div pub-key=&quot;&lt;?php echo $pn_pubkey; ?&gt;&quot; sub-key=&quot;&lt;?php echo $pn_subkey; ?&gt;&quot; ssl=&quot;off&quot; origin=&quot;pubsub.pubnub.com&quot; id=&quot;pubnub&quot;&gt;&lt;/div&gt;<br />
	&lt;script src=&quot;http://cdn.pubnub.com/pubnub-3.1.min.js&quot;&gt;&lt;/script&gt;<br />
	&lt;script&gt;(function(){</p>
<p>		var acronym = &quot;&lt;?php echo $acronym; ?&gt;&quot;;</p>
<p>	    // LISTEN FOR MESSAGES<br />
	    PUBNUB.subscribe({<br />
		    channel  : acronym,<br />
		    callback : function(message) {<br />
				$(&quot;#phrases&quot;).html(message.phrases)<br />
			}<br />
		})<br />
	})();&lt;/script&gt;<br />
&lt;/body&gt;<br />
&lt;/html&gt;<br />
[/php]</p>
