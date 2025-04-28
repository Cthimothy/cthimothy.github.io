---
layout: post
title: "Journelly and Org"
date: 2025-04-28
categories: blog
tags: 
---

# Journalling with Journelly

I recently started using [Álvaro Ramírez’s](https://lmno.lol/alvaro) excellent
Journelly app. It's still in beta, but it has become an essential part of my
Org workflow. If you're not familair with it, think of it as a traditional 
journalling app, but in the form of a sort of personal Twitter. It has 
the funtionality for a journal entry to contain a photograph, and also adds
a geolocation tag to the entry. Most importantly, it uses Org, so it's all lovely
plain text.

On it's own, it's a great app; but with a little bit of Lisp, becomes essential.
I hacked up some code that converts Journelly entries in to Denote Journal files:

1.  Extract the individual journal entries (Journelly stores all entries in a 
  single file)

2. Extract any photos

3. Mung the url to reflect the new image location

4. Extract the geolocation data, and add it to the Denote file name (@location)

This function gets run each morning as part of my morning Emacs & Org ritual, and means
that my Journals directory now includes all Journelly entries in seperate Denote Journal
files.

I rely on Org-agenda, and would *love* if Journelly gained to functionality to quicky
record a TODO, but as it is, I am really enjoying using it.

My horrible code is here: https://github.com/Cthimothy/journelly-to-denote/blob/main/journelly-to-denote.el
