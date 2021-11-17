# Summary

This project is an automation for Jira Cloud which allows users to flag mentions in comments by adding an exclamation mark after the mention (ie: @User Name !) to target it for automation.

I have created it so that users have an easy way of saying "Hey, this comment or task needs @This Person ! to look at it before it can proceed" without having to change the assignee or any other important fields.

### Usage

Users can add an "!" after a mention of another user in a comment. The automation will put the flagged mentions into the "Waiting on Reply" field. On our main dashboard users have a "Waiting on My Reply" widget, which populates via a JQL Filter Box. The JQL Filter shows all tasks in which the current user is present 

"Waiting on Reply[User Picker (multiple users)]" = currentUser()

This shows all the tasks where their name is present in the Waiting on Reply field so that they can see what tasks need their attention.

If a user currently in the Waiting on Reply field of a task then leaves a comment on that task, they are automatically removed from the field, and one less task is shown under their "Waiting on My Reply" widget on their dashboard. 


### Example Comment
Evan Nixon ! This mention is flagged for automation.
This is some example comment body text followed by a mention of Automation for Jira that is not flagged.

Automation for Jira is not a target for this automation because it’s mention isn’t followed by a “!”. 

But now Jira Outlook ! is targeted for automation. 

### Example Comment.Body

This is the actual output of the above comment via the Jira REST API (specifically version 2)

```json
[~accountid:610a6c430b454a00681be664] \\! This mention is flagged for automation.\nThis is some example comment body text followed by a mention of [~accountid:557058:f58131cb-b67d-43c7-b30d-6b58d40bd077] that is not flagged.\n\n\n[~accountid:557058:f58131cb-b67d-43c7-b30d-6b58d40bd077] is not a target for this automation because it's mention isn't followed by a "!". \n\nBut now [~accountid:5d53f3cbc6b9320d9ea5bdc2] \\! is targeted for automation. 
```

### REGEX

https://regex101.com/r/mWhPO5/1
