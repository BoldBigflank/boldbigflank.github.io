---
layout: post
status: publish
published: true
title: Cat Facts (aka Annoy Your Friends)!
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 98
wordpress_url: http://www.bold-it.com/wordpress/?p=98
date: '2012-04-28 00:01:13 -0700'
date_gmt: '2012-04-28 00:01:13 -0700'
categories:
- PHP
- Twilio
tags: []
comments: []
---
<p>A text conversation went viral a while ago, where a guy sent his friend text messages about cat facts, and then messed with him when he tried to get them to stop.  It was a clever idea, and seemed like a quick app to make using Twilio, so I did.</p>
<p>The initial system was made in about 20 minutes, but I kept adding features and fixes.  You send the phone number you would like to annoy to your Twilio number, then the system will send a cat fact to your friend.  Messages that do not contain a phone number will be responded with more cat facts.  Here's how it looks now:</p>
<p>[php title="sms.php"]<br />
&lt;?php<br />
$AccountSid = &quot;ACXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX&quot;;<br />
$Authtoken = &quot;YYYYYYYYYYYYYYYYYYYYYYYYYYYYYYYY&quot;;<br />
// Get a greeting based on the body<br />
$Body = $_GET['Body'];<br />
if(stripos($Body, &quot;e4n3m23pd90vc4:9nfaDFADFD42baconP0o&quot;) !== FALSE){<br />
	$greeting = &quot;&amp;lt;Command not recognized&amp;gt; &quot;;<br />
}<br />
else if(stripos($Body, &quot;stop&quot;) !== FALSE || strlen($Body)&gt;30){<br />
	$greeting = &quot;Hammer time. &quot;;<br />
}<br />
else if(stripos($Body, &quot;fuck&quot;) !== FALSE || stripos($Body, &quot;shit&quot;) !== FALSE || stripos($Body, &quot;asshole&quot;) !== FALSE){<br />
	$greeting = &quot;Watch your language meow! &quot;;<br />
}<br />
else{<br />
	$greeting = &quot;Thank you for using Fun Feline Facts! &quot;;<br />
}</p>
<p>// Keep from infinite loops<br />
if(phoneUs($Body)==phoneUs($_GET['To'])){<br />
	return;<br />
}</p>
<p>// Stop abusers<br />
$url = &quot;https://$AccountSid:$Authtoken@api.twilio.com/2010-04-01/Accounts/$AccountSid/SMS/Messages.json?To=&quot;. $_GET['To'] . &quot;&amp;From=&quot; . $_GET['From'] . &quot;&amp;DateSent=&quot; . date(&quot;Y-m-d&quot;);<br />
$result = json_decode(getUrl($url), true);<br />
$count = (isset($result['total'])) ? $result['total'] : 0;</p>
<p>// Load the file<br />
$handle = fopen(&quot;facts.txt&quot;, 'r');<br />
$facts = array();<br />
while($fact = fgets($handle))<br />
	array_push($facts, $fact);</p>
