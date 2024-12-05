;;; init.el --- Initialization File! --- -*- lexical-binding: t; -*-
;;; Code:

;; Packages
(require 'package)
(add-to-list 'package-archives
             '("melpa" . "http://melpa.org/packages/") t)
(package-initialize)

(unless (package-installed-p 'use-package)
  (package-refresh-contents)
  (package-install 'use-package))

(eval-when-compile
  (require 'use-package))

(use-package emacs
  :ensure t
  :init
  ;; Theme
  (add-to-list 'custom-theme-load-path "~/.emacs.d/themes")
  (load-theme 'rotor :no-confirm)
  ;; Sane defaults (credit bedrock-emacs by ashton314)
  (setopt inhibit-splash-screen t)
  (setopt initial-major-mode 'fundamental-mode)
  (setopt display-time-default-load-average nil)
  (setopt auto-revert-avoid-polling t) ; Reread from disk for file changes automatically
  (setopt auto-revert-interval 5)
  (setopt auto-revert-check-vc-info t)
  (global-auto-revert-mode)
  (savehist-mode) ; Save history of minibuffer
  (setopt sentence-end-double-space nil)
  (when (display-graphic-p)
    (context-menu-mode))
  ;; Litter fixes
  (defun bean--backup-file-name (fpath)
    "Return a new file path of a given file path. If the new path's directories doesn't exist; create them."
    (let* ((backupRootDir (concat user-emacs-directory "emacs-backup/"))
	   (filePath (replace-regexp-in-string "[A-Za-z]:" "" fpath )) ; remove Windows driver letter in path
           (backupFilePath (replace-regexp-in-string "//" "/" (concat backupRootDir filePath "~") )))
      (make-directory (file-name-directory backupFilePath) (file-name-directory backupFilePath))
      backupFilePath))
  (setopt make-backup-file-name-function 'bean--backup-file-name)
  (setopt enable-recursive-minibuffers t)                ; Use the minibuffer whilst in the minibuffer
  (setopt completion-cycle-threshold 1)                  ; TAB cycles candidates
  (setopt completions-detailed t)                        ; Show annotations
  (setopt tab-always-indent 'complete)                   ; When I hit TAB, try to complete, otherwise, indent
  (setopt completion-styles '(basic initials substring)) ; Different styles to match input to candidates

  (setopt completion-auto-help 'always)                  ; Open completion always; `lazy' another option
  (setopt completions-max-height 20)                     ; This is arbitrary
  (setopt completions-detailed t)
  (setopt completions-format 'one-column)
  (setopt completions-group t)
  (setopt completions-group t)
  (setopt completion-auto-select 'second-tab)            ; Much more eager
  (keymap-set minibuffer-mode-map "TAB" 'minibuffer-complete) ; TAB acts more like how it does in the shell
  (ido-mode)
  (setopt line-number-mode t)                        ; Show current line in modeline
  (setopt column-number-mode t)                      ; Show column as well

  (setopt x-underline-at-descent-line nil)           ; Prettier underlines
  (setopt switch-to-buffer-obey-display-actions t)   ; Make switching buffers more consistent

  (setopt show-trailing-whitespace nil)      ; By default, don't underline trailing spaces
  (setopt indicate-buffer-boundaries 'left)  ; Show buffer top and bottom in the margin

  ;; Enable horizontal scrolling
  (setopt mouse-wheel-tilt-scroll t)
  (setopt mouse-wheel-flip-direction t)
  (setopt indent-tabs-mode nil)
  (setopt tab-width 4)
  (blink-cursor-mode -1)                                ; Steady cursor
  (pixel-scroll-precision-mode)                         ; Smooth scrolling
  (cua-mode)
  (add-hook 'prog-mode-hook 'display-line-numbers-mode)
  (setopt display-line-numbers-width 3)           ; Set a minimum width
  ;; Nice line wrapping when working with text
  (add-hook 'text-mode-hook 'visual-line-mode)
  (setopt tab-bar-show 1)
  ;; Add the time to the tab-bar, if visible
  (add-to-list 'tab-bar-format 'tab-bar-format-align-right 'append)
  (add-to-list 'tab-bar-format 'tab-bar-format-global 'append)
  (setopt display-time-format "%a %F %T")
  (setopt display-time-interval 1)
  (display-time-mode))

(use-package evil
  :ensure t
  :demand t
  :bind (("<escape>" . keyboard-escape-quit))
  :init
  (setq evil-want-keybinding nil)
  (setq evil-undo-system 'undo-fu)
  (setq evil-insert-state-cursor '(hbar . 8))
  :config
  (evil-mode 1))

(use-package evil-collection
  :ensure t
  :after evil
  :config
  (setq evil-want-integration t)
  (evil-collection-init))
  

;;; init.el ends here

(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(package-selected-packages '(evil-collection evil)))
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )
