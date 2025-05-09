---
layout: post
title: "Keystroke tracking"
date: 2025-05-08
categories: blog,emacs
tags: 
---

### Update:  2025-May-09
#### Demi-fix: Now only tracks command and meta keys

```
(defun tw/keylog-toggle ()
  "Toggle key logging with timestamps. Only logs keys starting with C- or M-, ignoring mouse events."
  (interactive)
  (let* ((hook-symbol 'tw/keylog--log-command-hook))
    (unless (fboundp hook-symbol)
      (fset hook-symbol
            (lambda ()
              (let* ((buffer-name "*Key Log*")
                     (keys (key-description (this-command-keys-vector))))
                (unless (or (string-match-p "<mouse-" keys)
                            (string-match-p "<wheel-" keys)
                            (string-match-p "<double-" keys)
                            (string-match-p "<triple-" keys)
                            (string-match-p "<down-mouse-" keys)
                            (string-match-p "<drag-mouse-" keys))
                  (when (or (string-prefix-p "C-" keys)
                            (string-prefix-p "M-" keys))
                    (let ((timestamp (format-time-string "%Y-%m-%d %H:%M:%S")))
                      (with-current-buffer (get-buffer-create buffer-name)
                        (goto-char (point-max))
                        (unless (bolp)
                          (insert "\n"))
                        (insert (format "[%s] %s" timestamp keys))
                        (dolist (win (get-buffer-window-list (current-buffer) nil t))
                          (with-selected-window win
                            (goto-char (point-max)))))))))))
    (if (member hook-symbol post-command-hook)
        (progn
          (remove-hook 'post-command-hook hook-symbol)
          (message "Key logging stopped."))
      (add-hook 'post-command-hook hook-symbol)
      (message "Key logging started. See buffer *Key Log*"))))
```

---

### Update: 2025-May-09
It's quickly became apparent that this approach is far from ideal. FIXME: Only capture command key strokes (C- and M-) and arguments;
 which, the more I think about it, the less trivial it becomes.
 
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

```
(Defun tw/keylog-toggle ()
  "Toggle key logging with timestamps. Ignoring mouse events."
  (interactive)
  (let* ((buffer-name "*Key Log*")
         (hook-symbol 'tw/keylog--log-command-hook))
    (unless (fboundp hook-symbol)
      (fset hook-symbol
            (lambda ()
              (let ((keys (key-description (this-command-keys-vector))))
                (unless (or (string-match-p "<mouse-" keys)
                            (string-match-p "<wheel-" keys)
                            (string-match-p "<double-" keys)
                            (string-match-p "<triple-" keys)
                            (string-match-p "<down-mouse-" keys)
                            (string-match-p "<drag-mouse-" keys))
                  (let ((timestamp (format-time-string "%Y-%m-%d %H:%M:%S")))
                    (with-current-buffer (get-buffer-create buffer-name)
                      (goto-char (point-max))
                      (unless (bolp)
                        (insert "\n"))
                      (insert (format "[%s] %s" timestamp keys))
                      (dolist (win (get-buffer-window-list (current-buffer) nil t))
                        (with-selected-window win
                          (goto-char (point-max))))))))))
    (if (member hook-symbol post-command-hook)
        (progn
          (remove-hook 'post-command-hook hook-symbol)
          (message "Key logging stopped."))
      (add-hook 'post-command-hook hook-symbol)
      (message "Key logging started. See buffer %s" buffer-name))))
```
