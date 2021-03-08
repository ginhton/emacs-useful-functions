# emacs useful functions

a collection of useful emacs functions

## toggle maximize buffer
```elisp
(defun toggle-maximize-buffer ()
  "Toggle maximize buffer"
  (interactive)
  (if (= 1 (length (window-list)))
      (progn
        (set-window-configuration my-saved-window-configuration)
        (goto-char my-saved-point))
    (setq my-saved-window-configuration (current-window-configuration)
          my-saved-point (point))
    (delete-other-windows)))
```

## resize window
```elisp
(defun transient-window-resize ()
  "Transient version of window resize"
  (interactive)
  (let ((echo-keystrokes nil))
    (message "Resize Window: [}]enlarge-h, [{]shrink-h, [+]enlarge, [-]shrink")
    (set-transient-map
     (let ((map (make-sparse-keymap)))
	   (define-key map [?+] #'enlarge-window)
	   (define-key map [?}] #'enlarge-window-horizontally)
	   (define-key map [?-] #'shrink-window)
	   (define-key map [?{] #'shrink-window-horizontally)
	   map)
       t)))
```

## switch to last buffer
```elisp
(defun switch-to-last-buffer ()
  (interactive)
  (switch-to-buffer (other-buffer (current-buffer) 1)))
```
