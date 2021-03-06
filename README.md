# Uncrustify Automator Services for Xcode 4 #

- Author: Tony Arnold, tony@thecocoabots.com
- Requirements: Xcode 4 or higher, Mac OS X 10.6 or higher

## What's it do? ##

These automator scripts allow you quickly reformat your Objective-C code using the brilliant `uncrustify` command-line utility ([http://uncrustify.sf.net/](http://uncrustify.sf.net/)).

A sample Objective-C uncrustify configuration file is available at [http://gist.github.com/261662/](http://gist.github.com/261662/) - just copy or move this file to `~/.uncrustify.cfg` to use it.

## Installation ##

I will assume you have a basic understanding of installing software using a package manager like [Homebrew][hb].

 1. Install **uncrustify**. I use [Homebrew][hb] to do this — `brew install uncrustify` — but you could just as easily do it by hand, or ;
 2. Make sure that **uncrustify** is in your `$PATH` — you can verify this by opening a new terminal window and typing `which uncrustify` — if the full path to your copy of **uncrustify** is printed, you're set;
 3. Copy or move the included workflow files into `~/Library/Services/`.
 4. Open the "*Uncrustify Document*" using Automator, and update the line beginning with `set formatted_source` in the "*Run AppleScript*" block to reflect the path to your copy of uncrustify. It should look something like:
    `set formatted_source to do shell script "/usr/local/bin/uncrustify -c ~/.uncrustify.cfg -l OC -f " & quoted form of current_document_path`
 5. Do the same for the "*Uncrustify Document and Re-Indent*" automator workflow
 4. Open the "*Uncrustify Selected Source Code.workflow*" documents in Automator, and update the "*Run Shell Script*" block to reflect the path to your copy of uncrustify. It should look something like:
    `/usr/local/bin/uncrustify --frag -c ~/.uncrustify.cfg -l OC | cat`

## How do I use it? ##

### A word of caution ###

Uncrustify will write over your source files with it's changes without asking you if you choose to operate on an entire document. If you want to see what changes will be made without writing over your files, select all the code in your current Objective-C file and use the "*Uncrustify Selected Source Code*" service.

The "*Uncrustify Selected Source Code*" will only work with Objective-C documents due to the presence of the `-l OC` argument in the workflow script.

The "*Uncrustify Document*" service will first save any changes you've made to the frontmost source document, and then run it through uncrustify. It will also only work with Objective-C source code documents.

The "*Uncrustify Document and Re-Indent*" service will first do the same thing as the "*Uncrustify Document*" service, but will then use Xcode's own "*Re-Indent*" function, which should mean that your final document format's indenting will match Xcode's editing style. It will also only work with Objective-C source code documents.


### How to ###

1. Open a document (or multiple documents), or select text in an already open document;
2. Go to the **Xcode** menu, then select *Services* and make your choice from the scripts starting with "*Uncrustify...*".

Your file's contents will be updated immediately.

## Copyright ##

Copyright 2010—2011 Tony Arnold. See LICENSE for details.


 [hb]: http://mxcl.github.com/homebrew/
