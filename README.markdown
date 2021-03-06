Zotero Browser
==============

**IMPORTANT** This currently will only work in Firefox 3.5 (3.5.9 is the most
  recent version and will be supported with security fixes until August 2009)
  due to upstream bugs with the POW web server.  You can obtain it from
  [Here](http://www.mozilla.com/en-US/firefox/all-older.html).

This is a web based browser for the Zotero bibliographic software
(http://zotero.org). 

The idea is basically to provide an easy to hack environment for
producing custom reports and other useful things for people who want
to use Zotero's excellent data models for building other useful
tools.  While this is possible by creating a new Firefox extension to
interact with Zotero directly, in a lot of situations this is just far too
much trouble.  

Installation
============

Fortunately the "Plain old Webserver" Firefox extension gives us full
access to Firefox's internals including the Zotero API.  You will need
to install this into the same Firefox profile as your Zotero
library. It's available from here:
https://addons.mozilla.org/en-US/firefox/addon/3002.

Once POW is up and running, you can just put the files in this
distribution in a subdirectory in POW's htdocs directory, visit
relevant page (e.g. http://localhost:6670/zotero-browser/) and you're
good to go.

Roadmap
=======

At the moment, all the included scripts is:

  - list the collections in your library.  
  - A rather basic report of each question.  The report uses the jqote2 client side javascript template library (http://plugins.jquery.com/project/jqote2) which makes writing out data super easy if you have basic knowledge of HTML.

*Next Step*: Write an annotated bibliography browser.  Features are:

 - Create annotated bibliography from collection and/or 1 or more tags. DONE
 - List abstracts, notes and related items under each bibliographic entry. DONE
 - List what each item has been tagged with. 
 - List what collections the item belongs in.
 - Jquery magic to make these various lists hide/show for space efficiency.
 - Clickable link for each item to highlight the relevant part of the zotero collection pane (like provided in the timeline view from within zotero).

There's lots of potential for doing other interesting stuff -
tagclouds based on the content of the fulltext stored for each item, a
fulltext based browsable index, getting a JSON based web service up
and running to distribute information about your bibliographies.  The
possibilities are endless.

Tips and Tricks
===============

See annotated/index.sjs and annotated/lib/get_results.js for an
implementation designed to get around the fact that POW doesn't pass
arrays from GET requests properly.

You can get Native JSON support through firefox.  Here's the code required:

 var thing = {"this":"that","something":"else"}
 var json = Components.classes["@mozilla.org/dom/json;1"].createInstance(Components.interfaces.nsIJSON);
 var json_thing = json.encode(thing);
 var other_thing = json.decode(json_thing);

Some of the markup in zotero is not terribly valid (I'm looking at you
TinyMCE!).  This can cause havoc with the templating system jqote2.  To deal
with any issues arising from this, you should escape(html) on the server, and
unescape(html) on the client side in the template.

Source and contributions
========================

This is open source software, and your contribution is encouraged.
You can fork the git repository at
http://github.com/singingfish/zotero-browser

Bear in mind that the Zotero API documentation is also rather sparse,
and working out how to work with Zotero requires significant
javascript skills and quite a bit of source diving at this stage, so
if you work on this, please consider also contributing to the API
documentation at http://www.zotero.org/support/dev/api_user_docs .


Warning
=======

Keep backups of your Zotero library - messing around with the Zotero
API could cause you to inadvertently modify or destroy your collection!

Author
======

Kieren Diment <diment@gmail.com>

Licence
=======

This software can be distributed under the same terms as Zotero.
