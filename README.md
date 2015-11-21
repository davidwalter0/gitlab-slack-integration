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
    (format "\n\n%s%s\n"
      (shell-command-to-string
          "echo $(git log --format='%ci' -n1) \
                $(git log --format='%D' -n1|cut -f 3 -d' '|sed -e 's/,//g')")
      (shell-command-to-string
          "git log --format='%s' -n1")))
    (insert-string (shell-command-to-string "git commit -a -m \"test commit at $(date +%Y.%m.%d.%H.%M.%S.%:::z)\""))
  (save-buffer)
  (insert-string (shell-command-to-string "git push"))))

```
