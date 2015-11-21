### Text

(defun git-stamp ()
  (insert-string 
    (format "\n\n%s%s\n"
      (shell-command-to-string
          "echo $(git log --format='%ci' -n1) \
                $(git log --format='%D' -n1|cut -f 3 -d' '|sed -e 's/,//g')")
      (shell-command-to-string
          "git log --format='%s' -n1"))))

(git-stamp)


2015-11-21 12:25:06 -0500 master
2015.11.21.12.25.06.-05


2015-11-21 12:22:17 -0500 master
test hooks





