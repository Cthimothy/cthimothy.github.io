---
layout: post
title: "Elisp function to create new Jekyll blog post"
date: 2025-02-18
categories: blog
tags: 
---

# Create blog post
'(defun tw/create-jekyll-post ()
  "Create a new Jekyll blog post in ~/Projects/cthimothy.github.io/_posts/."
  (interactive)
  (let* ((title (read-string "Post title: "))
         (slug (replace-regexp-in-string "[^a-z0-9-]" "" (downcase (replace-regexp-in-string " " "-" title))))
         (date (format-time-string "%Y-%m-%d"))
         (filename (expand-file-name (format "%s-%s.md" date slug)
                                     "~/Projects/cthimothy.github.io/_posts/")))
    (if (file-exists-p filename)
        (message "File already exists: %s" filename)
      (find-file filename)
      (insert (format
               "---\n\
layout: post\n\
title: \"%s\"\n\
date: %s\n\
categories: blog\n\
tags: \n\
---\n\n"
               title date))
      (save-buffer)
      (message "Created new Jekyll post: %s" filename))))'
