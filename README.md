### Text
```
(git-stamp)


```


*Configure gitlab channel*
```
* create a channel for message
  channels + channel name

  #gitlab

* go to slack projectname.slack.com/services/
  integrations
  [Incoming WebHooks]
  Choose a channel
     #gitlab 

  generate or copy the [Webhook URL]

* go to gitlab url  -- http://host/username/projectname/services/slack/edit

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
  (shell-command-to-string "git push")
  (save-buffer)))

```
