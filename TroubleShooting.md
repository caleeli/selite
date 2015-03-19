

# Expect complexity #
This technology works with third party components and many variables. You can reduce amount of misunderstanding (for you and others) by providing and following clear and exact steps. Do not assume or simplify what seems obvious, duplicated or unnecessary.

## Got stuck? ##
When you read documentation, and things don't work:
  * stop, switch to doing something else (the less related the better), get back to it later or some other day
  * read or check 'backwards' - from the last parts to the earlier ones
  * print it
  * read a print out at a different place
  * discuss it with someone in person
  * ask someone else to follow instructions in his/her environment, or observe him/her doing it in your environment.

Do the same when you write a report about a potential issue.

# Versions of components #
Have Firefox and Selenium IDE that are supported by current SeLite. See ProjectHome > [Compatibility](ProjectHome#Compatibility.md). Get current versions of all SeLite add-ons - as per AddOns > [Latest releases](AddOns#Latest_releases.md). (If you only get add-ons that you need, you may not be able to [run packaged tests](#Run_packaged_tests.md)). For unreleased functionality use AddOns > [Cutting edge](AddOns#Cutting_edge.md).

# Loading Selenium plugins #
Check whether packaged Selenium extensions start correctly: Open Selenium IDE > menu Options > Options... > Plugins. Verify that each plugin is enabled and with no error message (in red). If there is an error, inspect [Browser Console](#Browser_Console.md). (That screen doesn't show error details in [auxilliary Selenium IDE inside browser](SeleniumIde#One_standard_Selenium_IDE;_auxiliary_Selenium_IDEs_inside_browse.md)).

By default, Selenium IDE disables plugins that fail on start, and it keeps them disabled on subsequent restarts of Selenium IDE. That's even if the problems get resolved - Selenium IDE won't load such plugins, until you enable them. So you may want to disable that in the options above. See also DevelopmentTools > [Selenium IDE settings](DevelopmentTools#Selenium_IDE_settings.md).

# Narrow down the problem #
This may help you to figure out the issue yourself. Even if you don't solve it, you'll have collected information that will assist others to help you. In order to locate the issue you need to (as applicable)
  * reload your test DB from the app DB and re-run the test
  * eliminate extras
    * disable all other Firefox extensions and plugins (including  well-known ones like Firebug). Only leave extensions required to run your test.
    * minimise any custom Selenium extensions
    * cut down your test
    * replicate the issue against local .html page(s), simplified as much as possible
    * replace SeLite-specific commands (e.g. _typeRandom_) with their Selenium alternatives and see whether your locators work.

## Browser Console ##
If Selenium IDE log doesn't give much information about the problem, you need a log from Firefox itself. Visit Firefox URL _about:config_. Set preference _devtools.chrome.enabled_ to true (by double-clicking). Restart Firefox and go to its menu > Tools > Web Developer > Browser Console. Does it show any errors or warnings? Re-check the console after you start Selenium IDE and when you run scripts.

## Separate Firefox profile ##
If you don't want to modify your existing Firefox profile, [create a new one](https://developer.mozilla.org/en-US/Add-ons/Setting_up_extension_development_environment#Development_profile) (with no spaces in its name). Enable [Browser Console](#Browser_Console.md). Add any necessary non-SeLite extensions, until the problem appears. Alternatively, you could also [duplicate the existing profile](http://kb.mozillazine.org/Moving_your_profile_folder) (which is stored as a folder) and narrow down the problem there.

# Run packaged tests #
If you use AddOns > [Cutting edge](AddOns#Cutting_edge.md), that also gives you PackagedTests. Otherwise get the tests from SeLite source as per InstallFromSource.

Disable all Selenium extensions other than ones supported by SeLite. Run the tests as per PackagedTests. Then enabled other Selenium extensions and see if they break the tests.

# Defects in third party components #
If the cause is in Firefox, Selenium IDE or a third party component, submit a report in the respective bug tracking system (see also ThirdPartyIssues). If the problem is likely to affect other SeLite users and the third party confirms it, add a comment to ThirdPartyIssues with a link to that issue. Then other users can star it (vote for it), which could motivate the third party to solve your problem.<a href='Hidden comment: TODO change this if I disable wiki comments'></a>

# Report the issue #
If the problem is not caused by third party or custom extensions, you have something to report. Follow ReportingIssues.