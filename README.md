### Text
```
(git-stamp)


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
(defun git-stamp ()
  (interactive)
  (save-excursion
  (next-line 2)
  (insert-string 
    (format "\nPrior commit: %s %s\n"
      (shell-command-to-string
          "printf '%s %s %s %s %s %s' $(git log --format=' %h %ci ' -n1) \
                $(git log --format='%D' -n1|cut -f 3,4 -d' '|sed -e 's/,//g')")
      (shell-command-to-string
          "git log --format='%s %N' -n1|head -1")))
  (shell-command-to-string "git commit -a -m \"Commit performed by git-stamp at $(date +%Y.%m.%d.%H.%M.%S.%::z)\"")
  (shell-command-to-string "git push github")
  (save-buffer)))

```
---
### gitlab

add .slackurl with the url of the slack channel to message

slack-status must be run with the step-or-build option && rc

---
### mirror

mirror --repos=repos-space-separated-file-list

continuous monitoring of a restricted list of repositories pulling
commits and posting to a private repo.


---
### configure the gitlab runner instances to auto register

extract the settings -- http://host/ci/admin/runners : get the token
from the admin page and use this token to register that will allow
auto registration across projects [ shared runners ], rather than
using the per project runners

On the project page.


TODO: extract and enable shared runners ]]

http://host/user/project/runners


