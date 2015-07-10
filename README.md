# spacemacs
This is my spacemacs config file. Is this for you? If you're all
about emacs, probably not, since you have your own set up.

If you're interested, here's what this config gets you:

##Defaults

* Mode: Straight up holy mode, cause evil is really not that cool.
* Theme: Monokai
* Auto-Save: Original (auto-saves in-place instead of to cache)
* 

##Layers
The following layers are enabled:

* auto-completion
* better-defaults
* clojure
* emacs-lisp
* elixir
* erlang
* git
* github
* haskell
* javascript
* markdown
* python
* org
* search-engine
* shell
* syntax-checking
* version-control

##Additional Packages
The following additional packages are enabled:
     
* alchemist
* cider

##Keyboard Mapping

```
;; commenting/uncommenting
(global-set-key (kbd "C-c C-r") 'comment-region)
(global-set-key (kbd "C-c C-u") 'uncomment-region)

;; set frame to 80 columns (plus 2 for padding)
(global-set-key "\C-x=" '(set-frame-width (selected-frame) 82))

;; paging
(global-set-key (kbd "M-]") 'forward-paragraph)
(global-set-key (kbd "M-[") 'backward-paragraph)

;; killing up to character (requires zap-up-to-char function below)
(global-set-key (kbd "C-c C-k") 'zap-up-to-char)

;; searching - replace default search with regexp search
(global-set-key (kbd "C-s") 'isearch-forward-regexp)
(global-set-key (kbd "C-r") 'isearch-backward-regexp)
(global-set-key (kbd "C-M-s") 'isearch-forward)
(global-set-key (kbd "C-M-r") 'isearch-backward)

;; defining/running macro 
(global-set-key (kbd "C-c C-d C-m") 'kmacro-start-macro)
(global-set-key (kbd "C-c C-d C-e") 'kmacro-end-macro)
(global-set-key (kbd "C-c C-c C-m") 'call-last-kbd-macro)

;; multi-term - my term of choice
(global-set-key (kbd "C-c C-m") 'multi-term)

;; erc
(global-set-key (kbd "C-c C-e") 'erc)

;; undo
(global-set-key (kbd "C-/") 'undo)

;; cut/copy
(global-set-key (kbd "C-w") 'kill-ring-save)
(global-set-key (kbd "M-w") 'kill-region)

;; fill-column-indicator
(global-set-key (kbd "C-x C-m C-f") 'spacemacs/toggle-fill-column-indicator)
```

##Functions
```
  (defun zap-up-to-char (arg char)
    "Kill up to, but not including ARGth occurrence of CHAR.
  Case is ignored if 'case-fold-search' is non-nil in the current buffer.
  Goes backward if ARG is negative; error if CHAR not found.
  Ignores CHAR at point."
    (interactive "p\ncZap up to char: ")
    (let ((direction (if (>= arg 0) 1 -1)))
      (kill-region (point)
                   (progn
                     (forward-char direction)
                     (unwind-protect
                         (search-forward (char-to-string char) nil nil arg)
                       (backward-char direction))
                       (point)))))
```
