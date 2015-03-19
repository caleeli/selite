

# Summary and scope #
These notes about [Selenium IDE](http://seleniumhq.org/projects/ide) are on top of its [standard documentation](http://docs.seleniumhq.org/docs/02_selenium_ide.jsp). This assumes that you have installed all SeLite AddOns. If you develop test scripts, frameworks or plugins, see also DevelopmentTools.

# Auto-generated Selenese commands #
Selenese commands are defined in one of three primary forms: <i>xyz, <b>get</b>Xyz</i> and <i><b>is</b>Xyz<b>Present</b></i>. Selenium auto-generates their variations (listed below).

Selenium IDE shows the original reference for both the primary and auto-generated actions. However, the online reference contains only the primary actions/functions. So if you'd like to locate them online, use the following mapping.

| **Primary commands**<br> (as listed both online and in Reference tab) <table><thead><th> <b>Auto-generated commands</b> <br>(listed in Reference tab only, but not online)                                     </th></thead><tbody>
<tr><td> xyz<br>(implemented by function <b>do</b>Xyz) </td><td> xyz<b>AndWait</b>                       </td></tr>
<tr><td> <b>assert</b>Xyz                              </td><td> <b>verify</b>Xyz                         </td></tr>
<tr><td> <b>get</b>Xyz<br><b>is</b>Xyz (other than <b>is</b>Xyz<b>Present</b>)<br> (rarely useful on its own,<br> use generated commands instead)              </td><td> <b>assert</b>Xyz<br><b>assertNot</b>Xyz </td></tr>
<tr><td>                                                                                   </td><td> <b>verify</b>Xyz<br><b>verifyNot</b>Xyz              </td></tr>
<tr><td>                            </td><td> <b>store</b>Xyz<br>                                       </td></tr>
<tr><td>                            </td><td> <b>waitFor</b>Xyz<br><b>waitForNot</b>Xyz                                </td></tr>
<tr><td> <b>is</b>Xyz<b>Present</b><br>(rarely useful on its own,<br> use generated commands instead) </td><td> <b>assert</b>Xyz<b>Present</b> <br><b>assert</b>Xyz<b>NotPresent</b> </td></tr>
<tr><td>                                                                                   </td><td> <b>verify</b>Xyz<b>Present</b> <br><b>verify</b>Xyz<b>NotPresent</b> </td></tr>
<tr><td>                                                                                   </td><td> <b>store</b>Xyz<b>Present</b> </td></tr>
<tr><td>                                                                                   </td><td> <b>waitFor</b>Xyz<b>Present</b> <br><b>waitFor</b>Xyz<b>NotPresent</b>  </td></tr></tbody></table>

<h1>Selenese parameters (Target and Value)</h1>
<a href='Hidden comment: Comment: Selenese commands accept up to two parameters: Target and Value.
* Target is often a locator (an expression that identifies an element). It can also be a Javascript expression to evaluate (with _getEval_), or something else.
* If Target is a locator, Value is usually an expected or new value, which is compared or entered into element identified by Target. Value can also be a name of a stored variable, or something else.'></a><br>
<br>
<ul><li><a href='http://release.seleniumhq.org/selenium-core/1.0.1/reference.html'>Selenium Core reference</a> and its section on <a href='http://release.seleniumhq.org/selenium-core/1.0.1/reference.html#locators'>Element Locators </a> are handy.<a href='Hidden comment: TODO: Compare to https://selenium.googlecode.com/git/ide/main/src/content/selenium-core/reference.html'></a><br>
</li><li>Back ticks <code>`...`</code> anywhere in Target or Value columns are a part of EnhancedSyntax.</li></ul>

<h2>XPath</h2>
Full XPath locators start with <i>xpath=</i> or with //. Usually an XPath expression starts with //, with which you don't need to use <i>xpath=</i>. However, some SeLite commands (like <i>clickRandom</i> and <i>selectRandom</i>) only accept XPath as the locator, but they require it not to contain any leading <i>xpath=</i> prefix (whether the XPath starts with // or not).<br>
<br>
See resources on XPath:<br>
<ul><li><a href='https://developer.mozilla.org/en-US/docs/Web/XPath'>MDN</a>
</li><li><a href='http://www.w3.org/TR/xpath/'>W3C</a>
</li><li><a href='https://developer.mozilla.org/en-US/docs/XPath/Functions'>XPath functions supported by Firefox</a>
</li><li><a href='http://stackoverflow.com/questions/365750/xpath-sibling-conditional-testing'>XPath siblings</a></li></ul>

<h2>UI-Element mappings</h2>
<a href='http://www.seleniumhq.org/docs/06_test_design_considerations.jsp#ui-mapping'>'UI Mapping'</a> (or 'UI-Element mapping') defines a mapping between meaningful names of elements on webpages, and the elements themselves. Element locators are in forms<br>
<ul><li><i>ui=semanticPageName:semanticElementName(...)</i> or<br>
</li><li><i>ui=semanticPageName:semanticElementName(...)->xpathOffsetLocator.</i>
(The example there is for Java only, while SeLite frameworks define UI Mappings in Javascript.)</li></ul>

See also <a href='https://selenium.googlecode.com/git/javascript/selenium-core/scripts/ui-doc.html'>detailed reference</a>. If you've installed Selenium IDE, you can get the same reference offline through Selenium IDE menu > Help > UI-Element Documentation or at a Firefox URL: <i>chrome://selenium-ide/content/selenium-core/scripts/ui-doc.html</i>.<br>
<br>
<h1>Variables</h1>
<h2>Stored variables</h2>
Some Selenese actions store variables, to be used by further actions. SelBlocksGlobal manages scope of such variables. When inside a SelBlocksGlobal function, you can only use stored variables set in that function (or passed as parameters to it). The local scope also means: if you set a stored variable within a function and the same stored variable exists in the caller scope (that invoked the current function), the variable in the caller scope won't be affected.<br>
<br>
Parameters of Selenese actions can access stored variables as <code>${name-of-the-variable} </code>. Those get replaced by the value of the variable. However, if the action processes the parameter as a Javascript expression (e.g. <i>storeEval, getEval...</i> or when using EnhancedSyntax), and if the variable contains an array/object or a non-numeric string (possibly with an apostrophe or quotation mark), then the replacement won't work robustly. For those cases use <i>storedVars.name-of-the-variable</i> or <i>storedVars['name-of-the-variable']</i>. See also EnhancedSyntax.<br>
<br>
<h2>Javascript variables</h2>
Sometimes you want a 'global' variable that spreads across the functions (which stored variables can't). Use 'direct' Javascript variables for it. Set them using command/action <i>getEval</i> with the target being: <i>variable1=valueOrExpression, variable2=valueOrExpression....</i>

Don't use command <i>storeEval</i> for that - it sets a stored variable, which is local.<br>
<br>
<h1>Limitations of getEval, storeEval</h1>
Command <i>getEval</i> (and derived commands like storeEval - as per <a href='#Auto-generated_Selenese_commands.md'>Auto-generated Selenese commands</a> above) etc. don’t like string literals <i>"\n"</i> or <i>'\n'</i> (or any string literals that contain them). Then they generate a confusing error 'unterminated string literal'. Use <i>String.fromCharCode(10)</i> instead of <i>'\n'</i>.<br>
<br>
<h1>Tips on GUI usability</h1>
<a href='Hidden comment: TODO Check/report: Sometimes, if a Selenium-driven web application opens a new window, there won"t be any vertical scrollbar even if the page is longer than the window view. Mouse scroll wheel won"t work either. You have to click at the window and use page up/down or arrows.'></a><br>
<br>
When saving a test case or a test suite, Selenium IDE doesn't add <i>'.html'</i> to the filename. Add <i>.html</i> extension yourself, so that later you can identify the file more easily.<br>
<br>
<h2>Using multiple Selenium IDEs in parallel</h2>
A running Firefox instance can show only one standard Selenium IDE window. Yet, viewing/editing different test cases in multiple Selenium IDE windows (at the same time) increases productivity. Several ways exist for it, varying in intuitiveness, simplicity and accessibility. Some involve multiple running instances of Firefox, with separate profiles.<br>
<br>
Don't modify same test case or test suite in various Selenium IDE windows simultaneously.<br>
<br>
<h3>One standard Selenium IDE; auxiliary Selenium IDEs inside browser</h3>
This shows one Selenium IDE detached from Firefox browser windows. Other Selenium IDEs are inside browser windows, but they may look standard, too. Compared to the next method, this<br>
<ul><li>(+) is simpler to set up, to start and to maintain<br>
</li><li>(+) involves less maintenance: it runs only one Firefox instance (with one profile)<br>
</li><li>(+) is more convenient: shared bookmarks, window history, add-ons etc.<br>
</li><li>(+-) shares history of recent files in Selenium IDE; however, it gets overwritten by the instance closed as the last one<br>
</li><li>(-) can't run scripts in auxiliary Selenium IDEs (they target their own window/tab). If you modify a script there without saving it and your run a command that changes the current page, your changes will be lost! So you should use auxiliary Selenium IDEs primarily to view scripts (for reference). Auxiliary Selenium IDEs don't load any SettingsManifests neither any <a href='SettingsOverview.md'>configuration</a> sets associated with test suites. (That prevents potential conflicts due to the fact that any auxiliary Selenium IDEs share Selenium Core scope along with the standalone Selenium IDE, if any). Therefore they don't load any <a href='BootstrapLoader.md'>Bootstrapped</a> extensions, either.</li></ul>

Steps<br>
<ol><li>Install <a href='https://addons.mozilla.org/en-US/firefox/addon/stylish'>Stylish</a>
</li><li>Install <a href='https://addons.mozilla.org/en-US/firefox/addon/hide-tab-bar-with-one-tab/'>Hide Tab Bar With One Tab</a>
</li><li>Install <a href='https://addons.mozilla.org/en-us/firefox/addon/hide-navigation-bar/'>Hide Navigation Bar</a> (for usage see below)<br>
</li><li>Restart Firefox<br>
</li><li>Install <a href='https://userstyles.org/styles/110010/selenium-ide-per-tab-coloured-menu-text'>per-tab coloured menu text</a>:<br> <a href='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshots/110010_after.jpeg?r=1424730593'><img src='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshot_thumbnails/110010_after.jpeg?r=1424730593&extensionForGoogleCode=file.jpeg' /></a>
</li><li>Start Firefox and standalone Selenium IDE (by Ctrl+Alt+S, or Firefox menu Tools > Selenium IDE).<br>
</li><li>Display auxiliary Selenium IDEs. For each<br>
<ol><li>open a new Firefox window<br>
</li><li>open one of URLs<br>
<ul><li><i>chrome://selenium-ide/content/selenium-ide.xul#GREEN</i>
</li><li><i>chrome://selenium-ide/content/selenium-ide.xul#BLUE</i>
</li><li><i>chrome://selenium-ide/content/selenium-ide.xul#RED</i>
</li><li><i>chrome://selenium-ide/content/selenium-ide.xul#WHITE</i>
</li></ul></li><li>if you have already opened <i>chrome://selenium-ide/content/selenium-ide.xul</i> and later you add or change the hash part (<i>#GREEN, #BLUE</i>, <i>#RED</i> or <i>WHITE</i>), it won't take effect (even after you hit Enter) until you refresh the URL e.g. by F5 key (which will lose any modifications)<br>
</li><li>hide Firefox navigation bar by pressing F2 (you may need to press it twice)<br>
<ul><li>(+) it applies to the current window and any new windows later, but not to other existing Firefox windows<br>
</li><li>(-) however, after a Firefox restart it applies to all windows; then press F2 to show navigation bar where you want it</li></ul></li></ol></li></ol>

In auxiliary IDEs<br>
<ul><li>optionally, press F11 for full screen mode (this is probably beneficial only if you have more than two physical screens)<br>
</li><li>(-) if you hide Firefox menu, it often doesn't show up when you press Alt key. Then you need to click at the very top of the browser window (which shows <i>testCaseName (testCaseFileName.html) - Selenium IDE X.Y.Z - Mozilla Firefox</i>) and then press Alt.<br>
</li><li>(-) pressing F5 (which reloads Selenium IDE), or closing Selenium IDE tab/window with 'x' icon, applies without any confirmation about unsaved test cases/test suite.</li></ul>

<a href='Hidden comment: Comment:
TODO see http://www.doknowevil.net/2009/04/13/cool-firefox-xul-tricks-with-firefox/
'></a><br>
<br>
There is also Firefox menu > View > Sidebar > Selenium IDE. However, that Selenium IDE sidebar has restricted width. Like Auxiliary Selenium IDEs, Selenium IDE in a sidebar doesn't load any SettingsManifests neither any <a href='SettingsOverview.md'>configuration</a> sets. Please, vote at ThirdPartyIssues > <a href='https://bugzilla.mozilla.org/show_bug.cgi?id=406629'>Sidebars (history, bookmarks) should not have maximum width</a> so that it gets fixed.<br>
<br>
<h3>Multiple standard Selenium IDEs</h3>
This shows multiple Selenium IDEs, detached from Firefox browser windows. Compared to the previous method, this<br>
<ul><li>(-) needs multiple running Firefox instances (and profiles). Each profile each needs an installation of Selenium IDE; ones that run scripts also need their own installations of SeLite AddOns and any other extensions.<br>
</li><li>(+) can run multiple scripts in parallel with separate sessions (cookies)</li></ul>

To set up<br>
<ol><li>Create Firefox profiles, one per Selenium IDE: Follow <a href='https://developer.mozilla.org/en-US/Add-ons/Setting_up_extension_development_environment'>Setting up extension development environment (MDN)</a> > <a href='https://developer.mozilla.org/en-US/Add-ons/Setting_up_extension_development_environment#Development_profile'>Development profile</a>.<br>
</li><li>Start multiple Firefox instances, one per profile, with command line parameters <i>-no-remote</i> and (<i>-P ProfileName</i>).<br>
</li><li>Install Selenium IDE in each profile. Install SeLite AddOns any other extensions in profiles where you will run scripts.<br>
</li><li>Mark the second and successive profiles to identify Selenium IDEs:<br>
<ul><li>Visually by colour<br>
<ol><li>Install <a href='https://addons.mozilla.org/en-US/firefox/addon/stylish'>Stylish</a>
</li><li>Restart Firefox<br>
</li><li>Install styles for the second and further Selenium IDEs:<br>
<ul><li><a href='https://userstyles.org/styles/109886/selenium-ide-green-menu-text'>green menu text</a>:<br> <a href='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshots/109886_after.jpeg?r=1422833554'><img src='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshot_thumbnails/109886_after.jpeg?r=1422833554&extensionForGoogleCode=file.jpeg' /></a>
</li><li><a href='https://userstyles.org/styles/110005/selenium-ide-blue-menu-text'>blue menu text</a>:<br> <a href='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshots/110005_after.jpeg?r=1422833463'><img src='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshot_thumbnails/110005_after.jpeg?r=1422833463&extensionForGoogleCode=file.jpeg' /></a>
</li><li><a href='https://userstyles.org/styles/110006/selenium-ide-red-menu-text'>red menu text</a>:<br> <a href='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshots/110620_after.jpeg?r=1424729821'><img src='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshot_thumbnails/110620_after.jpeg?r=1424729821&extensionForGoogleCode=file.jpeg' /></a>
</li><li><a href='https://userstyles.org/styles/110620/selenium-ide-white-menu-text'>white menu text</a>:<br> <a href='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshots/110620_after.jpeg?r=1424728011'><img src='https://df6a.https.cdn.softlayer.net/80DF6A/static.userstyles.org/style_screenshot_thumbnails/110620_after.jpeg?r=1424728011&extensionForGoogleCode=file.jpeg' /></a>
</li><li>You can switch between styles in Firefox menu Tools > Add-ons > User Styles.<br>
</li></ul></li></ol></li><li>By language<br>
<ul><li>(-) This applies to the whole Firefox instance (rather than just Selenium IDE). That can make it difficult to use!<br>
</li></ul><ol><li>Install <a href='https://addons.mozilla.org/en-US/firefox/addon/simple-locale-switcher/'>Simple Locale Switcher</a>
</li><li>Restart Firefox<br>
</li><li>Install different language packs through Firefox toolbar > 'Simple Locale Switcher' green button > 'Get more language packs...'</li></ol></li></ul></li></ol>

<h4>Custom styles for Stylish</h4>
Use can create or adjust a style in Firefox menu Tools > Add-ons > User Styles > 'Write New Style' and 'Edit', respectively. However, it's not obvious what CSS to use. It's unclear how to change colour of e.g. window border or window grey background (which would be beneficial for intuitive visual identification).