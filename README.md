# ewnium
The Emacs EWW version of Vimium plugin


## Installatin

```lisp
(use-package eww
  :defer t
  :init
  (add-hook 'eww-after-render-hook #'shrface-mode)
  :config
  (require 'shrface))

(use-package shrface
  :ensure t
  :defer t
  :config
  (shrface-basic)
  (shrface-trial)
  (shrface-default-keybindings) ; setup default keybindings
  (setq shrface-href-versatile t))

(use-package shr-tag-pre-highlight
  :ensure t
  :after shr
  :config
  (add-to-list 'shr-external-rendering-functions
               '(pre . shr-tag-pre-highlight)))

(use-package ewnium
  :ensure nil
  :load-path "path/to/ewnium"
  :hook (eww-mode . ewnium-mode))
```



## Issues
- Function names are hidden when inspecting keybindings.
  Due to how eww mode works, (it creates local keymaps for input elements such as text/radio/etc),
  the code has to also support this other wise, you can be in a text input and press "d" and
  instead of typing a letter, it'll try and execute a command.


  Fix will probably be to make each function check the context,
  instead of what I'm doing which is monkey patching the functions at the end for a quick fix.
