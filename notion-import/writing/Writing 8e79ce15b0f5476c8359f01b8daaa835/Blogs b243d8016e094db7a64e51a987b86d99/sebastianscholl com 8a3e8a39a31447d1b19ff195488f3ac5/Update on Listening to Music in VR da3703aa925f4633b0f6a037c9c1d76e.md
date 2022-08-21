# Update on Listening to Music in VR

Created: August 25, 2021 12:25 PM
Location: New York City, United State of America
Original Publish Date: April 24, 2016
Tags: Tech & Code

*If you missed it, check out my first demo of [Koo-VR at this link](https://mynamessebastian.com/2016/04/10/virtual-reality-music-player-visualizing-spotifys-api/)*

Since my last article where I demod a music player for virtual reality I've re-engineered the application in a way I'm very excited about. Why am I excited? Well, two reasons. The first is that it is now built with Angular and published to the web. And the second is that I've not been able to find any examples of WebVR experiences being built with Angular!

The usual static HTML web pages that we often visit are not dynamic enough for virtual reality. When building experiences for the web though, HTML is what we must end up with for it to be rendered in our browsers. A framework like Angular allows us to extend the common HTML vocabulary in an application structure that is both light and easily packaged - enabling the creation of web experiences that are extremely responsive and expressive.

Imagine that you design a room in virtual reality where there is a table in the center. Normally, if I wanted to add anything to that scene - say, a glass of water - I'd have to reload the scene entirely to add the new element (something like Ajax *could* be used, but that would be difficult to maintain as any complexity develops). This is a huge issue from an UX point of view, because the introduction of any new element would be an interruption to the immersion.

In my case, this issue came about when loading in and visualizing albums covers. By using Angular, I was able to have the user cause an event, my *service* call Spotify, the *controller* add the response to *scope*, and then render each album in the scene, all without ever having to reloading - or more importantly, without the experience being interrupted.

Check out the project to-date by clicking the link below. Please pardon bugs...if you find them!

---

***[Koo-VR Music Player](https://young-refuge-92841.herokuapp.com/)***

---