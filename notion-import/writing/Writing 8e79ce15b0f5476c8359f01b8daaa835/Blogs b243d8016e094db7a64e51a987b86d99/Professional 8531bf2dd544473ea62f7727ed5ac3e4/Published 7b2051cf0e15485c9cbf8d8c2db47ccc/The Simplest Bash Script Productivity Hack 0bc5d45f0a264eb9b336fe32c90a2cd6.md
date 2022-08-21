# The Simplest Bash Script Productivity Hack

**This article was inspired by laziness.*

**The problem**

A part of my daily workflow is participating in forums. Every morning I read through Hacker News, 8base Community, several different subreddits, StackOverflow, and a few others for an hour. It’s how I like to engage with developers.

There is something simply tedious about this morning routine. Remember each community forum to visit is a slog. I end up always leaving a dozen or more tabs open in Chrome browser; my computer battery’s lifespan reduces to that of a gnat.

For a hot-second, I became all excited about finding some tab manager. After that second, I decided that the last thing I wanted was **another** app/extension in my life. So, I asked myself…

“What’s the most simple solution to track and open my forums every morning?”

**The solution**

After some brain-storming – a light rain, at best – I decided that I’d try to employ a Bash script. 2-minutes later everything worked; seriously, it was that simple.

Here’s what I did. Start by opening your terminal and running the following commands – or using equivalents.

```shell

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

"https://community.8base.com/"

"https://www.reddit.com/r/graphql/"

"https://www.reddit.com/r/webdev/"

"https://news.ycombinator.com/"

"https://stackoverflow.com/questions/tagged/firebase?tab=Newest"

"https://stackoverflow.com/search?tab=newest&q=graphql"

"https://stackoverflow.com/search?tab=newest&q=vue"

"https://github.com/8base/Documentation/issues"

)

# Open links in the list.

for i in "${links[@]}"

do

open "$i"

done

wait;

```

I’d be hard-pressed to find a more expressive script. However, lets quickly run through what’s happening.

The `links` variable stores an array of URLs – at any time, add or remove URLs relevant to you. The `for` loop iterates over the `links` array, where each URL is passed as an argument to the `open` command.

Save the script and hop back into your terminal. The `launcher.sh` file needs execution permissions. We can grant that using the following `chmod` command.

```shell
chmod +x launcher.sh

```

Sweet! That’s it. Double-click the `launcher.sh` file on your Desktop and all your tabs will appear.

**The Decoration**

There is one glaring issue that must be mitigated. This script looks UhhhGLY on our home screen! Let’s improve that.

I found [this newspaper emoji icon](https://www.google.com/search?biw=1438&bih=744&tbm=isch&sa=1&ei=mwiuXcGCIajc5gKSvprIBQ&q=emoji+newspaper&oq=emoji+new&gs_l=img.3.1.0l10.23737.25343..28407...0.0..0.111.602.8j1......0....1..gws-wiz-img.......0i67j0i131.230QlpydfW0#imgrc=yx5qmw_ZCaWm-M:) on Google Images. Simply right-click it in the browser and select “Copy Image”. Now, right-click the` launcher.sh` file and open the “Get Info” pane. In the top-left, select the file icon so that it highlights and press `[CMD] + V` to paste it.

Rename the file to whatever you’d like; it’s fine to remove the `.sh` file extension.

**All Done**

The file should look like a native desktop app at this point! Double-click it and all specified URLs will open in your default browser. If you need to update the URLs, simply open it in a text editor.

That’s it.