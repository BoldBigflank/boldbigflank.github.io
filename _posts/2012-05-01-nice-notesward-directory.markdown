---
layout: post
status: publish
published: true
title: Nice Notes/Ward Directory
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 123
wordpress_url: http://www.bold-it.com/wordpress/?p=123
date: '2012-05-01 23:16:02 -0700'
date_gmt: '2012-05-01 23:16:02 -0700'
categories:
- PHP
- Twilio
tags: []
comments: []
---
<p>(Posting from a Starbucks in Seattle, because it seemed like the right thing to do)</p>
<p>I made a SMS service for people in my local church group to send each other anonymous compliments (nice notes) and receive responses.  The process is simple:</p>
<p>Send the following to the Twilio number: &lt;First name&gt; &lt;Last name&gt; &lt;message&gt;</p>
<p>This has a second feature: If there are less than three words in the text message, it checks the directory of people for names that are similar, and returns the name and addresses of those.</p>
<p>[php title="sms.php"]<br />
&lt;?php<br />
$AccountSid = &quot;&quot;;<br />
$AuthToken = &quot;&quot;;</p>
<p>// Connect to the database<br />
$con = mysql_connect(&quot;localhost&quot;,&quot;root&quot;,&quot;&quot;);<br />
mysql_select_db(&quot;nicenotes&quot;, $con);</p>
<p>$message = parseBody($_GET['Body']);<br />
$From = phoneUS($_GET['From']);</p>
<p>if($message['to'] &amp;&amp; $message['text']){<br />
	// Log the message<br />
	if($message['to'] != $From){<br />
		$sql = &quot;INSERT INTO log SET log.`To` = '$message[to]', log.`Re` = '$From', log.`Body` = '$message[text]'&quot;;<br />
		mysql_query($sql);<br />
	}<br />
	echo &quot;&lt;Response&gt;&quot;;<br />
	echo &quot;&lt;Sms to=&quot;$message[to]&quot;&gt;$message[text]&lt;/Sms&gt;&quot;;<br />
	echo &quot;&lt;/Response&gt;&quot;;<br />
}<br />
else{<br />
	echo &quot;&lt;Response&gt;&quot;;<br />
	echo &quot;&lt;Sms&gt;Could not figure out who you were trying to message.  Try again, or tell Alex Swan.&lt;/Sms&gt;&quot;;<br />
	echo &quot;&lt;/Response&gt;&quot;;<br />
}</p>
<p>function parseBody($Body){<br />
	// Load the csv<br />
	$names = array();<br />
	$fp = fopen('menu.csv', 'r');<br />
	while($line = fgets($fp)){<br />
		$parts = explode(&quot;,&quot;, $line);<br />
		$names[strtolower($parts[0])] = $parts[1];<br />
	}<br />
	fclose($fp);<br />
	// Get the first two words of the Body</p>
<p>	$arrayMatches = explode(&quot; &quot;, $Body);<br />
	if($arrayMatches &amp;&amp; count($arrayMatches) &gt;= 3){ // It's a nice note<br />
		$name = strtolower($arrayMatches[0] . &quot; &quot; . $arrayMatches[1]);<br />
		if(isset($names[&quot;$name&quot;])){ // It's a new one<br />
			$to = $names[&quot;$name&quot;];<br />
			$message = substr($Body, strlen($name)+1);<br />
			return array(&quot;to&quot;=&gt;phoneUS($to), &quot;text&quot;=&gt;&quot;Provo 174th e-note: &quot; . htmlspecialchars($message));<br />
		}<br />
		else{ // It's possibly a reply<br />
			// Check old messages to respond<br />
			// Find the name based on the sender<br />
			$From = phoneUS($_GET['From']);<br />
			$sql = &quot;SELECT * FROM log WHERE log.`To` = '$From' ORDER BY id DESC LIMIT 1&quot;;<br />
			$result = mysql_query($sql);<br />
			if($log = mysql_fetch_array($result)){<br />
				return array(&quot;to&quot;=&gt;phoneUS($log['Re']), &quot;text&quot;=&gt;&quot;e-note reply: &quot; . htmlspecialchars($Body));<br />
			}<br />
		}<br />
	}<br />
	else{ // It's guessing the name<br />
		$message = array();<br />
		$Body = strtolower($Body);<br />
		foreach($names as $key=&gt;$value){<br />
			$nameArray = explode(&quot; &quot;, $key);<br />
			if(levenshtein($nameArray[0], $Body) &lt;= 2 || levenshtein($nameArray[1], $Body) &lt;= 2 || levenshtein($key, $Body) &lt;= 4){<br />
				array_push($message, ucwords($key) . &quot;: $value&quot;);<br />
			}<br />
		}<br />
		return array(&quot;to&quot;=&gt;phoneUS($_GET['From']), &quot;text&quot;=&gt;htmlspecialchars(implode($message)));<br />
	}<br />
}</p>
<p>function phoneUS($number){<br />
    $pattern = &quot;/^D*[1]?D*(d{3})D*(d{3})D*(d{4})(?:D*)$/&quot;;<br />
    preg_match($pattern, $number, $numberArray);</p>
<p>    if(!$numberArray){<br />
        return 0;<br />
    }<br />
	return &quot;+1&quot;.$numberArray[1].$numberArray[2].$numberArray[3];<br />
}</p>
<p>?&gt;<br />
[/php]</p>
<p>The directory of members is a csv file in this fashion:<br />
[text]<br />
Al Deans,8884446633<br />
Alex Foy,5557770000<br />
[/text]</p>
<p>And the mysql database it checks looks like this:<br />
[sql]<br />
CREATE TABLE `log` (<br />
  `id` int(11) unsigned NOT NULL AUTO_INCREMENT,<br />
  `To` varchar(14) DEFAULT NULL,<br />
  `Re` varchar(14) DEFAULT NULL,<br />
  `Body` varchar(320) DEFAULT NULL,<br />
  PRIMARY KEY (`id`)<br />
) ENGINE=InnoDB AUTO_INCREMENT=84 DEFAULT CHARSET=latin1;<br />
[/sql]</p>
