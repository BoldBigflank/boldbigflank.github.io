---
layout: post
status: publish
published: true
title: Deep Thoughts by Jack Handey
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 62
wordpress_url: http://www.bold-it.com/wordpress/?p=62
date: '2012-04-26 06:45:45 -0700'
date_gmt: '2012-04-26 06:45:45 -0700'
categories:
- PHP
- Python
- Twilio
tags: []
comments: []
---
<p>UPDATE: The code needed to be changed just a little, since the php function scandir did not work any more.  Details below.</p>
<p>I had my friend Drew (<a href="https://twitter.com/#!/VVADrew">@VVADrew</a>) do some voice work with a collection of funny thoughts for a Twilio contest a while back.  The call will loop indefinitely, each time choosing a random thought from a collection I saved to Amazon S3.  Hit the button to have a listen.</p>
<p><?php wp_c2client("APea9f479790404ae7806db3ed59ba68ce", "Deep Thought"); ?><br />
<a href="http://bold-it.com/wp-content/uploads/2012/04/10330519_707213019325421_4246844595203672680_n.jpg"><img src="http://bold-it.com/wp-content/uploads/2012/04/10330519_707213019325421_4246844595203672680_n.jpg" alt="The judges got a kick out of it." class="aligncenter size-full wp-image-449" /></a></p>
<p>The code itself is quite simple:</p>
<p>[php title="voice.php"]<br />
&amp;lt;?php<br />
$dir = &amp;quot;audio&amp;quot;;<br />
$bucket = &amp;quot;https://s3.amazonaws.com/twiliodeepthought&amp;quot;;<br />
$listing = simplexml_load_string(file_get_contents($bucket));<br />
$files = $listing-&amp;gt;Contents;<br />
$random = rand(0, count($files));<br />
$file = $files[$random]-&amp;gt;Key;</p>
<p>echo &amp;lt;&amp;lt;&amp;lt;END<br />
&amp;lt;Response&amp;gt;<br />
&amp;lt;Play&amp;gt;$bucket/$file&amp;lt;/Play&amp;gt;<br />
&amp;lt;Pause length=&amp;quot;4&amp;quot; /&amp;gt;<br />
&amp;lt;Redirect method=&amp;quot;GET&amp;quot;&amp;gt;voice.php&amp;lt;/Redirect&amp;gt;<br />
&amp;lt;/Response&amp;gt;</p>
<p>END;<br />
?&amp;gt;<br />
[/php]</p>
<p>Now, we pull an XML file listing the contents of the bucket, then pick one from our array Contents.</p>
<p>Here is an older version, made in python for Google App Engine<br />
[python title="main.py"]<br />
from google.appengine.ext import webapp<br />
from google.appengine.ext.webapp import util<br />
import twilio<br />
from random import choice</p>
<p>SMS_MAX = 155</p>
<p>class MainHandler(webapp.RequestHandler):<br />
    def get(self):<br />
        f = open('deepthoughts.txt', 'r')<br />
        data = f.readlines()<br />
        f.close()<br />
        deepThought = choice(data).replace(&amp;quot;n&amp;quot;, &amp;quot;&amp;quot;)</p>
<p>        r = twilio.Response()<br />
        for i in range(0, len(deepThought) / SMS_MAX + 1):<br />
            chunkStart = i * SMS_MAX<br />
            chunkEnd = chunkStart + SMS_MAX<br />
            messageNumber = &amp;quot;&amp;quot;<br />
            if(len(deepThought) &amp;gt; SMS_MAX): messageNumber = `i+1` + &amp;quot;/&amp;quot; + `len(deepThought)/SMS_MAX+1` + &amp;quot; &amp;quot;<br />
            r.addSms(messageNumber + deepThought[chunkStart:chunkEnd])<br />
        self.response.out.write(r)</p>
<p>def main():<br />
    application = webapp.WSGIApplication([('/', MainHandler)],<br />
                                         debug=True)<br />
    util.run_wsgi_app(application)</p>
<p>if __name__ == '__main__':<br />
    main()<br />
[/python]</p>
<p>For more information, watch my screencast for the same system in Python</p>
<p><iframe width="640" height="360" src="http://www.youtube-nocookie.com/embed/TTo4E4WuK2E" frameborder="0" allowfullscreen></iframe></p>
