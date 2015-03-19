

# Support scope #
SeLite doesn't support functionality of related components and technologies (Selenium IDE, SelBlocks, SQLite, Firefox, Selenium selectors, XPath, Javascript...). See also WikiPages > [Documentation scope](WikiPages#Documentation_scope.md).

Search in current [issues](https://code.google.com/p/selite/issues/list?can=1&q=status%3ANew+OR+status%3AAccepted+OR+status%3AStarted+OR+status%3AWontFix). If an existing issue covers your problem, vote for it.

# Report an issue #
First, follow TroubleShooting. Before you [report an issue](https://code.google.com/p/selite/issues/entry), note details and versions of
  * any SeLite extensions
  * Selenium IDE
  * any other Firefox extensions
  * Firefox (and if it's not a current release then also URL from where you downloaded it)
  * SQLite DB (if applicable)
  * OS and whether 32 or 64 bit
  * any non-SeLite components and their origin - the URL for download or GIT/SVN checkout (including branch and revision)

Collect any errors from logs (as per TroubleShooting). If logs are short, copy and paste them in the error report. Otherwise install AddOnsThirdParty > File Logging, restart Firefox, re-run your script, save the log in a file and attach it to the error issue.

By submitting or commenting on a report, you agree that any part of it can be used in SeLite (under current or any future license).

<a href='Hidden comment: Comment: too much:
* apply [https://developer.mozilla.org/en-US/docs/Mozilla/QA/Bug_writing_guidelines Bug Writing Guidelines] from Mozilla
* follow [https://bugzilla.mozilla.org/page.cgi?id=etiquette.html Etiquette] of Bugzilla
* create reports as [http://sscce.org/ Short, Self Contained, Correct Examples]
'></a>

## Submit any failing the tests ##
Save your test cases and test suites, along with any HTML forms/pages as per PackagedTests > [Structure](PackagedTests#Structure.md). If needed, include store any [Settings](SettingsOverview.md) as per [SettingsManifests](SettingsManifests.md) > ['Values' manifests](SettingsManifests#'Values'_manifests.md). Put that in a .zip file and attach it to the issue. That prevents typing mistakes and misunderstanding. Alternatively, if you report only a few simple Selenese command calls, you could send them as text
```

command | target | value
command | target | value
```
However, that allows for mistakes on both sides. Also, the system for tracking issues may modify text content (e.g. it changes names of wiki pages and any URLs to links).

Do not send any screenshots that just show messages or your command(s). Report any messages as text. Only attach screenshots if they demonstrate a defect that doesn't have a message.

## Submit your Firefox profile ##
If the problem only happens with third party or custom extensions, or if it involves a complex situation, you may need to attach your Firefox profile. See also TroubleShooting > [Separate Firefox profile](TroubleShooting#Separate_Firefox_profile.md). [Locate the Firefox profile](https://support.mozilla.org/en-US/kb/profiles-where-firefox-stores-user-data#w_how-do-i-find-my-profile) folder. Turn Firefox off, remove any [private data](https://support.mozilla.org/en-US/kb/recovering-important-data-from-an-old-profile#w_your-important-data-and-their-files) and _places.sqlite_. Zip up the folder and attach it to the issue (or email it to the maintainer).