---
layout: post
status: publish
published: true
title: Create Temporary Phone Numbers Using Twilio
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 256
wordpress_url: http://www.bold-it.com/?p=256
date: '2012-08-08 13:19:07 -0700'
date_gmt: '2012-08-08 21:19:07 -0700'
categories:
- PHP
- Twilio
tags: []
comments:
- id: 29
  author: Elaine
  author_email: help@twilio.com
  author_url: ''
  date: '2012-12-11 17:13:19 -0800'
  date_gmt: '2012-12-12 01:13:19 -0800'
  content: Unfortunately, Craigslist does not accept VOIP numbers for its verification
    calls, and this includes Twilio numbers. So Twilio phone numbers cannot be used
    to verify Craigslist accounts.
- id: 30
  author: alex
  author_email: alex@bold-it.com
  author_url: http://www.bold-it.com
  date: '2012-12-16 18:51:19 -0800'
  date_gmt: '2012-12-17 02:51:19 -0800'
  content: That's fine, I didn't use this for creating usernames or person verification.  This
    is just something you can put in a public forum with the ability to drop in the
    future.
---
<p>Using Twilio and PHP, you can create a temporary phone number for your own purposes.  You can put this on Craigslist for some ads, and delete the number when you're done.</p>
<p>The less tech-advanced can use <a href="http://burnerapp.com" target="_blank">Burner Phone</a>, which also has more features than this particular script.  I built my script for a most basic forwarding, and it does just that.</p>
<p>[php title="forward.php"]<br />
&lt;?php<br />
// Constants<br />
$TWILIO_ACCOUNT_SID = &quot;&quot;; // Your Twilio Account SID<br />
$TWILIO_AUTH_TOKEN = &quot;&quot;; // Your Twilio Auth Token<br />
$FORWARD_NUMBER = &quot;&quot;; // The number to receive the calls/texts in format +1XXXYYYZZZZ</p>
<p>$to = $_REQUEST['To'];<br />
$from = $_REQUEST['From'];<br />
$body = $_REQUEST['Body'];</p>
<p>if($_REQUEST['CallSid']){ // Phone Call<br />
	print &lt;&lt;&lt;END<br />
&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;<br />
&lt;Response&gt;<br />
  &lt;Dial callerId='$from'&gt;$FORWARD_NUMBER&lt;/Dial&gt;<br />
&lt;/Response&gt;<br />
END;<br />
}<br />
else if($from == &quot;$FORWARD_NUMBER&quot;){ // SMS Reply<br />
	// Send the message to the last person who sent a text<br />
	$json_string = file_get_contents(&quot;https://$TWILIO_ACCOUNT_SID:$TWILIO_AUTH_TOKEN@api.twilio.com/2010-04-01/Accounts/$TWILIO_ACCOUNT_SID/SMS/Messages.json?To=$to&quot;);<br />
	$parsed_json = json_decode($json_string, TRUE);<br />
	foreach($parsed_json['sms_messages'] as $message){<br />
		if($message['from']==&quot;$FORWARD_NUMBER&quot;)<br />
			continue;<br />
		$recipient = $message['from'];<br />
		break;<br />
	}<br />
	print &lt;&lt;&lt;END<br />
&lt;Response&gt;<br />
&lt;Sms to='$recipient'&gt;$body&lt;/Sms&gt;<br />
&lt;/Response&gt;<br />
END;<br />
}<br />
else{ // SMS<br />
	print &lt;&lt;&lt;END<br />
&lt;Response&gt;<br />
&lt;Sms to='$FORWARD_NUMBER'&gt;$from:$body&lt;/Sms&gt;<br />
&lt;/Response&gt;<br />
END;<br />
}</p>
<p>?&gt;<br />
[/php]</p>
<p>The way this is set up, you don't even need your own database.  This just uses the Twilio SMS log.  There are a few drawbacks: phone calls are incoming-only; you can only send messages to the most recent person; and long messages may be curtailed.  Luckily, it's still useful enough for most purposes.</p>
<p>To use this script:</p>
<ol>
<li>Save this script to your server (updating the first three lines)</li>
<li>Buy a number from <a href="http://www.twilio.com" target="_blank">Twilio</a></li>
<li>Point the SMS and Voice URL to your script</li>
<li>Use the number as your own</li>
</ol>
<p>Simple as that!</p>
