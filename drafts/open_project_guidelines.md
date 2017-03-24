Software Project Guidelines 2017A
=================================

(C) Daniel Dunn 2016,2017.

Introduction
============

This document intends to be a general reusable template for a coding, contributing, development process, and style guide for open source projects that is independent of any particular project or language.

Attribution
-----------

All code or other data taken from third party sources should be properly attributed and included in some kind of credits page or file, accessible to the user if the program is a GUI application.

This includes cases where it is not legally necessary, such as code that has been explicitly released to the public domain. Attributing all contributions not only helps authors get proper credit but may assist with debugging later.

One-line fragments copied from the internet should have a URL link to their source directly in the code, along with a comment indicating the author.

Versioning
----------

One of the following two versioning conventions should be used.

#### Time-based versioning

If this option is used, the version number should be the year, some seperator mark, and a number. The second release of the 2016 would then be 2016 v2, or 2016 update 2.

Development editions should have the word "development" after them, likewise with alpha, beta, etc.

#### Semantic Versioning

If this option is used, the version number for a stable release displayed to be read by humans should be of the form MAJOR.MINOR.PATCH, using a slight modification of [Semantic Versioning](http://semver.org/) by [Tom Preston-Werner](http://tom.preston-werner.com/)

MAJOR numbers indicate breaking changes, MINOR numbers indicate new features, and PATCH numbers indicate bugfixes. "Breaking changes" should be interpreted with respect to specs and documentation, unless there are a lot of programs depending on a bug, bugfixes are never breaking if they do not change the spec.

The modifications that should be used are:

-   It is acceptable to leave off the patch number if it would otherwise be zero.
-   Incrementing the major number is acceptable even if the program is fully compatible with the old version if enough major changes or rewrites exist that hidden backwards incompatibilities are likely.
-   Pre-release versions should use the names "development", "alpha", "beta", and "rc"
-   Only bugfixes should be made after the beta stage
-   Only "safe" bugfixes or fixes for very important bugs should be made in the release candidate stage.
- Minor releases may include beta features that may change or be removed without incrementing tha major number so long as the release that introduced the feature domuments that the feature is subject to change.

- If that documentation is removed at any point, from then on the feature must be considered stable and no backwards-incompatible changes to it may occur without a major number increase.

"Browser marketing style" version numbering where the major number increments for every slight change is not acceptable and should never be used.

"Desktop-like" software, GUI programs, anything meant to be directly used by an end user(Including CLI programs), programs meant to interact with hardware devices, and libraries meant to read or interpret data or document files should maintain backwards compatibility with old saved data as much as possible even across major-numbered versions.

Distributions should create separate packages for each major version and only rarely increment it(see python2 and python3).
Backwards compatibility should not be broken lightly.

Distributions and packages of libraries should never modify the meaning of existing names. If foo originally symlinked to foo1, it shpuld continue to do so even after foo1 is obsolete.

To allow for one version of a program to use either version of a library if it is available, packages may provide symlinks of the form foo2,3 meaning "Either foo2 or foo3, whichever is newer unless configured otherwise", or "foo2-4" meaning "Any foo between 2 and 4"

**You should never rely on a version number as your only indication of compatibility.**

Version Control
---------------

Unless there is reason to do otherwise, [Git](https://git-scm.com/), a Git hosting service like GitHub or GitLab, and something along the lines of the GitFlow workflow should be used for version control. Projects should use the master branch for stable releases, and have a separate branch called "develop" for the active development branch.

 A basic summary is that new features should begin as branches from develop and be merge-rebased back into develop. When ready, a testing branch off of develop should be made, to which only bugfixes are allowed, before it is finally merged(not rebased) into master. The final version number increment, etc should be done directly in master.

Bugfixes should be back merged using merge-rebase into develop.

See the GitFlow model by [Vincent Driessen](http://nvie.com/about/) for details.

Planning
--------

Any section of code that is missing something or should be changed or re-examined should have a comment marked with todo: 

A git hosting service with a wiki and an issue tracker supporting comments, and planning and discussion for bugs and new features should take place there.

General discussion should take place preferrably on a forum-like platform as opposed to a mailing list, unless the discussion is primarily aimed at a core group of developers with relatively few "drive-by" pull requests.

Build scripts 
--------------

Anything that requires conversion from one format to another before releases(Such as any tool-generated source code, compiled code, etc) should have that process automated, using either make or a shell script.

There should be a file named releasing.md in the repo detailing all steps needed to create an official release of the software.

Change Logs
-----------

Every new feature, bug fix, or refactoring shall be accompanied in the same commit by an entry in the relevant change log. 

Small projects should have one change log file containing the entire history. Larger projects should have one change log per version, in their own folder, and with each log file named after the version that introduces the changes in the log.

Change log entries should usually be short one line descriptions.

Change logs should be kept in .txt or markdown formats.

Tests
-----

Every new feature should include an automated or semi-automated means of testing said feature, and every bugfix should include a test against regression of that bug. but for difficult to test things such as the UI, this is not an absolute requirement.

Individual unit tests are nice to have but are not required except for particularly important sections or things known to be highly prone to regression.

Tests should never be removed so long as the thing they are testing is included, even when you are sure the code they test is correct.

Formatting and Style
--------------------

These styles are meant to be considered as "defaults" for projects not using some other standard. Where a language has a generally accepted style convention, that style should be used instead.

In C like languages, either the  [K&R](https://en.wikipedia.org/wiki/Indent_style#K.26R_style), GNU, or Allman styles should be used, with GNU avoided if automated formatting tools are not available.

In Python-like languages, PEP8 should be followed loosely as a general guide, but use of camelCase should be considered fully acceptable, especially for projects that also contain Arduino code.

"Hungarian Notation" of any kind should be avoided, as should most names containing both underscores and capitalization.

Names should not begin with a capital letter unless they are classes or types, even if they are acronyms. In contrast to the advice of PEP8, when using CamelCase, only the first letter of acronyms should be capitalized.

Avoid multiple statements or assignments on one line, and limit functions to 80 lines each at most if possible.

### Commenting and Documenting

Reliance on "Self documenting code" should be avoided, as it often assumes the reader has an understanding of the system that he or she might not actually have.

Instead, code should be commented extensively, with nearly every function having at least a line or two describing what it does.

Specific comment formatting requirements are to be avoided except for when automated documentation generators are used.

but comments should document the meaning and type of every parameter and returned element that is not obvious within a few seconds of looking at a function.

Developer documentation (Except public APIs)on smallish projects should be kept inside the code as comment blocks and docstrings as much as possible.

End user and public API documentation should be maintained in the repo as md, rst, or HTML documents. 

Long Lines
----------

No line should contain more than a few individual operators or function calls. Instead, well named or commented intermediate values should be used, and comments should also be used if the function is nontrivial.

Plugins
-------

Systems having many functions that perform the same class of task should separate tasks into plugins. Plugins should be designed so that they can easily be removed without affecting the rest of the system.

Examples of systems where this pattern is relevant are importing multiple file types for the same basic data, getting the same kind of data from different kinds of services, or performing the same kind of interaction with different hardware devices.

"Large" GUI applications should have "Tools" plugins in a tools menu with the capability to show arbitrary dialog boxes and perform arbitrary operations on the current loaded data.

Plugins should not load the entirety of their code at startup, and should be indexed and listed at startup and load as needed.

Cloud Dependence
----------------

Systems should not depend on the cloud for any task not involving communication, backup, or some other task that fundamentally cannot be done locally.

Systems should not depend on cloud applications that cannot be self-hosted at all. An exception is services like GitHub to which many alternatives are available, and which is widely accepted as the standard.

This includes development, build process, editing, and all other aspects of the system.

Proprietary Software
--------------------

Systems should not in any way depend on proprietary software for operation or development, or for editing of any resource file.

One exception to this is proprietary drivers and firmware blobs required for correct hardware functionality. These can be considered part of the hardware itself, although the writing of free drivers is still worthwhile.

Another exception is proprietary cloud services, but only where a free equivalent is readily available.

Libraries
---------

Where practical, code should not be written if someone else already has. Try to avoid duplicating code that exists in libraries somewhere. If practical, you should fix buggy or badly performing libraries instead of writing your own.

Including libraries directly in the project should be acceptable and should be preferred where a modified version of a library is needed.

Libraries should provide the most basic functionality with as little code as possible. A simple example should be possible in five lines or less for as much of the major functionality as possible.

User Interface
--------------

### Notifications

Applications should not send the user excessicve notifications. For instances where there is any doubt as to whether the user will want a notification, a configuration option to disable it should be provided.

### Windowing

Multi-window interfaces should be avoided, and support for tabbed editing should strongly be preferred for all editor-like programs.

Dockable dialogs that can be closed should be re-openable in less than 4 clicks.

### Hiding and pagination

The "click to show more" pattern must always be avoided when there is sufficient space. There should never be a "click to expand" box with nothing below it.

Overflow menus of any kind should not be used unless necessary.

Tabs should be preferred to accordion-style interfaces.

### Shortcuts

Applications should not use keyboard shortcut as the sole means of exposing functionality unless those shortcuts are commonly accepted(ctrl-c, ctrl-v, ctrl-x, ctrl-y, etc).

Keyboard shortcuts for common functions should only use the control key and should not use more than 2 keys in a shortcut.

Undo should be mapped to ctrl-z, redo should be mapped to ctrl-z, redo should be mapped to both ctrl-y and ctrl-shift-z, but ctrl-y should be used if both cannot be.

ctrl-c, x, and v should be copy, cut, and paste respectively.

The space bar should play or pause the active media file.

Backspace should not be used for backwards navigation, nor should it be used to delete the selected element in contexts where a backwards navigation action also exists, unless there is a multi-level undo.

A right click should nearly always invoke a context menu on the selected element.

Single clicks should usually just select and double clicks should activate a given element.

See [Wikipedia](https://en.wikipedia.org/wiki/Table_of_keyboard_shortcuts) for a general idea of common shortcuts. Most of the ones listed are not well known enough to serve as the only means of access to a feature.

### Confirmation

Dangerous functions such as delete should never be implemented without a confirmation dialog or an undo function of some type.

### Fancy web design technologies

In general these should be avoided. Pages should use as much plain static HTML as possible with as few HTTP requests as possible.

Pages that show different content on mobile and desktop should be avoided. If possible all mobile-specific sites and "responsive" should be avoided in favor of one site design that works on both desktop and mobile, without actively modifying the page beyond what is possible in pure CSS.

JS based dropdown menus, most single page apps, etc should all be avoided.

Once loaded the page should not move around if possible. Setting the scroll position via means other than anchors should be avoided.

Page numbering should always be from oldest to newest, to avoid as much as possible the case that new pages added change the meaning of existing page numbers.

Where entries are always inserted at the end of a list, and content will persist for months or years, page numbers should have a persistant meaning of "The first n entries after X" so that pages will always contain the same content unless an entry on that page specifically was deleted.

### Scrolling


Endless scrolling should almost always be avoided in basically *any* context, except where older content is unlikely to ever be relevant at any point in the future. Discussion forms and blogs should especially avoid it.

No one element should need to scroll both vertically and horizontally except for display of large images and maps.

CSS
---

As much as possible, CSS stylesheets should avoid using class names and ids and should rely on semantic markup and structure. See "Reusable CSS Classes" for what to do in other cases.

Errors
------

The user should always be presented with full debugging information when an unusual error occurs, and all errors should be logged or output to stderr or a GUI display or at least have an option to be output in such a way.

Exceptions should be prefered over return values to indicate errors,unless there is a specific reason.

Things that are not actually errors that are likely to occur often in normal use, such as "No new data" can be indicated with return values instead. An example would be a function that retrieves the latest data from a sensor, or else Null if no new data has been recieved.

Disk IO
-------

The disk should not be written to unless needed. Anything not user-critical or very large should be maintained in RAM until the application exits, the user manually saves, or some sync interval passes. Things like documents the user is editing may be saved immediately on modification, but things like the current window position and simple settings that would take less than a few seconds to redo should stay in RAM until the app exits.

Things that may be changed extremely frequently, such as scrolling position in a text editor should especially not write to disk when not needed. Frequent unneeded disk writes increase vulnerability to power-loss corruption on some filesystems, increase wear on SSDs, and can even reduce performance if they in extreme cases.

This also applies to embedded software that can write to flash. Anything that is likely to be frequently changed(More than once per day, or 10x per day with higher endurance EEPROM) should probably not be saved without a manual command.

Features like storing the last mode automatically on power off should either not be implemented at all, or should use battery backed ram.

Most RTC chips have several dozen bytes of ram that may be used for this purpose.

Things like window or UI element size and position, Unimportant log entries, and the like should be maintained in RAM and written when the application closes, or not written at all. 

Simply opening a document in an editor should not cause a disk write.

Files and Folders
-----------------

Applications should never crash if a log or cache file is deleted, and should simply create the missing file. Applications should as much as possible use default settings to replace files, except where doing so might create a security error.

A warning should always be printed whenever a missing or corrupt file is detected.

Files with no extension should be avoided except for executable files.

Important files should be protected by the backup-before-write or the atomic rename pattern. In the (POSIX only without special API calls) atomic rename pattern, you write the new file into a temporary file and rename it to the same name as the old file had, which on some systems can be used as an atomic replacement operation.

In the backup-before-write pattern, a copy of the file is made before editing and deleted after completing the changes to the original file. The backup file should have the same name as the old one, but with a tilde ~ appended.

With this pattern there is no easy way to detect which file is the correct one, the backup file or the original. To resolve this, the files can contain checksums or a simple fixed marker at the end. Fixed end markers have the advantage of allowing hand-editing but cannot detect corruption.

You can also use a third file, the same name as the original with a tilde and an exclamation point appended may be used. This file should be created after finishing the backup copy but before starting to write to the original, and deleted with the backup file. If it exists, regardless of contents, you know the backup completed successfully.

### Configuration Files
Applications that provide background services should use directories instead of individual files for configuration, scripting, etc, and should process files within them in sorted alphabetical or ASCIIbetical order.

This allows easier management by automated tools, as it is easier to add a file to a folder than it is to automatically modify and restore a file, and also takes advantage of built-in filesystem locking and atomicity. In general, when exposing an API based on a file, consider if a folder would be more appropriate. An example is the way that [systemd](https://www.freedesktop.org/software/systemd/man/systemd.unit.html) uses unit files in folders instead of cron's normally single crontab per user.

Files without a specific extension should be ignored in such folders, allowing for the create-rename atomicity pattern.

Applications should never crash if a log or cache file is deleted.

Files with no extension should be avoided except for executable binary files. If you don't want an extension on an executable script file, use a symlink to a file with the proper extension if the application supports it.

Time and Date
-------------

2 digit years should not be used in any context, and binary Timestamps should be more than 32 bits.

Dates should be in ISO YYYY-MM-DD, or else the month should be named instead of referred to by number. When a named or abbreviated month is used with a 4 digit year, any ordering of the components can be easily disambiguated.

Times should be in HH:MMam/pm format. Times with no am/pm marker should be assumed to be in 24H time.

Time zones should use Olson/IANA naming, e.g. *Europe/Paris*

Binary times should use the UNIX epoch.

All timestamps in applications and file formants should support at minumim millisecond resolution, and should support dates in the distant past if there is any possibility of the format ever being used with historical data.

Data Formats
------------

Files storing hierarchical data besides markup should use JSON, YAML, or a binary format.

Configuration files should either use INI-like, YAML, delimiter-separated, scripting language source, or plain text, with the extension .conf being preferred for INI-like files.

Shell utilities where practical should use [JSON](http://www.json.org/), [YAML](https://en.wikipedia.org/wiki/YAML) or CSV as their input and output.

Hierarchal data should not be represented in custom machine-readable text formats, nor should XML be used for anything other than document-like structure.

Log files should support gz or b2z compression.

Where the packing of large numbers of files is needed, ZIP should be used unless features not present in ZIP are required. Custom formats that act as containers for other files should use the ZIP format as a basis.

Images should nearly always be stored as SVG, PNG or JPG except for legacy compatibility. As PNG is lossless and supports uncompressed blocks, it is almost always preferable to BMP.

SVG images should be preferred in documents and web pages, and anything originally created as vector art.

Formatted text should generally use Github Flavored Markdown, ODT, or HTML.

Applications should not make unnecessary use of SQL or SQLite databases, or of XML based storage backends; readable text files should be used  instead unless relational semantics or transations are needed.

Custom formats requiring metadata should store said metadata as a YAML or INI-like header, delimited with the standard YAML document delimiter of three dashes on their own line. Three dashes on their own line should generally be the standard "document separator"

New custom formats should always support extensibility, either by chunks containing type identifiers, reserved heirarchy namespaces, or some other means. Custom formats should contain a version identifer.

Custom binary formats should contain "magic number" identifiers of at minimum 8 bytes.


Documentation should be kept as either markdown or HTML, with the latter only used if it is intended to be displayed via the web in some way.

Documentation that is intended for print and must be formatted a specific way should be maintained in ODT format, however this should be avoided if possible due to the difficulty in merging such files, and markdown,rst, plain text, etc should be preferred.

Identifiers
-----------

### Global Identifiers

Software objects that have any identity outside the scope of one instance of one program, or may theoretically have an identity outside one instance of one program, should use either UUIDs,XML/Java/DBus/etc style [reverse dns names](https://en.wikipedia.org/wiki/Reverse_domain_name_notation) like "com.example.foo.bar", [URNs](https://en.wikipedia.org/wiki/Uniform_Resource_Name), [EUI numbers](https://en.wikipedia.org/wiki/MAC_address), or user-assignable free-text names or numbers as their primary identifiers.

As EUI numbers require a central authority they should not be used except where their small size is critical.

Identifier schemes may support more than one of the above choices.

The suggested method for supporting multiple schemes(Such as data or plugin types, device models, node identifiers, file numbers, etc), is to allow both reverse-dns entries and URNs, disambiguating via regexes, and treating anything that is not valid as one or the other as a local-use only identifier. Anything that does not contain at least one . cannot be a reverse-dns entry(Unless you allow root zones as identifiers), and anything not contaiing a : cannot be a URN, and colons generally never appear in reverse-dns names.

UUIDs can be used in this way via the urn:uuid URI scheme.

Non-standard URI schemes should be avoided for the most part, however URI-like formats not intended to be part of the URI namespace but using the same or a similar format bay be used for internal use(e.g. "playsound:beep" as some kind of action identifier in a game.)

Use of schemes involving obtaining a number from the vendor of the software should be avoided, as should use of small numbers as the primary ID of objects in file formats. Device IDs should never use small numbers.

Objects that exist in a global namespace should support titles or aliases if they are ever to be displayed in a list seen by humans. Devices intended as peripherals(External storage, controllers, etc) should have programmable utf-8 titles.

### Local Identifiers

Custom identifier schemes meant to identify things in a limited scope should usually have some set of "custom" or "private use" identifiers, prefixes, ranges, or root namespaces.

One of the following three schemes is suggested for identifiers with limited scope not subject to collision issues on a global scale:

One is to use reserved characters, such as reserving all identifiers starting with '\_\_', reserving all characters containing a dot, colon, or slash and allow custom or local use of the rest, or some similar prefix or suffix based scheme.

#### Prefix Based

In general, "special" or "builtin" identifiers should never begin with "x-" and anything starting with this string should be reserved for private use, but applications actually using "x-" prefixes strings must not cause data loss or any other such undesirable result in the event of a collision.

#### Hierarchy/URI-Like

Another way is to use loosely follow the URI concept, use slash separated hierarchy and to specify which root directories can and cannot be reserved. In applications like this percent encoding should be used to escape the slash, and at the characters ./?:;\[\]{}() should be reserved.
Identifiers using this method without a scheme should generally be assumed to be in some default namespace.
Such "URI-like" strings should never be used where the potential for conflict or confusion exists with real URIs, such as on the web, or in file managers, and should not be used for objects with a presence outside a limited scope, such as nodes in one network, actions in a set of related applications, etc.

#### Numerical

A third way, mainly for embedded devices, is to use a simple numbering scheme, where the first or last N numbers are reserved. This scheme must not be used for device or node IDs unless the numbers are set by the end user.

Libraries
---------

Libraries, even those that are a single file, should always be distributed as a folder for consistency and easy of packaging license info and readme files with the library. Ideally any documentation aside from a short readme and the license and credits, any unit tests, and other related files should be stored outside of the main library folder to allow libraries to be dropped in unmodified to statically linked projetcs

Responsiveness
--------------

Things with a GUI should not become unresponsive. Because of this, long IO operations(And all network IO) should always be done in the background, or in a loop that yields to the GUI event loop occasionally(This may be preffered due to locking issues)
In addition, all UI actions should immediately give some indication, such as displaying a progress bar.

Concurrency
-----------

Many modules requiring both high read performance and locks to access a data structure can use a read-only copy of that data structure that is only ever atomically updated by copying the working structure under the lock. Many operations can be satisfied without the overhead of a lock in this way

Legacy Support
--------------

Unless your application is likely to be used in a corporate environment or by a large audience of nontechnical users, don't spend too much effort on support for old versions of browsers.

However, as mentioned before, desktop-type apps should retain compatibility with old save files indefinitely, and applications to support hardware devices should retain support for older versions of the devices indefinitely.

Use of deprecated or removed command line arguments in shell programs should not cause errors.

Network and other IO
----------

Devices that normally communicate via the internet should, where possible, be able to discover each other via the local network in the absence of internet connectivity.

mDns should be used for local discovery, and occasional one-to-one requests that are not performance critical should be send via HTTP.

Where it is practical, serverless systems should be preffered to systems requiring a server.

Nodes should automatically retry and reconnect after a network failure, and, as much as is possible, should re-enter the same state they were in before the disconnection.

In GUI applications, a user action should not be required for a reconnection unless there are potential side effects, nor should a message popup be displayed. Instead, a status indicator should be used.

This also applies to non-ip networks like USB.

### HTTP

Passwords shall not be sent via unencrypted HTTP. GET requests should have no side effects, except where the URL contains some kind of security token, encrryption
is used, and aspects of the server such as logging is handled so as not to leak the password.

Security
--------

Passwords should not be stored in plaintext on the server. Storing passwords on the client for use in accessing the server is acceptable. HTTP applications should always support TLS but should not require it except for things that do not obviously need security. 

Memory Management
-----------------

In applications making heavy use of RAM, manual cleanup on unused objects is often insufficient due to bugs and coding errors, leading to frequent memory leaks in many applications. Because of this, liberal use of weak references should be made in languages that support them for all objects that are repeatedly created and destroyed at runtime.
Because garbage collection can be unpredictable, program correctness should not rely on weakly referenced data being collected in a timely manner.

Misc
----

Literal strings, numbers, and similar data should usually be avoided and moved to configuration files, however this may not always be practical or neccesary.
