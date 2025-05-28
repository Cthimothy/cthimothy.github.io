---
layout: post
title: "Simplifying my PKM"
date: 2025-05-26
categories: blog,pkm,emacs,denote
tags: 
---

	I have an unhealthy relationship with PKM, task and project management systems. Similar to  how
	audiophiles are sometimes guitly of 'listening to their 	hifi systems', PKM users cab be guilty 
	of 'using' their chosen systems, rather than *actually* using them. As an Emacs user, this worsens 
	the issue by an	order of magnitude.
	
	Over the years I've spent hundreds of hours developing and refining my Emacs Org-mode system; I have
	written countless functions in an attempt to streamline and simplify my workflow, including
	creating an entire front end with dedicated windows and buffers, displaying tags (multiple types of),
	various agenda views, different capture configs, methods of searching, filtering and surfacing,
	even integrating an LLM. And, while I have thoroughly enjoyed hacking on it, I'm not sure if it ever
	actually made me noticably more productive.
	
	So, I decided to experiment going back to something far simpler; of course, still using Emacs.
	
	For a while now, I've been using Prot's excellent Denote package, which I integrated in to my earlier,
	overly baroque system, and I am still using it now. My current configuration depends on whether I am 
	using my laptop, or at my desk. On my laptop, I use easysession to configure a window layout with a
	vertical split; denote-dired-mode on the left hand side, and the right for viewing notes. I use a
	a few functions to display, search and filter notes:
	
-  C-c d o: Open Denote directory
-  C-c d n: New Denote note
-  C-c d k: List all Denote keywords (filenames)
-  C-c d f: Filter matching keywords
-  C-c d F: Exclude matching keywords
-  C-c d g: Grep Denote notes - case insensitive
-  C-c d G: Grep Denote notes - case sensitive
-  C-c c b: Create new blog entry
-  C-c d j n: Create daily journal
-  C-c d j j: Convert Journelly entries in to distinct Denote notes
-  ]: Open note in right hand window

	As well as simplifying my PKM, I have also downsized my org-agenda use. I've moved away from a complicated set
	of functions, and now simply use it to list ALL my tasks (with some grouping), which I re-file tasks I wish to 
	undertake that day in to that day's Tasks secion of my daily denote journal. 

	It all works well, and although I do miss hacking on my productivity system, I am finding myself actually ejoying
	being more productive.
