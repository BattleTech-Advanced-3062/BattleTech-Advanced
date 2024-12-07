# Wiki Automation Documentation

The Wiki Automation uses Github's Actions to post to (currently) the BTA MediaWiki.

In order to do this, some setup and guardrails are needed. 

# How this works
In order to minimize consumption of free Github Actions minutes, these workflows only trigger on merge to the `wiki` branch. Yes, Amid knows we have thousands. This decision was made with an eye towards long-term expansion. There is no risk of costs, as running out of free minutes simply fails all running or future jobs for the month until the Organization's plan is upgraded.

Create a `wiki` branch and make sure it has the latest code.

The actual function is very simple: the action checks out this repo and the [wiki-automation](https://github.com/BattleTech-Advanced-3062/bta-wiki-automation) one, then runs the scripts from the automation repo against this one. 

# Settings
## Variables and Secrets

The automation uses Mediawiki's login functions to post to the API. As such, a bot account is required. Go to [the wiki page](https://www.bta3062.com/index.php?title=Special:BotPasswords) for that and create one for the wiki automation and give it the following grants:

- Basic rights
- High-volume editing
- Edit existing pages
- Create, edit and move pages
- Upload new files
- Upload, replace and move files
- Rollback changes to pages
- Delete pages, revisions, and log entries
- Hide users and suppress revisions
- Protect and unprotect pages
- Merge Page Histories
- "rawdata" rights bundle

Record the password somewhere, like your password manager.

Next, go to the repo Settings and go to the Secrets and variables section, under Security. Select the Actions submenu. 

Under the Secrets tab, click "New repository secret" and add the password with the name WIKI_PASS.

Under the Secrets tab, click "New repository secret" and add the bot's username with the name WIKI_USER. Reminder that MediaWiki bot names are formatted as "YourUserName@BotName"

## User Rights
If you want a user to have the ability to rerun and maybe some deeper troubleshooting capabilities, that user will need Write abilities to the repository. 

There may be a way to restrict the user further with Custom Roles, but apparently Amid can't test that in his corporate account because that functionality is restricted to Organization administrators and he's managed to avoid that permissions set so far.  