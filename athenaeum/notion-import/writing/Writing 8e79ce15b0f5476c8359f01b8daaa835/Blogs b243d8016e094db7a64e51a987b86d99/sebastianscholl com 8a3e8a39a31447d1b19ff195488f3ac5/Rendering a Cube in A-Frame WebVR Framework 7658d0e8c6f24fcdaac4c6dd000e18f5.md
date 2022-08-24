# Rendering a Cube in A-Frame WebVR Framework

Created: August 25, 2021 12:16 PM
Location: New York City, United State of America
Original Publish Date: April 8, 2016
Tags: Tech & Code

Several weeks ago a colleague and I decided it would be worth our combined efforts to begin exploring virtual reality as developers. Slowly, we've begun patching together a curriculum of sorts that should ready us to tackle several passion projects in the near future. Being that there is limited learning material on VR available (relative to other technologies), I hope that logging my own trials, tribulations, and successes may leave a meaningful paper trail for those after me.

# **A-Frame:**

A-frame is an abstraction of the three.js library. A framework developed by Mozilla's VR team to enable Web based virtual reality experiences in an extremely accessible way. After spending last week dirtying my hands working directly with three.js, it quickly became apparent that taking a step back as to engage with A-frame would provide much needed training wheels.

Why go for the training wheels? Well, a virtual reality environment is a whole different beast from what most people - developers and users - are used to. We live in the 3rd dimension, so it is easy for us to look at and absorb a 2nd dimension environment (a plane). However, in virtual reality we recreate the 3rd dimension with a screen being our new eyes - meaning that instead of creating a 2D plane to be observed, we are creating a 3D environment that we will be within! In order to do that, there’s a whole slew of new variables that we as developers must take into consideration. And using a framework like A-frame allows you to focus less on complex code and more on internalizing 3D concepts. And at the same time there is still very little that you cannot do using A-frame!

# **Setting up A-Frame:**

Mozilla’s VR states that their “goal is to help bring high-performance virtual reality to the open web”. In pursuit of that goal, they’ve made setting up A-frame unbelievably simple. Simply include a script tag in the head of a html page to be rendered in a browser and include A-frame’s minified CDN as so:

There are several other ways to go about it, whether that’s starting out by playing in codepen.io or leveraging npm. However doing it this way is a quick path to accessing the library.

Take the following code and copy it into a new html document. After doing so, open up in your browser (use Chrome or Firefox):

```html
<!DOCTYPE html>
<html>
<head>
    <title></title>
		<script src="https://aframe.io/releases/latest/aframe.min.js"></script>
</head>
	<body>
	<a-scene>
	  <a-entity geometry="primitive: box; width: 2; height: 2; depth: 2"></a-entity>
	</a-scene>
	</body>
</html>
```

Congrats! You’ve render you first (maybe) cube in a virtual reality web environment. Later on I’ll get into the actual Javascript that’s being executed behind A-frame here. However, feel free to play around with the a-entity’s attributes to see how it affects the cube, as well as Google “a-frame a-entity geometry”.

![https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-12-28-57-am.png](https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-08-at-12-28-57-am.png)