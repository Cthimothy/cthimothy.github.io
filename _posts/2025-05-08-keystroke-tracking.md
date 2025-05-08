---
layout: post
title: "Keystroke tracking"
date: 2025-05-08
categories: blog,emacs
tags: 
---

I wanted a way to see my Emacs key strokes in real time, so I wrote a small function to display them in a buffer.
I'm sure there are better, existing solutions but this one works for me. It's a bit rough at the moment, as I need to find a way of
 going from this:

```
[2025-05-08 13:41:20] C-x b
[2025-05-08 13:41:22] 
[2025-05-08 13:41:23] k
[2025-05-08 13:41:23] e
[2025-05-08 13:41:23] y
[2025-05-08 13:41:23] SPC
[2025-05-08 13:41:24] l
[2025-05-08 13:41:24] o
[2025-05-08 13:41:24] g 
```
To something like this:
```
[2025-05-08 13:41:20] C-x b key SPC log
```
[https://github.com/Cthimothy/key-logger](https://github.com/Cthimothy/key-logger)
