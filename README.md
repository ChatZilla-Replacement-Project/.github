# What we are
ChatZilla, aka cZ, was one of the best IRC clients ever.  Unfortunately, it had problems.  The biggest of which is how it was based on Mozilla's older XUL technology which is no longer supported.

## What made cZ better than other IRC clients?
* It could shorten irc:// urls by replacing the full host name (the irc.libera.chat part) with just a name for the network.  So instead of `irc://irc.libera.chat/chatzilla`, you'd get `irc://libera/chatzilla`.
* It could replace known emoticons with graphical emoji on incomming messages.  So `:)` would be rendered as this: ![:)](http://chatzilla.hacksrus.com/common/image/face-smile.png)
* Tabs could be renamed by the user or a script.
* The topic bar could expand as needed.
* The input box had two sizes.  In the small size, it would treat the user pressing Return/Enter as a signal to send.  However, in the larger size, the Return/Enter key would put a newline into the text.  In either case, the newline would be sent in the text.  Other clients split the text into multiple texts at each newline.
* The entire UI could be styled with CSS.  No other client provides anything like that.  They might let you change the colors, but cZ could be told to add icons to each tab to mark the status.

# What we like in other clients
While cZ is our favorite existing client, there are a few features in other clents we'd like to offer in our product.  First and foremost, most of those clients have built in support for SASL and Bouncer logins.  cZ does have SASL script, but nothing for logging into your bouncer.

## From HexChat, Y-Chat,, and other X-Chat forks
* X-Chat on Windows could let users change formatting by reclicking on selected text or with a special formatting toolbar.

## From Konversation
* One of Konversation's biggest selling points is something that all KDE programs have: An editable main toolbar.

## From Konversation and SMUXI
* These clients can be scripted from your choice of anything that can be run from the Linux commandline.  This might end up being copied.

## From Quassel and SMUXI
* These clients can connect to a remote routing server.  This is kind of like a private bouncer built right in.  You could have your client computers X and Y.  But they both connect to "server" routing to the real IRC server.

# The vision
The intention is to end up with a user interface, or UI, largely based on that of cZ.  Internally, we like the idea of maintaining some of the logic in the existing cZ application.  However, the code in there is ancient.  Not only is it relying on the old XUL technology, but it predates the newer JavaScript lannguage features like classes.

For scripting, if we can ensure we don't end up with a security hole, it'd be nice to copy the system used by Konversation and [SMUXI where any executable in the correct folder is effectively a script](https://github.com/ChatZilla-Replacement-Project/.github/edit/main/README.md#from-konversation-and-smuxi).  However, we shouldn't limit ourselves to that.  Instead, we should mimic cZ's existing alias system where an alias like `checknick` might evaluate to `whois $(1); ns info $(1)`.  Note that runs two commands.  Also, many systems may not be able to run JavaScript, though we may not want to maintain the existing cZ SDK.  It is a pain in the neck to work with.

But we should also provide one final option: Plugins could provide more flexibilty for someone wanting to customize the program.  They'd do this by letting the plugin interact with the client by asking it questions.  The system used by Konversation and SMUXI limit the script/plugin to whatever can be passed in text environment variables.  They do let developers use more languages though.

## What we'd develop in
That's way up in the air.  As noted, cZ was written with XUL and JavaScript.  XUL is definitely out as Mozilla doesn't maintain it.  If we use JS, it will be the latest version of JavaScript we can expect in today's browsers.  But that might not meet some of our goals if we require any executable to act like a script.  [There's certainly discussion of porting cZ to a web extension](https://bugzilla.mozilla.org/show_bug.cgi?id=1322442), but they're waiting on some WE extensions to go any further.

cZ did have the ability to run without a browser with help from XulRunner, but that died a LONG time ago.  Mozilla lost interest in XR before they dropped XUL.  There's been no XR replacement.

That leaves abandoning the browser entirely.  Since cZ could run that way, we aren't losing anything.  Instead, we might gain users who wouldn't use our choice of browser.

At least one potential developer on the project works mainly with C# and Windows Presentation Framework.  WPF and .NET do run outside Windows with help from [Wine](https://www.winehq.org/) and [Mono](https://www.winehq.org/), but we'd need to limit ourselves to slightly older versions of .NET and C#.  Java is an option as that developer does work with it and Swing.  But many others represent a learning curve.  Options include C#/GTK#, C#/QtSharp, C++/GTK, C++/Qt, C++/Wx, and more.

# Note: Our name is only a placeholder.  As such, once we have a better name, expect our GitHub URL to change.
In the meantime, we're on IRC at [irc.libera.chat/chatzilla-replacement-project](irc://irc.libera.chat/chatzilla-replacement-project) or [ircs.libera.chat/chatzilla-replacement-project (SSL)](irc://ircs.libera.chat/chatzilla-replacement-project).
