# Emacs for Julia editing

I use emacs for my Julia editing.  An edited version of my .emacs (not
working) is below.

I usually run a separate REPL in a terminal as opposed to within
emacs.  As I found that it can hang emacs, if e.g. tons of output gets
spewed to it.  However, with below setup you can run a julia-repl
within emacs: `M-x julia-repl` (using
https://github.com/tpapp/julia-repl).

To automatically update code within a REPL session I use the excellent
[Revise.jl](https://github.com/timholy/Revise.jl).

```elisp
;; Julia setup:
;  Use Revise.jl!!! That's it.

;; http://emacswiki.org/emacs/DeletingWhitespace#toc3
(add-hook 'before-save-hook 'delete-trailing-whitespace)

;;;;;;;;;;;;;;;;;;;;;;;;;;;
;; common settings
;;;;;;;;;;;;;;;;;;;;;;;;;;;
(load-file "~/.emacs_common")
;; Ido, Emacs Server, show paren, (global-font-lock-mode t), key-bindings

;;;;;;
;; Code refactoring
;;;;;;
; http://oremacs.com/2015/01/27/my-refactoring-workflow/
; M-S-, to grep (recursively)
; C-c C-p edit grep buffer
; save
(setq load-path (cons "~/elisp/wgrep" load-path))
(require 'wgrep)

;; Magit -> I should use it


;; JULIA ;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;;
(require 'julia-mode)
;; https://tpapp.github.io/post/emacs-julia-customizations/
(defun customize-julia-mode ()
  "Customize julia-mode."
  (interactive)
  ;; my customizations go here
  (font-lock-add-keywords nil
                        '(("\\<\\(FIXME\\|TODO\\|QUESTION\\|NOTE\\)"
                           1 font-lock-warning-face t)))
  (flyspell-prog-mode)
  (ispell-change-dictionary "en_US")
  )

(add-hook 'julia-mode-hook
      (lambda ()
        (customize-julia-mode)
))

; Make indentation work for long functions:
; https://github.com/JuliaEditorSupport/julia-emacs/issues/5
(setq julia-max-block-lookback 30000)

;; julia-repl https://github.com/tpapp/julia-repl
(require 'julia-repl)
(add-hook 'julia-mode-hook 'julia-repl-mode) ;; always use minor mode

;; CTAGS ETAGS
; https://www.emacswiki.org/emacs/EtagsTable
; M-. and M-,
(require 'etags-table)
(setq etags-table-alist
      '(
        (".*\\.jl$" "/home/mauro/julia/julia-0.6/TAGS" "/home/mauro/.julia/v0.6/TAGS")
        ))
(setq tags-case-fold-search nil) ; case sensitive search
;;; View tags other window
(defun view-tag-other-window (tagname &optional next-p regexp-p)
  "Same as `find-tag-other-window' but doesn't move the point"
  (interactive (find-tag-interactive "View tag other window: "))
  (let ((window (get-buffer-window)))
    (find-tag-other-window tagname next-p regexp-p)
    (recenter 0)
    (select-window window)))
(global-set-key (kbd "M-*") 'pop-tag-mark)
```
