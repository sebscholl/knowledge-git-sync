# Virtual Reality Music Player

Created: August 25, 2021 12:19 PM
Location: New York City, United State of America
Original Publish Date: April 10, 2016
Tags: Tech & Code

For the past week, a friend ([Holly Peck](http://blog.holly-peck.com/)) and I have spent our leisure time building a virtual reality music player. This is the first demo we have to show - please feel free to give feedback as well as contribute to the [code's repository](https://github.com/sebscholl/koo-vr/tree/master/a-frame-playlister)!

[https://www.youtube.com/watch?v=4KuF1pX_omI&w=560&h=315](https://www.youtube.com/watch?v=4KuF1pX_omI&w=560&h=315)

The project uses A-Frame. You'll notice that the video is split-screen. This is because it was a screen capture on my Galaxy S6 when being held in a Google Cardboard type headset. When wearing the headset, your eyes naturally merge both images and simple glass lenses correct for some of the distortion. The screen's center point follows your heads movement, meaning that the screens cursor follows ones direct line of vision.

Using Spotify's API, we make an AJAX call to get the album images and mp3 track previews. This all comes back as JSON data that we're able to iterate over using JQuery or Javascript, format into A-Frame entities, and append to the DOM. Positioning is dynamic depending on how many tracks are being returned, meaning that tracks will always face and be evenly distributed in a circle around the user.

Playing and pausing tracks are initiated by `.mouseenter()` and `.mouseleave()` events, which can best be compared to a hover event. A very cool part of A-Frame's sound attribute is that it is spatially aware and emanates sounds from the entities themselves which hold them. Therefore, volume con be "controlled" in two ways. The first way is of course by using ones volume controls, and the second is by the distance between you and an object within a scene.

Lastly, the scene itself was created simply by using A-Frame's `<a-sky>`, `<a-plane>`, and `<a-sphere>` elements. Together, with added textures and spacial properties, they made up the moon, sky and ground. When wearing a headset we don't have controls to navigate a scene. However, on a desktop we are able to use WASD controls to navigate a scene much like a video game.