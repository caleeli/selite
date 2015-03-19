

See also SeleniumIde > [Auto-generated Selenese commands](SeleniumIde#Auto-generated_Selenese_commands.md).

# Locating Javascript implementation of Selenese 'doer' commands #
Selenese primary 'doer' commands (i.e. ones with primary forms that don't start with _**get**_ neither with _**is**_ as per table in SeleniumIde > [Auto-generated Selenese commands](SeleniumIde#Auto-generated_Selenese_commands.md)) are defined in Javascript functions whose names start with _**do**_. E.g. command _xyz_ is implemented in function <b>do</b>Xyz_. Therefore do not search for them case sensitively._

# Locating a Javascript function in sources #
There are various ways of how to define/set/override a function in Javascript (usually through setting it as if it were a field on the class prototype object). So if you need to debug/modify/extend a function, it may not be easy to locate. You can use the following regular expressions to find definition(s) of a function (if implemented in one of the common ways). Replace _FUNCTION_ with the name of the function.

The regex itself, e.g. for use in NetBeans:
```
function\s+FUNCTIONNAME[^a-zA-Z0-9_]|[^a-zA-Z0-9_]FUNCTIONNAME\s*[:=]\s*function|\[\s*['"]FUNCTIONNAME['"]\s*\]\s*=\s*function
```
The same regex escaped for use in bash:
```
egrep -r "function\s+FUNCTIONNAME[^a-zA-Z0-9_]|[^a-zA-Z0-9_]FUNCTIONNAME\s*[:=]\s*function|\[\s*['\"]FUNCTIONNAME['\"]\s*\]\s*=\s*function" *
```

This is especially useful with Selenium which uses same name functions in various classes/components. There may be various versions of the same class/component, depending on how the code is executed - via Selenium IDE or via webdriver (but only Selenium Core and IDE is relevant to SeLite).

# Defining functions in Selenium Core #
This is for files normally loaded into Selenium Core/Selenese scope (via BootstrapLoader or ExtensionSequencer, which use [JavascriptComplex> mozIJSSubScriptLoader](JavascriptComplex#mozIJSSubScriptLoader.md)). (Those are not [Javascript code modules](JavascriptComplex#Javascript_code_modules.md).)

You can define functions for Selenese scope in either way mentioned in JavascriptEssential > [Defining Javascript functions](JavascriptEssential#Defining_Javascript_functions.md). However, if you use [the classic way](JavascriptEssential#The_classic_way.md), do that only in _strict_ mode. Otherwise the function will be in the Selenium global scope (i.e. outside of Selenium Core/Selenese scope) - then you need to see ExtensionSequencer > [Core extensions loaded twice](ExtensionSequencer#Core_extensions_loaded_twice.md).

# Special rules for custom Selenese commands #

## Action commands ##
Don't have names of Selenese actions (i.e. ones implemented by Javascript function <i><b>do</b>Xyz</i>) start with _getXyz_ (i.e. implemented as **Selenium.prototype.doGetXyz**), unless you have a very good reason. Such names would imply that the command is a 'getter' rather than a 'doer'. They would suggest that there are other auto-generated Selenese commands for them (**assertXyz, verifyXyz, waitForXyz, storeXyz** - as per SeleniumIde > [Auto-generated Selenese commands](SeleniumIde#Auto-generated_Selenese_commands.md)), but those wouldn't exist.

TODO Similarly for other prefixes (as in SeleniumIde)?

## Getter commands ##
Don't define the second parameter (usually called 'value') for Selenese getter commands. See https://code.google.com/p/selenium/issues/detail?id=3202.