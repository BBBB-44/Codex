Do Not Start with a Hyphen: Avoid starting a filename with a hyphen (e.g., -file.txt). Command-line tools may mistake them for command options (like -f or -r), causing issues.

Avoid Special Characters: While hyphens are safe, avoid other special symbols like ! @ # $ % & * ( ) = + [ ] { } | ; ' " , < > / ?.

Use meaningful names:

uml-class-notes.md
csharp-methods.md
interface-overview.md

Date Prefixes

Useful for notes, logs, journals, changelogs.

Examples:

2026-05-07-class-notes.md
2026-05-07-meeting-notes.md

ISO format (YYYY-MM-DD) is best because files sort correctly alphabetically and chronologically.


Underscores because hyphens might exist in original data, like title or author surname. 


Why Hyphens are Recommended
Web-Friendly: Search engines treat hyphens as spaces, helping with SEO, whereas underscores are often ignored.


But the thing I noticed more often that has a big impact in setting for an option imo is the difference when selecting text (use the example above):
Double clicking with the mouse (or using Ctrl+Shift+Arrow Keys) only selects text seperated by hyphens. 

20210918_Bill_daughter-appointment-doctor.pdf

 That's because a hyphen is a word boundary whilst an underscore is not.

The same thing would be true in a regular expression, if your regex uses word boundaries it won't detect an underscore. 
