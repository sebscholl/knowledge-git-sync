**Date:** [[2021-08-29]]
**Tags:** #code #productvity #medium

# A Simple Productivity Hack Using Bash Scripts

Created: August 29, 2021 1:45 PM
Location: Miami, United State of America
Original Publish Date: November 20, 2019
Tags: Tech & Code

### **How to expedite workflows by launching browser tabs from bash scripts.**

![https://cdn-images-1.medium.com/max/2560/1*7cljyjXZ6eyzfZGXu_m_IA.png](https://cdn-images-1.medium.com/max/2560/1*7cljyjXZ6eyzfZGXu_m_IA.png)

### **The problem**

A part of my daily workflow is participating in forums. Every morning I read through Hacker News, 8base Community, several different subreddits, StackOverflow, and a few others for an hour. It’s how I like to engage with developers.

There is something merely tedious about this morning routine. Remembering each community forum to visit is a slog. I end up always leaving a dozen or more tabs open in Chrome browser; my computer battery’s lifespan reduces to that of a gnat.

For a hot-second, I became all excited about finding some tab manager. Once that second cooled, I decided that the last thing I wanted was **another** app/extension in my life. So, I asked myself…

> “What’s the most simple solution to track and open my forums every morning?”
> 

### **The solution**

After some brain-storming — a light rain, at best — I decided that I’d try to employ a Bash script. 2-minutes later, everything worked; seriously, it was that simple. Here’s what I did.

Start by opening your terminal and running the following commands — or using equivalents.

```bash
# Move to the Desktop directory
cd ~/Desktop

# Create a new bash script
touch launcher.sh

# Open the script in a text editor
code launcher.sh
```

With the bash script open, copy and paste the following code into the file.

```bash
#!/bin/bash

# Keep a list of links.
links=(
 “https://community.8base.com/"
 “https://www.reddit.com/r/graphql/"
 “https://news.ycombinator.com/"
 “https://github.com/8base"
)

# Open links in the list.
for i in “${links[@]}”
do
 open “$i”
done

wait;
```

I’d be hard-pressed to find a more expressive script. However, lets quickly talk through what’s happening.

The `links` variable stores an array of URLs. The `for` loop iterates over each URL in `links` and passes it as an argument to the `open` command to launch a new tab in your default browser.

Save the script and hop back into your terminal. The `launcher.sh` file needs execution permissions. We can grant that using the following `chmod` command.

```bash
chmod +x launcher.sh
```

Sweet! That’s it. Double-click the `launcher.sh` file from your Desktop and all your tabs will appear.

### **The Decoration**

There is one glaring issue that must be mitigated. This script looks UhhhGLY on our home screen! Let’s improve that.

I found [this newspaper emoji icon](https://www.google.com/search?biw=1438&bih=744&tbm=isch&sa=1&ei=mwiuXcGCIajc5gKSvprIBQ&q=emoji+newspaper&oq=emoji+new&gs_l=img.3.1.0l10.23737.25343..28407...0.0..0.111.602.8j1......0....1..gws-wiz-img.......0i67j0i131.230QlpydfW0#imgrc=yx5qmw_ZCaWm-M:) on Google Images. Simply right-click it in the browser and select “Copy Image.” Now, right-click the `launcher.sh` file and open the “Get Info” pane. In the top-left, select the file icon so that it highlights and press `[CMD] + V` to paste it.‍

![https://cdn-images-1.medium.com/max/800/0*mwyl7Brj6k4nm9Ut.png](https://cdn-images-1.medium.com/max/800/0*mwyl7Brj6k4nm9Ut.png)

Rename the file to whatever you’d like; it’s fine to remove the `.sh` file extension.

### **The End**

The file should look like a native desktop app at this point! Double-click it, and all specified URLs will open in your default browser. If you need to update the URLs, simply do so in a text editor. What I’ve begun to do is duplicate these scripts for different workflows (i.e. `Forums Launcher`, `News Launcher`, `Debugging Launcher`).‍

---