<p>$message = &quot;&quot;;<br />
while($message==&quot;&quot; || strlen($message)&gt;160){<br />
	$random = rand(0, count($facts));<br />
	$randomFact = trim($facts[$random]);</p>
<p>	$message = htmlspecialchars(&quot;$greeting$randomFact Me-wow!&quot;);<br />
}</p>
<p>$toAttribute = (phoneUs($Body)!=0) ? &quot;to=&quot;&quot; . phoneUs($Body) . &quot;&quot;&quot; : &quot;&quot;;<br />
echo &quot;&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;&quot;;<br />
echo &quot;&lt;Response&gt;&quot;;<br />
if($count&lt;8){<br />
	while(strlen($message)&gt;0){<br />
		echo &quot;&lt;Sms $toAttribute&gt;&quot; . substr($message, 0, 160) . &quot;&lt;/Sms&gt;&quot;;<br />
		$message = substr($message, 160);<br />
	}<br />
	if($toAttribute != &quot;&quot; &amp;&amp; phoneUS($Body) != phoneUs($_GET['From']))<br />
		echo &quot;&lt;Sms&gt;(&quot; . ++$count . &quot; of 8 per day)A cat fact has been sent to your friend. Purr-fect! felinefacts@bold-it.com&lt;/Sms&gt;&quot;;<br />
}<br />
echo &quot;&lt;/Response&gt;&quot;;</p>
<p>function phoneUS($number){<br />
    $pattern = &quot;/^D*[1]?D*(d{3})D*(d{3})D*(d{4})(?:D*[xX]D*(d*))?$/&quot;;<br />
    preg_match($pattern, $number, $numberArray);</p>
<p>    if(!$numberArray){<br />
        return 0;<br />
    }<br />
	$extension = isset($numberArray[4]) ? $numberArray[4] : &quot;&quot;;<br />
	return &quot;+1&quot;.$numberArray[1].$numberArray[2].$numberArray[3];<br />
}</p>
<p>function getUrl($url) {<br />
    $ch = curl_init();<br />
    curl_setopt($ch, CURLOPT_URL, $url);<br />
    curl_setopt($ch, CURLOPT_HEADER, 0);<br />
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);<br />
    $result = curl_exec($ch);<br />
    curl_close($ch);<br />
    return $result;<br />
}<br />
?&gt;<br />
[/php]</p>
<p>And the file of <a href="http://bold-it.com/wp-content/uploads/2012/04/facts.txt" target="_blank">facts</a> it uses</p>
<p>The first section (lines 6-17) add a little spice to the conversation.  If it detects a few key words, it will change the message slightly.</p>
<p>[php]<br />
// Get a greeting based on the body<br />
if(stripos($Body, &quot;e4n3m23pd90vc4:9nfaDFADFD42baconP0o&quot;) !== FALSE){<br />
	$greeting = &quot;&amp;lt;Command not recognized&amp;gt; &quot;;<br />
}<br />
else if(stripos($Body, &quot;stop&quot;) !== FALSE || strlen($Body)&gt;30){<br />
	$greeting = &quot;Hammer time. &quot;;<br />
}<br />
else if(stripos($Body, &quot;fuck&quot;) !== FALSE || stripos($Body, &quot;shit&quot;) !== FALSE || stripos($Body, &quot;asshole&quot;) !== FALSE){<br />
	$greeting = &quot;Watch your language meow! &quot;;<br />
}<br />
else{<br />
	$greeting = &quot;Thank you for using Fun Feline Facts! &quot;;<br />
}<br />
[/php]</p>
<p>Someone had the bright idea to send its own number to itself, causing an infinite loop.  After it crashed the system, I put the next section in.</p>
<p>[php]// Keep from infinite loops<br />
if(phoneUs($Body)==phoneUs($_GET['To'])){<br />
	return;<br />
}[/php]</p>
<p>We got a few people who would spam the same number 30+ times, really racking up the credit costs.  To stop this, I checked the logs to see how often they had used the system that day, and stopped working at around 8 messages.</p>
<p>[php]// Stop abusers<br />
$url = &quot;https://$AccountSid:$Authtoken@api.twilio.com/2010-04-01/Accounts/$AccountSid/SMS/Messages.json?To=&quot;. $_GET['To'] . &quot;&amp;From=&quot; . $_GET['From'] . &quot;&amp;DateSent=&quot; . date(&quot;Y-m-d&quot;);<br />
$result = json_decode(getUrl($url), true);<br />
$count = (isset($result['total'])) ? $result['total'] : 0;[/php]</p>
<p>After those checks, it loads the cat fact file, picks one (that will fit in just one message), and puts the greeting, fact and suffix together.</p>
<p>[php]// Load the file<br />
$handle = fopen(&quot;facts.txt&quot;, 'r');<br />
$facts = array();<br />
while($fact = fgets($handle))<br />
	array_push($facts, $fact);</p>
<p>$message = &quot;&quot;;<br />
while($message==&quot;&quot; || strlen($message)&gt;160){<br />
	$random = rand(0, count($facts));<br />
	$randomFact = trim($facts[$random]);</p>
<p>	$message = htmlspecialchars(&quot;$greeting$randomFact Me-wow!&quot;);<br />
}[/php]</p>
<p>Lastly, it prepares a TwiML response, directing one message to the new person, and one back at the sender as confirmation.</p>
<p>[php]$toAttribute = (phoneUs($Body)!=0) ? &quot;to=&quot;&quot; . phoneUs($Body) . &quot;&quot;&quot; : &quot;&quot;;<br />
echo &quot;&lt;?xml version=&quot;1.0&quot; encoding=&quot;UTF-8&quot;?&gt;&quot;;<br />
echo &quot;&lt;Response&gt;&quot;;<br />
if($count&lt;8){<br />
	while(strlen($message)&gt;0){<br />
		echo &quot;&lt;Sms $toAttribute&gt;&quot; . substr($message, 0, 160) . &quot;&lt;/Sms&gt;&quot;;<br />
		$message = substr($message, 160);<br />
	}<br />
	if($toAttribute != &quot;&quot; &amp;&amp; phoneUS($Body) != phoneUs($_GET['From']))<br />
		echo &quot;&lt;Sms&gt;(&quot; . ++$count . &quot; of 8 per day)A cat fact has been sent to your friend. Purr-fect! felinefacts@bold-it.com&lt;/Sms&gt;&quot;;<br />
}<br />
echo &quot;&lt;/Response&gt;&quot;;[/php]</p>
<p>At the end of my file I've made two helper functions.  The first takes the body of the text message and sees if it can pull a US phone number from it (since people have many ways of creating a phone number) and returns it in standard format.  The second function is just a cURL function that helps handling the call to the Twilio SMS Log.</p>
<p>[php]function phoneUS($number){<br />
    $pattern = &quot;/^D*[1]?D*(d{3})D*(d{3})D*(d{4})(?:D*[xX]D*(d*))?$/&quot;;<br />
    preg_match($pattern, $number, $numberArray);</p>
<p>    if(!$numberArray){<br />
        return 0;<br />
    }<br />
	$extension = isset($numberArray[4]) ? $numberArray[4] : &quot;&quot;;<br />
	return &quot;+1&quot;.$numberArray[1].$numberArray[2].$numberArray[3];<br />
}</p>
<p>function getUrl($url) {<br />
    $ch = curl_init();<br />
    curl_setopt($ch, CURLOPT_URL, $url);<br />
    curl_setopt($ch, CURLOPT_HEADER, 0);<br />
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);<br />
    $result = curl_exec($ch);<br />
    curl_close($ch);<br />
    return $result;<br />
}[/php]</p>
