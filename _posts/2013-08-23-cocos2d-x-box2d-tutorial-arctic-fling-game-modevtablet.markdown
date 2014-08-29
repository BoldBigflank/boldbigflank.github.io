---
layout: post
status: publish
published: true
title: Cocos2d-x Box2D Tutorial - Arctic Fling Game - MoDevTablet
author:
  display_name: alex
  login: alex
  email: alex@bold-it.com
  url: ''
author_login: alex
author_email: alex@bold-it.com
excerpt: "Here's a Cocos2d-x Box2D tutorial on how to make a physics-based game we've
  dubbed Arctic Fling.  Throw fish at the opposing penguin to knock them over.  You
  can see the completed project on <a href=\"https://github.com/BoldBigflank/arctic-fling\"
  target=\"_blank\">GitHub</a>\r\n\r\n<a href=\"http://bold-it.com/wp-content/uploads/2013/08/2013-08-23-15.06.23.png\"><img
  src=\"http://bold-it.com/wp-content/uploads/2013/08/2013-08-23-15.06.23.png\" alt=\"2013-08-23
  15.06.23\" width=\"1024\" height=\"768\" class=\"alignnone size-full wp-image-342\"
  /></a>\r\n"
wordpress_id: 336
wordpress_url: http://bold-it.com/?p=336
date: '2013-08-23 22:17:31 -0700'
date_gmt: '2013-08-23 22:17:31 -0700'
categories:
- Cocos2d
- iOS
- Cocos2d-x
- Box2D
- Game
tags: []
comments: []
---
<p>Here's a Cocos2d-x Box2D tutorial on how to make a physics-based game we've dubbed Arctic Fling.  Throw fish at the opposing penguin to knock them over.  You can see the completed project on <a href="https://github.com/BoldBigflank/arctic-fling" target="_blank">GitHub</a></p>
<p><a href="http://bold-it.com/wp-content/uploads/2013/08/2013-08-23-15.06.23.png"><img src="http://bold-it.com/wp-content/uploads/2013/08/2013-08-23-15.06.23.png" alt="2013-08-23 15.06.23" width="1024" height="768" class="alignnone size-full wp-image-342" /></a></p>
<p>Here are the steps we'll take to create this game.</p>
<ul>
<li>Create a Cocos2D-x project with Box2D</li>
<li>Create the artwork and Box2D Shapes</li>
<li>Change touches to throw fish</li>
<li>Place bases using friction joints</li>
<li>Use a Contact Listener to determine collision behavior</li>
<li>End the game</li>
<li>Delete unneeded fish</li>
</ul>
<h1>Create a Cocos2d-x Project With Box2D</h1>
<p>I used the Cocos2d-x Git repo using the install_xcode_templates.sh script, then in XCode created a Cocos2d-x with Box2D project.</p>
<h1>Create the Artwork and Box2D Shapes</h1>
<p>The fastest way I've found to set up Box2D shapes is to use <a href="http://www.codeandweb.com/physicseditor/" target="_blank">Physics Editor</a> application. There are a few things to make these work well in our project:</p>
<ul>
<li>Change the Exporter to Box2D generic (PLIST)</li>
<li>Change the PTM-Ratio to match your Project (it's probably 32.0)</li>
<li>Set your anchor points to Relative 0.5/0.5</li>
<li>Density, Restitution and Friction can be different based on your preferences. I usually kept the base's density twice what the fish's was, and made the fish's restitution was generally 0.2. More restitution means more bouncy.</li>
</ul>
<p>I've provided the graphics, shapes and plist I used as an example.  The art was lovingly created by <a href="https://twitter.com/dianaphamhere">Diana Pham</a> (<a href="https://github.com/dianapham">GitHub</a>)(<a href="http://www.linkedin.com/in/dianaphamhere">LinkedIn</a>)  . Feel free to try out different options to see what changes. <a href="http://bold-it.com/wp-content/uploads/2013/08/Resources.zip">Get them here.</a></p>
<p><a href="http://bold-it.com/wp-content/uploads/2013/08/BR5JZSBCMAAFHZK.jpg"><img src="http://bold-it.com/wp-content/uploads/2013/08/BR5JZSBCMAAFHZK.jpg" alt="We made a great team." width="1024" height="768" class="alignnone size-full wp-image-348" /></a></p>
<h1>Change Touches to Throw Fish</h1>
<p>The first thing we’re going to do is change the addNewSpriteAtPosition method to include a name and velocity, as well as change the method to use our Physics Editor created shapes. In HelloWorldScene.h, change the addNewSpriteAtPosition to this:<br />
[cpp]b2Body * addNewSpriteAtPosition(string name, cocos2d::CCPoint p, cocos2d::CCPoint velocity);<br />
[/cpp]</p>
<p>Add these two helper files to your Classes directory, and add them to your XCode project<br />
<a href=”https://raw.github.com/AndreasLoew/PhysicsEditor-Cocos2d-x-Box2d/master/Demo/generic-box2d-plist/GB2ShapeCache-x.cpp”>GB2ShapeCache-x.cpp</a><br />
<a href=”https://raw.github.com/AndreasLoew/PhysicsEditor-Cocos2d-x-Box2d/master/Demo/generic-box2d-plist/GB2ShapeCache-x.h”>GB2ShapeCache-x.h</a></p>
<p>Also in HelloWorldScene.cpp, add it to your includes<br />
[cpp]#include &quot;GB2ShapeCache-x.h&quot;[/cpp]</p>
<p>And load the shape cache.  At the top of HelloWorld::HelloWorld(), add this<br />
[cpp]<br />
    GB2ShapeCache *sc = GB2ShapeCache::sharedGB2ShapeCache();<br />
    sc-&gt;addShapesWithFile(&quot;shapes.plist&quot;);<br />
[/cpp]</p>
<p>[cpp]<br />
b2Body* HelloWorld::addNewSpriteAtPosition(string name, CCPoint p, CCPoint velocity)<br />
{<br />
    CCLOG(&quot;Add sprite %0.2f x %02.f&quot;,p.x,p.y);</p>
<p>    // Create a sprite<br />
    CCSprite *sprite = CCSprite::create((name+&quot;.png&quot;).c_str());</p>
<p>    sprite-&gt;setPosition(p);</p>
<p>    addChild(sprite);</p>
<p>    // Create the Box2D body<br />
	b2BodyDef bodyDef;<br />
	bodyDef.type = b2_dynamicBody;<br />
    bodyDef.angle = ccpToAngle(velocity);<br />
	bodyDef.position.Set(p.x/PTM_RATIO, p.y/PTM_RATIO);<br />
	bodyDef.userData = sprite;<br />
	b2Body *body = world-&gt;CreateBody(&amp;bodyDef);</p>
<p>    // add the fixture definitions to the body</p>
<p>    GB2ShapeCache *sc = GB2ShapeCache::sharedGB2ShapeCache();<br />
    sc-&gt;addFixturesToBody(body, name.c_str());<br />
    sprite-&gt;setAnchorPoint(sc-&gt;anchorPointForShape(name.c_str()));</p>
<p>    // Set them in motion<br />
    b2Vec2 f = 6.0 * b2Vec2(velocity.x, velocity.y); // 6.0 is just to make it more powerful<br />
    body-&gt;ApplyForceToCenter(f);</p>
<p>    return body;<br />
}</p>
<p>[/cpp]</p>
<p>In HelloWorldScene.h, add the following public method:</p>
<p>[cpp]virtual void ccTouchesEnded(cocos2d::CCSet* touches, cocos2d::CCEvent* event);[/cpp]<br />
This means we're going to be defining this method in our class.</p>
<p>In HelloWorldScene.cpp, add the following:<br />
[cpp]<br />
string names[] = {<br />
    &quot;fishPink&quot;,<br />
    &quot;fishPurple&quot;,<br />
    &quot;fishBlue&quot;,<br />
    &quot;fishYellow&quot;,<br />
    &quot;fishOrange&quot;,<br />
    &quot;fishRed&quot;,<br />
    &quot;fishGreen&quot;<br />
};</p>
<p>void HelloWorld::ccTouchesEnded(CCSet* touches, CCEvent* event)<br />
{<br />
    if(!gameInProgress) return; // Ignore input when game is ended</p>
<p>    //Add a new body/atlas sprite at the touched location<br />
    CCSetIterator it;<br />
    CCTouch* touch;</p>
<p>    for( it = touches-&gt;begin(); it != touches-&gt;end(); it++)<br />
    {<br />
        touch = (CCTouch*)(*it);</p>
<p>        if(!touch)<br />
            break;</p>
<p>        CCPoint location = touch-&gt;getLocationInView();<br />
        CCPoint startLocation = touch-&gt;getStartLocationInView();</p>
<p>        CCPoint velocity = ccpSub(touch-&gt;getLocationInView(), touch-&gt;getStartLocationInView());<br />
        velocity = CCPointMake(velocity.x, -1.0* velocity.y);<br />
        startLocation = CCDirector::sharedDirector()-&gt;convertToGL(startLocation);<br />
        location = CCDirector::sharedDirector()-&gt;convertToGL(location);</p>
<p>        CCSize s = CCDirector::sharedDirector()-&gt;getWinSize();</p>
<p>        string spriteName = names[rand()%7];</p>
<p>        b2Body * blast = addNewSpriteAtPosition( spriteName, location, velocity );<br />
        blast-&gt;SetAngularVelocity( (rand() % 6) - 3);<br />
        CCSprite * blastSprite = (CCSprite *)blast-&gt;GetUserData();<br />
        // Left side 3, right side 4<br />
        blastSprite-&gt;setTag(( startLocation.x &lt; s.width/2 ) ? 3:4);<br />
    }<br />
}<br />
[/cpp]</p>
<p>Right now, we have the sprite being created at the location the touch ended, and in the direction the touch moved.  This is like a flick action.  You could change these around however you like, such as make them go the opposite direction, like a slingshot.  You could also start the sprite at the beginning touch spot. Try things out!</p>
<p>You can also adjust the gravity to your liking in the initPhysics() function. I've set mine to<br />
[cpp]gravity.Set(0.0f, -4.0f);[/cpp]</p>
<h2>(iOS Only) Allow Multitouch</h2>
<p>In the AppController.mm, right after *__glView is defined (about line 39) add the following:<br />
[cpp]__glView.multipleTouchEnabled = true;[/cpp]</p>
<p>If you forget this, there might be some strange behavior when you have two people flinging fish at the same time.</p>
<h1>Place Bases Using Friction Joints</h1>
<p>Normally, physics object have no rotational friction, which means when they start spinning they will keep going until something stops them. We want to add a little challenge to our game, so we want the bases to stop spinning after each hit.  We’re going to define a max torque variable here. At the top of HelloWorldScene.cpp, near your other define statement, add this:<br />
[cpp]<br />
#define BASE_MAX_TORQUE 30<br />
[/cpp]<br />
In HelloWorld::HelloWorld(), remove code specific to the demo.  After this->initPhysics(); add this<br />
[cpp]<br />
// Base 1<br />
    base1 = addNewSpriteAtPosition(&quot;fullModel&quot;, ccp(s.width/4.0, s.height/2), CCPointZero);<br />
    CCSprite * base1Sprite = (CCSprite*)base1-&gt;GetUserData();<br />
    base1Sprite-&gt;setTag(1);</p>
<p>    // -Friction<br />
    b2FrictionJointDef base1Friction;<br />
    base1Friction.Initialize(base1, groundBody, base1-&gt;GetWorldCenter());<br />
    base1Friction.maxTorque = BASE_MAX_TORQUE;<br />
    base1Friction.collideConnected = true;<br />
    world-&gt;CreateJoint(&amp;base1Friction);</p>
<p>    // -Pivot<br />
    b2RevoluteJointDef base1JointDef;<br />
    base1JointDef.Initialize(base1, groundBody, base1-&gt;GetWorldCenter());<br />
    world-&gt;CreateJoint(&amp;base1JointDef);</p>
<p>    // Base 2<br />
    base2 = addNewSpriteAtPosition(&quot;fullModel-right&quot;, ccp(3.0*s.width/4.0, s.height/2), CCPointZero);<br />
    CCSprite * base2Sprite = (CCSprite*)base2-&gt;GetUserData();<br />
    base2Sprite-&gt;setTag(2);</p>
<p>    // -Friction<br />
    b2FrictionJointDef base2Friction;<br />
    base2Friction.Initialize(base2, groundBody, base2-&gt;GetWorldCenter());<br />
    base2Friction.maxTorque = BASE_MAX_TORQUE;<br />
    base2Friction.collideConnected = true;<br />
    world-&gt;CreateJoint(&amp;base2Friction);</p>
<p>    // -Pivot<br />
    b2RevoluteJointDef base2JointDef;<br />
    base2JointDef.Initialize(base2, groundBody, base2-&gt;GetWorldCenter());<br />
    world-&gt;CreateJoint(&amp;base2JointDef);<br />
[/cpp]</p>
<p>There, now our bases are fixed to a specific point on the screen, and will only spin a little when hit by fish. </p>
<h1>Determine a Winner</h1>
<p>Define the angle you want for the winner to be set<br />
[cpp]<br />
#define MAX_ANGLE (M_PI / 3.0)<br />
[/cpp]<br />
This will make it Pi/3, or roughly 60 degrees.</p>
<p>Also create a variable to know when the game is over, and a label to display who has won<br />
In HelloWorldScene.h, add a private variable:<br />
[cpp]<br />
bool gameInProgress;<br />
CCLabelTTF *label;</p>
<p>[/cpp]<br />
In HelloWorldScene.cpp, in the HelloWorld() function, add<br />
[cpp]<br />
    gameInProgress = true;<br />
    label = CCLabelTTF::create(&quot;Arctic Fling&quot;, &quot;Marker Felt&quot;, 32);<br />
    addChild(label, 0);<br />
    label-&gt;setColor(ccc3(0,0,255));<br />
    label-&gt;setPosition(ccp( s.width/2, s.height-50));</p>
<p>[/cpp]</p>
<p>We can ignore touches once the game has ended. At the top of ccTouchesEnded, add<br />
[cpp]<br />
if(!gameInProgress) return; // Ignore input when game is ended<br />
[/cpp]</p>
<p>Then in the update() function, add this to the bottom<br />
[cpp]<br />
    if(gameInProgress){<br />
        // Check for game winning conditions<br />
        if( base1-&gt;GetAngle() &gt; MAX_ANGLE || base1-&gt;GetAngle() &lt; -1.0 * MAX_ANGLE ){<br />
            // Base 2 wins<br />
            label-&gt;setString(&quot;Player 2 Wins&quot;);<br />
            // Unhook penguin 1 from the base</p>
<p>            // Show new game button<br />
            gameInProgress = false;</p>
<p>        };</p>
<p>        if(base2-&gt;GetAngle() &gt; MAX_ANGLE || base2-&gt;GetAngle() &lt; -1.0 * MAX_ANGLE){<br />
            // Base 2 wins<br />
            label-&gt;setString(&quot;Player 1 Wins&quot;);<br />
            // Unhook penguin 2 from the base</p>
<p>            // Show new game button<br />
            gameInProgress = false;<br />
        };</p>
<p>    }</p>
<p>[/cpp]<br />
This will check the angle of the base each time and end the game when the winner is determined.</p>
<h1>Delete Unneeded Fish</h1>
<p>You'll notice that the fish end up piling up at the bottom of the screen. We should get rid of fish that fall to the bottom, or fish that are created on top of our own base.<br />
This will be added to the tutorial soon.  This involves creating a Contact Listener class, tagging sprites and deleting the right sprites.</p>
