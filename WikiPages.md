

# Navigation, labels and filters #
Pages are sorted and filtered by navigation labels
  * GeneralImportance: important for most readers .. important for a few
  * Technicality: least technical .. highly technical
Those levels are represented visually by X..XXXXX.

# Terminology #
Since Selenium and SeLite are not test-specific, documentation calls test cases or suites _scripts_. They're called <i>Selenese scripts</i> when there's a need to differentiate them from Javascript or other scripts. Some other terms are at TestMethods and TestMethodsTheory.

# Documentation scope #
Wiki describes the mainstream use cases, handled in the most common ways. For more information see PackagedTests or the source code. Then you can experiment.

Documentation doesn't cover general functionality of related technologies (see also [ReportingIssues](ReportingIssues.md) > [Support scope](ReportingIssues#Support_scope.md)). If SeLite elaborates on those topics, it's only if they are not clear or obvious from their original documentation source, or where SeLite modifies their features. Such notes and some references to third party documentation are at [Selenium IDE](SeleniumIde.md), DevelopmentTools, JavascriptEssential, JavascriptComplex, InstallFromSource.

# Firefox _chrome://_ URLs #
Some of SeLite GUI is accessible via special Firefox URLs that start with _chrome://_ (which don't work in other browsers). Such links can also show source of SeLite and its Selenese references.

The documentation presents such URLs text _in italics_, but not as links. That's because Firefox doesn't allow linking to them from the internet. <a href='Hidden comment: Comment: Even if you make chrome:// a link by putting it between [], you save .wiki locally and you open it in Firefox with Wiki Viewer, Firefox will not follow such link. Also, googlecode wiki doesn"t allow such URLs either.'></a>

# Comments #
By submitting a comment you agree that project administrator(s) can, without notice,
  * edit your comment, or
  * incorporate your comment into SeLite documentation, under the current or any future license of SeLite documentation, or
  * remove your comment.

# Format #
Most user documentation goes to wiki. Implementation documentation is mostly in the source comments, and some in wiki.

Detailed descriptions of Selenese commands are in reference files (outside of wiki). You can find them
  * online - see AddOns
  * in Selenium IDE reference pane (once you type a chosen command in IDE).

Why using wiki for user-facing documentation? See WikiStandard. Also, read that before reading any other internal pages.

If you read [Object Diagrams](https://code.google.com/p/selite/w/list?q=label:ObjectDiagram), you may want to see WikiStandard > [Textual object diagrams](WikiStandard#Textual_object_diagrams.md).