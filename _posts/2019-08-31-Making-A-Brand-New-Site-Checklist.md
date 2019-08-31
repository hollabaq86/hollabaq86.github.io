---
author: xoxo Holla
---

_Making a Brand New Site from Scratch: A Checklist_

# Overview

Let's face it. Every now and then you find a little project you want to put on the internet. Maybe it's something silly, maybe it's something to help out a friend or family member. If you're like me and spend most of your working life _maintaining_ existing code, sometimes your brain just draws a total `"nothing"` when you need to start a website from the very beginning.

I'm making this checklist for myself so that hopefully it'll be easier for me the next time I need to do this. Hope it helps you, too:

- [] Make a new repo
- [] Consider the projects needs and find the simplest way to deploy. 
- [] Choose a framework that makes this deployment strategy _just as easy_
- [] Get your index route created
- [] Create `home.html` page:

	- Meta tags to include bare minimum:
		- [] charset
		- [] http-equiv
		- [] name="description"
		- [] viewport
		- [] robots... if you don't want them to index/follow
	- [] set the lang
	- [] title tag

	- Link Yer CSS:
		- [] Have a Normalize file
		- [] Have a style file

	- Start crafting your HTML sections using semantic tags:
		- [] header
		- [] footer
		- body: what info are you looking to display? Setup sections accordingly.
			- [] use filler text to illustrate what files/text goes with what HTML elements

	- Javascript: do you need actual files or is it so simple you just need to load a script?
		- [] Start adding references to files or setup `<script>` tags in your `<head>` tag. Don't forget about loading JS once the DOM is loaded ;)

You should have a bare skeleton with normalized CSS across browsers for you to start adding your content.

- [] Start fleshing out content. (Do not focus on styling yet.) This will include:
	- [] setting your `h1`, `h2`, `p`, `a` tags.
	- [] img tags:
		- [] alt attributes HARD REQUIREMENT
	