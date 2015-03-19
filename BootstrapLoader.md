
# Summary #
[SeLite Bootstrap](https://addons.mozilla.org/en-US/firefox/addon/SeLite-Bootstrap/versions/), one of SeLite AddOns, allows smoother development of Selenium Core extensions (just plain javascript files, not .xpi). It reloads them automatically on change.
It's more convenient than Selenium IDE's way of loading Core extensions (Selenium menu > Options > Options > General > 'Activate developer tools'), which requires you to check Selenium menu > Options > Options > General > 'Reload' button everytime you change your extension file.

# Details #
It adds field _bootstrapCoreExtensions_ to [Settings](SettingsOverview.md) module _extensions.selite-settings.common_, where you can choose file(s) containing your Core extension in Javascript (saved in UTF-8). If you're sharing your tests, you may want to configure that through SettingsManifests > [Literals for special values](SettingsManifests#Literals_for_special_values.md).

If you modify any one file that is registered with Bootstrap (while using Selenium IDE), all the registered files get re-loaded automatically next time you
  * run a single Selenese command (before that command)
  * run a test case/test suite (before the case/suite)
  * pause and subsequently resume a test case/test suite (before it is resumed)

Apply JavascriptEssential, especially [Strict Javascript](JavascriptEssential#Strict_Javascript.md) and [Prevent name conflicts](JavascriptEssential#Prevent_name_conflicts.md).

It works only in standalone Selenium IDE, but not in [auxiliary Selenium IDEs inside browser](SeleniumIde#One_standard_Selenium_IDE;_auxiliary_Selenium_IDEs_inside_browse.md) (neither in Selenium IDE in browser sidebar).

# Limitations #
## Intercepts ##
Bootstrap reloads all registered extensions (whenever you modify any one of them). So, if you 'extend' an existing method through a head/tail intercept, then don't re-save the method each time the script is run. Otherwise it would increase the intercept chain. Instead, save the original method on the first load only. For example:
```js

var originalMethod;
if( originalMethod===undefined ) {
originalMethod= Selenium.prototype.methodName;
}
Selenium.prototype.methodName= function(pqr...) {
originalMethod.call(this);
// extra new tasks...
}
```
See also JavascriptEssential > [Function intercepts](JavascriptEssential#Function_intercepts.md).

## Adding/modifying the Selenese (commands/getters etc.) ##
If you introduce or modify any Selenese command/getter - Selenium.prototype.doXXX, Selenium.prototype.getXXX or Selenium.prototype.isXXX, then those will be available to your test commands/case/test suite only **after** you run any Selenese command first. <a href='Hidden comment: Peter doesn"t know why.'></a>

## Switching between files ##
If you add/remove filenames from _bootstrapCoreExtensions_ (or you switch to a different default set or a test suite with a different set associated with it), Bootstrap can't 'unload' a file that it has loaded already. If you change the options back later, it won't re-run the file, unless its timestamp has changed.

## Dependencies between files ##
Bootstrap initiates Core extensions after any Core extensions loaded as Firefox add-ons (whether they use ExtensionSequencer or not).

If you have multiple files registered with Bootstrap through a 'values' manifest (as per SettingsManifests), they get loaded in that order.

However, if you register multiple files through profile-based configuration (as per SettingsInterface), their order is not guaranteed. Then you need more structure for that: package them as Firefox extensions and load them through ExtensionSequencer.

On change, Bootstrap re-loads all registered files, not just the one(s) updated. That allows dependant files to maintain their book keeping (if you used a 'values' manifest).