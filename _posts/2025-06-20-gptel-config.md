---
layout: post
title: "GPTel config"
date: 2025-06-20
categories: blog,ollama,gptel,emacs
tags: 
---

I've been playing with Ollama and gptel this morning. This is my very simple, hacky config thus far; it allows me to summarise marked regions in the current, open gptel window, or optioanlly with a prompt:

```
(use-package gptel
  :ensure t
  :config
  (setq gptel-backend
        (gptel-make-ollama "Ollama"
          :host "localhost:11434"
          :stream t
          :models '(llama3:8b)))   ;; use your exact model
  (setq gptel-model 'llama3:8b)
  (setq gptel-default-mode 'org-mode)

  (defun tw/gptel-send-region-with-prompt (start end prompt)
    "Send selected region with a custom prompt to the *Ollama* GPTel buffer."
    (interactive
     (list (region-beginning)
           (region-end)
           (read-string "Ask GPT about the region: " "Summarise this")))
    (let* ((text (buffer-substring-no-properties start end))
           (message (concat prompt "\n\n" text))
           (buf-name "*Ollama*"))
      (let ((buf (get-buffer buf-name)))
        (if buf
            (with-current-buffer buf
              (goto-char (point-max))
              (insert message)
              (gptel-send)
              (pop-to-buffer buf))
          (message "No GPTel buffer found named %s" buf-name)))))

  (define-prefix-command 'tw/gptel-prefix)
  (global-set-key (kbd "C-c g") 'tw/gptel-prefix)
  (define-key tw/gptel-prefix (kbd "p") #'tw/gptel-send-region-with-prompt)
  (define-key tw/gptel-prefix (kbd "s") #'tw/gptel-summarise-region))
  ```
