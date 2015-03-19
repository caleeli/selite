
# Why wiki for user-facing documentation #
## Other formats ##
It could be nice to have user/tester-facing documentation in a format that can be exported as HTML, PDF etc. [Selenium Documentation](http://code.google.com/p/selenium/wiki/Documentation) uses [reStructuredText](http://docutils.sourceforge.net/docs/user/rst/quickref.html). That needs special escaping of ${...}. It also didn't compile some pages (see [Selenium issue #5582](http://code.google.com/p/selenium/issues/detail?id=5582)). So all SeLite documentation goes to wiki, until there is something well proven to be more robust, practical and worthwhile.

## Benefits of wiki ##
  * hands-on, one source simple documentation in one place seems better
  * even if we had the documentation separate, we still need wiki (project website tabs have to point to wiki pages)
  * side navigation (TableOfContents), tags, sorting and filtering
  * simple syntax, based on MediaWiki and a bit similar to Confluence
  * edit online
  * edit offline
    * in a plain text editor (or NetBeans)
    * preview using
      * [Wiki Viewer](#Wiki_Viewer.md)
      * [Offline Editor](http://wikignpi.googlecode.com/hg/jquery-preview-ed.html) (not as practical as Wiki Viewer)
      * another option: [google-code-wiki-to-html](http://code.google.com/p/google-code-wiki-to-html)
    * then publish online by git
  * good integration with the project website. Wiki allows any number of label groups (prefixes) and it shows them as columns in the listing of the pages. We can have links that lists pages filtered by labels, which simplifies user's navigation.

One reason for not using GitHub is that its issues management doesn't allow users to attach files other than images. That goes against [ReportingIssues](ReportingIssues.md).

## Maintaining the documentation ##
Update TableOfContents (the navigation sidebar) if you
  * add or rename/split/merge a public page, or
  * change Technicality label of a page, or
  * rename any label used in TableOfContents (e.g. [ObjectDiagram](https://code.google.com/p/selite/w/list?q=label:ObjectDiagram))
And
  * Write and organise contents clearly.
  * Make it easy to read.
  * Make it hands on: provide examples.
  * If it seems to grow big, suggest new label groups and filters
  * Don't have any content before the first heading (<i><code>=</code> Heading... <code>=</code></i>)
  * Refer to third party documentation if you mention something for the first time (if you have a reference).
  * Don't use XML-like `<br/>`, because it adds several extra new lines. Use `<br>` instead.
  * Don't list pages with label Technicality or GeneralImportance set to 'Internal'.
  * Spread label values X..XXXXX more-less even.
  * On ThirdPartyIssues, spread values of Importance column even, too.
  * use `<wiki:toc max_depth="2" />` (or with a different level), except for very short pages with no sections/headers. Then have a header before the first paragraph, otherwise it may be overseen.
  * don't use CamelCase to auto-link in headers `=..=, ==...= etc.`. They render well in Wiki Viewer, but not online.
    * contents of such pages should not start with a paragraph, but with a heading. Otherwise the first paragraph is not in any part of TOC and it looks confusing.
  * I don't use fixed line length, especially not in wiki page sources. In code I split expressions on multiple lines if they are quite complex. A good IDE/editor should be capable of wrapping lines, so you can benefit from all your available screen area and not worry about line lengths. Also, having longer lines is better when you search for something, as seeing the matches in the search results may give you enough information (e.g. you know you don't need to change that occurrence), which saves you opening that line in editor. I suggest NetBeans. There choose menu Tools > Options > Editor > Formatting > Line Wraps: After words. If you want Eclipse try http://dev.cdhq.de/eclipse/word-wrap/ (install both components: word wrap and line numbering fix); however, line numbering fix (for Eclipse Kepler) doesn’t work in Eclipse Luna (4.4).
  * format any chrome:// (or javascript:) URLs in _italic_ but don't make them links. See WikiPages > [Firefox \_chrome://\_ URLs](WikiPages#Firefox_chrome://_URLs.md).
  * have ``_`code example`_`` instead of ```_code example_```. The later doesn't show up well in Wiki Viewer extension for Firefox.
  * beware that the following don't show up in Wiki Viewer
    * back tick (back apostrophe) ````` - which needs to be escaped between `{{{` and `}}}`
      * if backticks are unpaired, Wiki Viewer reports a warning even if they are escaped by `{{{` and `}}}`
    * curly bracket `{` or `}` - which need to be enclosed by back ticks `````

### Wiki page names ###
Always have wiki page names (file names) in CamelCase. Then you can benefit from autolinking in comments of [project's issues](https://code.google.com/p/selite/issues/list).

Keep page names short:
  * So that navigation can show Technicality rating next to them.
  * Have page name + technicality level (number of X's) long maximum 22 letters. If it was more, navigation didn't render well in Firefox and Google Chrome at some zoom levels.
  * Alternatively (but not ideally), use shortcuts rather than full page names in the navigation.

Use page name as the link text (i.e. use CamelCase auto-linking) as much as possible. Exceptions are:
| **Page name**            | **Link text** |
|:-------------------------|:--------------|
| <i>Abc</i>Framework    | _Abc_ |
| SelBlocksGlobal       | SelBlocks Global (on some pages) |
| ExtraCommands         | Commands |
| BootstrapLoader       | Bootstrap |
| SettingsOverview      | Settings |

### Wiki Viewer ###
[Wiki Viewer](https://addons.mozilla.org/en-us/firefox/addon/google-code-wiki-viewer/) is an add-on for viewing wiki pages in Firefox. You can open .wiki files through menu File > Open File..., or navigate to them through _file://_ URLs. If you edit many pages simultaneously, try Firefox menu View > Sidebar > Google Code Viki Viewer.

Using Wiki Viewer can be more robust and practical than editing online, but you need some workaround with it:
  * it doesn't auto-generate links for `CamelCase` page names (e.g. ProjectHome) and for URLs (i.e. http://seleniumhq.org/projects/ide doesn't auto-link in Wiki Viewer)
  * it creates links for `[anyPageName]`, but incorrectly. After you follow such a link, you need to append `.wiki` to the URL.
  * special characters in headers: Wiki Viewer and code.google.com treat some special characters (e.g. colon :, slash /, apostrophe ', dash - or a combination of a space and underscore) differently in headers = ... =, == ... ==, === ... === etc. Wiki Viewer produces anchors for such headers different to those from code.google.com. That matters if you link to such headers from other pages (or from outside of wiki). E.g., link to [WikiPages#Firefox\_chrome://\_URLs](WikiPages#Firefox_chrome://_URLs.md) is correct (it works online), but it doesn't work in Wiki Viewer (even after you adjust it to use .wiki). (Special characters in headers also affect links that come from `<wiki:toc max_depth="1"/>, <wiki:toc max_depth="2"/>, <wiki:toc max_depth="3"/>...`: the links then work within Wiki Viewer, but not online. So check such links to _#anchors_ before using them).
  * if you have a URL not within `[...]`, and it contains underscore(s), you'll get WIKI PARSE WARNING: unterminated `'_'`!
  * when you disable automatic links with exclamation mark !, Wiki Viewer still shows that '!'
  * it generates syntax warnings even if there's no problem
  * `<code>...</code>` doesn't render well
  * It renders content of `<wiki:comment>...</wiki:comment>` as normal text. To make it clear that it's a comment, start its content with _Comment:_, e.g. `<wiki:comment>...</wiki:comment>`.
  * `<pre>`...`</pre>`: if you have blank lines there, type at least one space in each. Otherwise wiki splits it into paragraphs and messes up indentation by one character.
  * If you want to render a back apostrophe, use {<b></b>{{`}}<b></b>}...{<b></b>{{`}}<b></b>}. It doesn't render well in Wiki Viewer, so check it online.
  * if unsure, see [wiki syntax](https://code.google.com/p/support/wiki/WikiSyntax) or copy & paste .wiki source into online editor and preview it

### Labels 'Technicality' and 'GeneralImportance' ###
'Technicality' indicates the minimal technicality level of audience for whom the topic is relevant.

'GeneralImportance' means how likely a user from a mixed audience will benefit from the topic. It doesn't reflect whether the coverage of the topic is simple or complex, or whether the topic is technical or non-technical.

GeneralImportance correlates a bit to reverse of Technicality. However, having both labels makes navigation easier, especially for first time or infrequent visitors.

Those labels have values X..XXXXX (or 'Internal'). I have tried to use gradual verbal values instead. But using words can be ambiguous. It also made listings of pages too wordy and harder to grasp. Using X....XXXXX is quite visual, therefore more intuitive. It lets the user focus on the goal of their navigation, rather than on interpreting words.

The values X..XXXXX are not 'exact'. They are adjusted a bit, so that the pages are spread somewhat even. That eases the navigation.

### Drawn diagrams ###
Make these nice. Draw them in LibreOffice/OpenOffice and save them as .odg. Then Edit > Select All; File > Export (export the selection, rather than the whole drawing area). Export as a .png, not interlaced, with lowest compression. Then commit both .odg and .png to git (TODO change? - test https links first: code repository, not wiki repository). In wiki use URLs to the .png images from git (https://code.google.com/p/selite/source/browse/diagrams > navigate to .png file > get the url of link 'View raw file').

#### Versions of LibreOffice ####
  * LibreOffice version that came with CentOS 6.4 didn't export as .png well - the quality was low.
  * CentOS 6.5 has LibreOffice 4.0.4.2, which is better than one from CentOS 6.4, but it still doesn't export very well.
  * LibreOffice 4.1.3.2 that came with Fedora 19 KDE worked well.
  * Fedora 20 KDE has LibreOffice 4.1.4.2, which renders well.

Please
  * follow http://www.slideshare.net/otikik/how-to-make-awesome-diagrams-for-your-slides
  * use colours black, Chart 11 for red, Green 4, Chart 12 for blue, Chart 3 for yellow

I think using any UML tools is more restrictive and less efficient. <a href='Hidden comment: That"s why I didn"t consider using e.g. http://plantuml.sourceforge.net and http://sourceforge.net/projects/plantumlnb'></a>

### Textual object diagrams ###
[Object Diagrams](https://code.google.com/p/selite/w/list?q=label:ObjectDiagram) draw ownership/reference relationships between objects, fields and functions. They usually don't necessarily describe class inheritance (which is clear from the source<a href='Hidden comment: (Comment: TODO: and from Javadoc'></a>).

Text diagrams don't need to be esthetic, but clear and easy to edit - so you can quickly update them whenever you change the relevant code. They are in plain text, with <b><, >, <code>^</code>, v</b> for connections. The diagrams look like this:<a href='Hidden comment: (Comment: Read this online)'></a>
<pre>
Example                                       Description<br>
<br>
ObjectConstructorName                         Full name of the 'class' - the constructor function of the object.<br>
Below the object constructor name are object fields. Indent them with two spaces.<br>
<br>
.fieldName                                  Field with a fixed (known) name. Prefix it with a dot.<br>
<br>
[ index description or expression ]         Dynamic field name.<br>
<br>
[ ObjectConstructorName.SECRET_FIELD_NAME ] Field with a fixed name, not referred to via a string/numeric literal across the code,<br>
but rather as a value of a defined constant.<br>
</pre>

#### Format ####
The simplest way is to have whole diagrams within `<pre>`...`</pre>`. Don't use {<b></b>{{...}}<b></b>}, since it adds some automatic highlighting, which won't make much sense for our graphs; it also shows horizontal scrollbars for long lines. Don't use {<b></b>{{...}}<b></b>} or `````...````` for parts of a line, because it ignores multiple consecutive whitespace.

So if you'd like to use formatting, links etc., you have to alternate `<pre>`...`</pre>` with wiki/html sections. But it's difficult to format those wiki/html sections to match formatting of the pre-formatted parts. It would also make wiki pages more difficult to edit (it's less WYSIWYG).

If you use [Wiki Viewer (Firefox add-on)](https://addons.mozilla.org/en-us/firefox/addon/google-code-wiki-viewer/) for checking these diagrams, note that
  * it will render `[`index description or expression`]` incorrectly (as link), unless there is a space after `[` and before `]`
  * it doesn't render `^`
  * it doesn't like blank lines (even if they contain a space)

# RSS XML Feeds #
As [reported by others](https://groups.google.com/forum/#!msg/mapsforge-dev/Nd8gt78CfVQ/tlAVDmJDA4MJ), GoogleCode git feeds are for whole repositories and not per document or branch. So I use http://www.feed43.com for page-specific feeds.

# Maintaining the list of third party issues #
Ideally, ThirdPartyIssues > 'Importance' means importance to vote for it, not importance of the issue itself (both from the perspective of SeLite). An issue may have enough votes/stars already to get dealt with - then it would be lower on the above list than issues that are less important for SeLite but that don't have sufficient votes/stars to get actioned.