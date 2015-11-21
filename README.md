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
    (insert-string (shell-command-to-string "git commit -a -m \"test commit at $(date +%Y.%m.%d.%H.%M.%S.%:::z)\""))
  (save-buffer)
  (insert-string (shell-command-to-string "git push"))))

(git-stamp)
```


2015-11-21 12:45:57 -0500 master
test commit at 2015.11.21.12.45.57.-05

[master 501ec12] test commit at 2015.11.21.12.46.39.-05
 1 file changed, 9 insertions(+)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   688c559..501ec12  master -> master


2015-11-21 12:45:41 -0500 master
test commit at 2015.11.21.12.45.41.-05

[master 688c559] test commit at 2015.11.21.12.45.57.-05
 1 file changed, 15 insertions(+), 1 deletion(-)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   3c4ce39..688c559  master -> master


2015-11-21 12:44:39 -0500 master
test commit at 2015.11.21.12.44.39.-05

[master 3c4ce39] test commit at 2015.11.21.12.45.41.-05
 1 file changed, 9 insertions(+)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   29e83b6..3c4ce39  master -> master


2015-11-21 12:37:16 -0500 master
test commit at 2015.11.21.12.37.16.-05

[master 29e83b6] test commit at 2015.11.21.12.44.39.-05
 1 file changed, 46 insertions(+), 1 deletion(-)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   2841a67..29e83b6  master -> master


2015-11-21 12:37:16 -0500 master
test commit at 2015.11.21.12.37.16.-05

On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
	.#README.md

nothing added to commit but untracked files present
Everything up-to-date


2015-11-21 12:37:16 -0500 master
test commit at 2015.11.21.12.37.16.-05

On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
	.#README.md

nothing added to commit but untracked files present
Everything up-to-date


2015-11-21 12:37:16 -0500 master
test commit at 2015.11.21.12.37.16.-05

On branch master
Your branch is up-to-date with 'origin/master'.
Untracked files:
	.#README.md

nothing added to commit but untracked files present
Everything up-to-date


2015-11-21 12:35:24 -0500 master
test commit at 2015.11.21.12.35.24.-05

[master 2841a67] test commit at 2015.11.21.12.37.16.-05
 1 file changed, 15 insertions(+)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   1ceaf85..2841a67  master -> master


2015-11-21 12:29:03 -0500 master
test commit at 2015.11.21.12.29.03.-05

[master 1ceaf85] test commit at 2015.11.21.12.35.24.-05
 1 file changed, 2 insertions(+), 1 deletion(-)
To git@k8s-node-01:davidwalter0/falcon-token-test.git
   fae92bd..1ceaf85  master -> master


2015-11-21 12:29:03 -0500 master
test commit at 2015.11.21.12.29.03.-05



2015-11-21 12:26:33 -0500 master
test commit at 2015.11.21.12.26.33.-05

