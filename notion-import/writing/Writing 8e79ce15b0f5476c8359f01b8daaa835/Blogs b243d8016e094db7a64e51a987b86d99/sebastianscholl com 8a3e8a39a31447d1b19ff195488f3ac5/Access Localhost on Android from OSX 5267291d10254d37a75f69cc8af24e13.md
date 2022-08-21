# Access Localhost on Android from OSX

Created: August 25, 2021 12:23 PM
Location: New York City, United State of America
Original Publish Date: April 13, 2016
Tags: Tech & Code

Web developers will often want to view their projects on mobile. In both Chrome and Firefox, the developer console gives us the ability to mimic mobile views by setting screen size containers. It's really not a comparable experience though to holding a phone while demoing.

The following guide is a trick that can be used to access a localhost server - hosted on a Mac - from an Android mobile device. Having a Samsung phone myself, it's how I've been testing WebVR experiences I build for Google Cardboard without being tethered. Reach out with any questions should there be a step that's unclear - or better way to do it!

# **Guide:**

First off, both your phone and laptop must be connected to the same WiFi network. If you're using your phones mobile hotspot, it will still work. However, make sure to connect both devices to the same network before moving forward.

Next, collect your phones IP address. To do so, I use the Network Info II app. There is most definitely another way to accomplish this. However, Network Info II works as needed and is document for this tutorials sake. Reference the screen shot below for what number to collect - the last listed IP: sectioned under **`rmnet_data1`.**

![https://mynamessebastian.files.wordpress.com/2016/04/phoneinet.png](https://mynamessebastian.files.wordpress.com/2016/04/phoneinet.png)

Now open the terminal on your computer (don't worry about which directory you're within) and run the command **sudo nano /etc/hosts/**. After entering your system password, you'll see near the top of the terminal a string of numbers with the word **localhost** following. Localhost is in fact just a loopback to your own computer's so that when you go to localhost in a browser it simply routes the http request to your local machine. In order to tie your phone into this loop, enter its IP address right between the string of numbers and Localhost - reference the screen shot below for a visual.

### **BEFORE**

![https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-11-33-09-am.png](https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-11-33-09-am.png)

### **AFTER:**

![https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-11-36-00-am.png](https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-11-36-00-am.png)

To save this, hit **control + X** and then **Y** when prompted to save. After that, the **enter key** will bring you back to the standard command line.

Open a second tab in the terminal and launch a local server. I've only tested this using a simple python server, which can be run by running in the terminal **`python -m SimpleHTTPServer 8000`**. However, I'm assuming that you can launch any local server you like, being that all you'll need to reference is the port number. If you do use the simple python server, that port number is 8000.

Run **ifconfig** in the terminal. This will bring up a slew of information, to which you should scroll about halfway down. What you are looking for is a string of numbers that follow after an **inet** and before **netmask** within either the **en0:** or **en1:** key. In the screenshot below, you would be looking for **192.168.3.100.**

![https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-1-05-21-pm.png](https://mynamessebastian.files.wordpress.com/2016/04/screen-shot-2016-04-13-at-1-05-21-pm.png)

Done! On your Android, open up a browser and visit the **inet** number, followed by a colon (**:)** and the port number. An example can be seen in the screenshot below.

![https://mynamessebastian.files.wordpress.com/2016/04/screenshot_20160413-131348.png](https://mynamessebastian.files.wordpress.com/2016/04/screenshot_20160413-131348.png)