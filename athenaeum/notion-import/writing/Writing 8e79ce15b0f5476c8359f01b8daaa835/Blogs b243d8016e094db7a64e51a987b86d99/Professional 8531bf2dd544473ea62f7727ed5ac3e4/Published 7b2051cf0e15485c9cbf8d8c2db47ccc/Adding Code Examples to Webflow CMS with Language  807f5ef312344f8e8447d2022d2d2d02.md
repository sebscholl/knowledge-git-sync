# Adding Code Examples to Webflow CMS with Language Highlighting_

# Adding Code Examples to Webflow CMS with Language Highlighting

Very recently the team at 8base decided to migrate our blog over from Medium to Webflow. If a bag-of-words analysis were run on transcripts from conversations we had around why to do this, the primary representation would encompass SEO and related jargon. Nevertheless, our lead designer has since poured many hours into building a beautiful new blog on Webflow - as well as migrated every published post over to their CMS.

‍

‍

Only once all the work was done did we realize that Webflow CMS has no support for code blocks 🤦

‍

‍

This wasn't trivial for us. As we're gearing up for the launch our new 8base Tutorials project (coming soon!) and often publishing blogs that demonstrate - with code - all the awesome things you can do on 8base, displaying properly formatted code both in-line and as blocks is a must. Hopefully, Webflow is going to give some special attention to the CMS after its latest and most significant round of funding. Every other aspect of their product either flirts with or embodies awesomeness. So why would we anticipate anything less for the CMS?

‍

That said, we had to come up with another solution in the meantime. Moreover, as is the case with most problems, they're rarely unique to the person experiencing them! A quick search on the interwebs, and you'll find a blog post on daily detailing the same problem and proposing a solution. With all due respect deserved to the author, his solution wasn't one we felt comfortable using.

‍

[Untitled](Adding%20Code%20Examples%20to%20Webflow%20CMS%20with%20Language%20%20807f5ef312344f8e8447d2022d2d2d02/Untitled%20Database%20cce4fd1d3ee04147800c81b07dc7e5bf.csv)

‍

### Defining Custom Tags

I'll keep this explanation short and sweet, in the spirit of the solution itself! To have the examples render in *this* post, I used alternative tag-names. That said, the formatted code blocks that you do see here are what you could expect were you to implement the suggestions yourself.

‍

Firstly, we defined two simple custom tags. The tags are an ERB + HTML style mash-up that allows for the easy denotation for when a code example starts and ends. Originally, we attempted at using HTML style tags (<>). However, they were being escaped and just led to a messier script.

‍

### **Code In-line**

[Untitled](Adding%20Code%20Examples%20to%20Webflow%20CMS%20with%20Language%20%20807f5ef312344f8e8447d2022d2d2d02/Untitled%20Database%20a11f160f8cd44bc1bb10642f4bb9d71f.csv)

‍

### **Code block**

[Untitled](Adding%20Code%20Examples%20to%20Webflow%20CMS%20with%20Language%20%20807f5ef312344f8e8447d2022d2d2d02/Untitled%20Database%20412f945320f545c6b7d6ab54db7f9d9c.csv)

‍

### Adding Highlight.js

Many solutions advised using [Prism](https://prismjs.com/) for syntax highlighting. Reading through their docs, it just felt like overkill. So instead, we landed on [Highlight.js](https://highlightjs.org/). What's great about Highlight.js is that it allows you to style code to reflect a preferred text editor theme easily. Meaning that if you're a fan of Sublime Text 3 or Atom, code samples can be highlighted using editor themes.

So, we added the following inside our Blog Post Template <head>...</head> tag. The *script* tag loads the Highlight.js library and the first *link* tag imports syntax highlighted CSS styling for all supported languages while the second one imports the [Atom One Light](https://highlightjs.org/static/demo/) editor theme.

‍

[Untitled](Adding%20Code%20Examples%20to%20Webflow%20CMS%20with%20Language%20%20807f5ef312344f8e8447d2022d2d2d02/Untitled%20Database%20f582f4deb9514596bff76f774e8f2772.csv)

### Writing the Script

By default, Webflow requires jQuery and makes it available globally. This allows us to use it in any custom script that we choose to add to our page templates. Naturally, the same thing could be accomplished using Vanilla JS. However, using jQuery felt just a bit tidier.

‍

[Untitled](Adding%20Code%20Examples%20to%20Webflow%20CMS%20with%20Language%20%20807f5ef312344f8e8447d2022d2d2d02/Untitled%20Database%20ec53a827db4d4382b6dbfb6f55863d74.csv)

‍

So, there are a couple of important things worth noting.

‍

1. The script executes on the $(document).ready() event.
2. The $("HTML_TAG:contains('CODE_TAG')") selectors return all DOM elements that contain the specified tag.
3. The Regex statement(s) match the custom opening and closing tags with proper HTML tags and preserve the language attribute - for the block - and all inner text.
4. Once the DOM is updated, the resulting code blocks are highlighted using the Highlight.js hljs.highlightBlock() function.

‍

We decided to forgo using syntax highlighting on the in-line examples. Instead, we added a custom *inline-code* class to the template that's independently styled. Additionally, we didn't like the extra space (**<br>** tag) that gets added to every code block. This is why we added the codeBlock.removeChild(block.childNodes[0]) line.

### **In Summary**

As soon as Webflow updates their CMS to support either Markdown or native code blocks, we'll likely scrap this solution that we just shared. That said, we're pretty happy with what we came up with for its the readability and maintainability!

‍

Feel welcome to use this strategy yourself and let us know how it works.

‍

‍

‍

‍