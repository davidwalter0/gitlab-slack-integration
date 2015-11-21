### Text
Shell command
```
git commit -a -m "test commit at $(date +%Y.%m.%d.%H.%M.%S.%:::z)"; git push
```
emacs function
```
(defun git-stamp ()
  (interactive)
  (save-excursion
  (next-line 2)
  (insert-string 
    (format "\n\n%s%s\n"
      (shell-command-to-string
          "echo $(git log --format='%ci' -n1) \
                $(git log --format='%D' -n1|cut -f 3 -d' '|sed -e 's/,//g')")
      (shell-command-to-string
          "git log --format='%s' -n1")))
  (insert-string (shell-command-to-string "git commit -a -m \"test commit at $(date +%Y.%m.%d.%H.%M.%S.%:::z)\"; git push"))))

(git-stamp)
```


2015-11-21 12:26:33 -0500 master
test commit at 2015.11.21.12.26.33.-05

