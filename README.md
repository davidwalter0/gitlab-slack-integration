### Text
```
(git-stamp)

git-stamp: 2015.11.22T.17.18.41.-05:00:00 at move scripts to bin
git-stamp: 2015.11.22T.12.52.03.-05:00:00 at add mirror action to copy .slackurl to /tmp/${repo}-slack-url
git-stamp: 2015.11.22T.12.45.37.-05:00:00 at slackurl debugging
```


*Configure gitlab channel monitor gitlab+slack*
```
* Slack:
* create a channel for message in slack
  Channels [+] channel name

  e.g.

    #gitlab

* go to slack's Integrations projectname.slack.com/services/
  [user pulldown menu v] or Manage Your Team.

  [Integrations]

  [Incoming WebHooks]

  Choose a channel
     #gitlab 

  generate or copy the [Webhook URL] add text describing the hook,
  like gitlab monitors

* go to gitlab url  -- http://host/username/projectname/services/slack/edit

  or for global option settings -- http://host/admin/application_settings/services

  Add the [Webhook URL] to the webhook and select the events.
  User Name seems arbitrary. Maybe use GitlabWebhook
  Save
  [Test Settings]


```


Shell command
```
git commit -a -m "test commit at $(date +%Y.%m.%d.%H.%M.%S.%:::z)"; git push
```
emacs function
```
;; (save-excursion
;; (next-line 2)
;; (insert-string 
;;   (format "\nPrior commit: %s %s\n"
;;     (shell-command-to-string
;;         "printf '%s %s %s %s %s %s' $(git log --format=' %h %ci ' -n1) \
;;               $(git log --format='%D' -n1|cut -f 3,4 -d' '|sed -e 's/,//g')")
;;     (shell-command-to-string
;;         "git log --format='%s %N' -n1|head -1")))
;; (shell-command-to-string "git commit -a -m \"Commit performed by git-stamp at $(date +%Y.%m.%d.%H.%M.%S.%::z)\"")
;; (shell-command-to-string "git push github")
;; (save-buffer)))



(defun git-stamp ()
  ;; (interactive)
  ;; (interactive "scomment prefix %s to: ")
  (interactive)
   (save-excursion
   (let ((git-comment (read-string "git-commit-text: " nil 'my-commit-history)))
       (list (region-beginning) (region-end) git-comment)
       (list my-commit-history git-comment)
      (next-line)
;;      (insert-string 
;;        (format "\n%s %s %s\n" git-comment
;;          (shell-command-to-string
;;              "printf '%s %s %s %s %s %s' $(git log --format=' %h %ci ' -n1) \
;;                    $(git log --format='%D' -n1|cut -f 3,4 -d' '|sed -e 's/,//g')")
;;          (shell-command-to-string
;;              "git log --format='%s %N' -n1|head -1")))
      (insert-string 
         (format "git-stamp: %s at %s" 
           (format-time-string "%Y.%m.%dT.%H.%M.%S.%::z")
           git-comment))
      (save-buffer)
      (shell-command-to-string
         (format "git commit -a -m \"%s by git-stamp at %s\"" 
                 git-comment
                (format-time-string "%Y.%m.%dT.%H.%M.%S.%::z"))))
      (shell-command-to-string "git push github")))


```
---
### gitlab

add /tmp/project-name-slackurl with the url of the slack channel to message
by copying from .slackurl file to /tmp/${repo}-slack-url

chmod 600 /tmp/project-name-slackurl
slack-status must be run with the step-or-build option && rc

---
### mirror

mirror --repos=repos-space-separated-file-list

continuous monitoring of a restricted list of repositories pulling
commits and posting to a private repo.


---
### bin/make-yaml

generate the yaml for an execute run after capturing the slack url to
the .slackurl will enable the url to be written to a secret in the
cluster when the pod is created for the slack-config instance.

make-yaml reads the slack-config-template.yaml and writes the
slack-config.yaml


```

bin/make-yaml

kubectl create -f slack-config.yaml 

```


---

### TODO

[ ] auto extract and enable shared runners
[ ] create a mirror yaml for replication controller/service for mirroring
[ ] create a standalone config / yaml replication controller/service for gitlab-ci
[ ] auto insert into a standalone private registry and repository
[ ] auto inject configurations for continuous runners
[ ] include all members with notifications
[ ] create config service for simple pull of config info from http://config/slackurl

http://host/user/project/runners


---
### configure the gitlab runner instances to auto register

extract the settings -- http://host/ci/admin/runners : get the token
from the admin page and use this token to register that will allow
auto registration across projects [ shared runners ], rather than
using the per project runners

On the project page.

