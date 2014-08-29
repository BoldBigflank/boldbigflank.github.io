---
layout: post
status: publish
published: true
title: Generate Map Tiles From Image
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
wordpress_id: 321
wordpress_url: http://bold-it.com/?p=321
date: '2013-06-18 08:58:25 -0700'
date_gmt: '2013-06-18 08:58:25 -0700'
categories:
- Python
tags: []
comments: []
---
<p>This Python script, <a href="https://gist.github.com/BoldBigflank/5803651">Image2Map.py</a>, will generate map tiles from images. The script accepts a png, jpeg or any PIL-compatible image.  I revisited it and noticed that it had some issues with the latest version of networkx, so I updated it. I tested this in Python 2.7.2 with networkx 1.7 and PIL installed.  Here's how you use <a href="https://gist.github.com/BoldBigflank/5803651">Image2Map.py</a>:</p>
<p><code>python Image2Map.py tileWidth tileHeight file</code><br />
For example:<br />
<code>python Image2Map.py 16 16 map.png</code></p>
<p>This goes hand in hand with <a href="https://github.com/JoeAnzalone/HTML5-Keen/blob/master/scripts/MapWriter.py" title="MapWriter.py" target="_blank">MapWriter.py</a>, which will allow you to create a Tiled TMX map from the two images, in this fashion:</p>
<p><code>python MapWriter.py 16 16 map.png map-Tileset.png</code></p>
<p><script src="https://gist.github.com/BoldBigflank/5803651.js"></script></p>
