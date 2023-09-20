# What we are
ChatZilla, aka cZ, was one of the best IRC clients ever.  Unfortunately, it had problems.  The biggest of which is how it was based on Mozilla's older XUL technology which is no longer supported.

## What made cZ better than other IRC clients?
* It could shorten irc:// urls by replacing the full host name (the irc.libera.chat part) with just a name for the network.  So instead of `irc://irc.libera.chat/chatzilla`, you'd see and enter `irc://libera/chatzilla`.  cZ would expand the URL on the fly before trying to contact the server.
* It could replace known emoticons with graphical emoji on incomming messages.  So `:)` would be rendered as this: ![:)](http://chatzilla.hacksrus.com/common/image/face-smile.png)
* Tabs could be renamed by the user or a script.  Something like `cZ Replacement` takes up less space than the channel identifier for our official channel: `#chatzilla-replacement-project`.
* The topic bar could expand as needed.
* The input box had two sizes.  In the small size, it would treat the user pressing Return/Enter as a signal to send.  However, in the larger size, the Return/Enter key would put a newline into the text.  In either case, the newline would be sent in the text.  Other clients split the text into multiple texts at each newline.
* The entire UI could be styled with CSS.  No other client provides anything like that.  They might let you change the colors, but cZ could be told to add icons to each tab to mark the status.  While our application might not be browser based, we'd like to offer something similar even if CSS can't be used.
* cZ would interpret some format codes for bold, underline, and italics and switch fonts.  So if you wrote `/i/`, it would put an 'i' in italics.  It also supported some MIRC codes for formatting.  We should support all the above.
* cZ let users rearrange tabs as desired.  Other clients forced all tabs to be sorted, but some group them by network.  That is better in some regards, but we like grouping channels as desired, such as topic.
* Because cZ was built on the Mozilla suite codebase, it came with free touchscreen support.  Few other legacy clients include this support.

# What we like in other clients
While cZ is our favorite existing client, there are a few features in other clents we'd like to offer in our product.
1. First and foremost, most of those clients have built in support for SASL and Bouncer logins.  cZ does have SASL script, but nothing for logging into your bouncer.
2. Many other clients attempt to maintain a marker line as to what they think you've read and haven't read for each channel.
3. Many clients also have buttons for toggling common channel modes and will commonly display a tooltip for what those modes mean.  That helps non-expert IRC users.
4. Several of these clients also can reload your log from previous sessions.
5. Many of these clients also let you configure custom actions for the user list.  These commonly appear anywhere you can right-click a user name, including the chat.  Most also let you put these actions into buttons that are typically shown near the bottom of the user list.

## From HexChat, Y-Chat,, and other X-Chat forks
* X-Chat on Windows could let users change formatting by reclicking on selected text or with a special formatting toolbar.

## From Konversation
* One of Konversation's biggest selling points is something that all KDE programs have: An editable main toolbar.

## From Konversation and SMUXI
* These clients can be scripted from your choice of anything that can be run from the Linux commandline.  This might end up being copied.

## From Quassel and SMUXI
* These clients can connect to a remote routing server.  This is kind of like a private bouncer built right in.  You could have your client computers X and Y.  But they both connect to "server" routing to the real IRC server.

## From non-IRC clients
IRC clients aren't limited to the best ideas.

### Element (Matrix) and Discord users can paste long blocks of text and/or images into the input box
This works by having the server then stores a copy online.  Since we don't have that ability with a server, we can't simply allow that.  But it's handy.  So we'd rely on something like [Paste.pics](https://paste.pics/) and [PasteBin.com](https://pastebin.com).  Both might have to be written as plugins so if their API changes, we can simply issue a new version of the plugin.  Plus, users could choose which site to use.

### Element (Matrix) can a really good marker line
While Discord also has a decent marker line, Element's version is better.  The user can switch between the first post they missed and the most recent as often as they want.  When the user first arrives back at their computer, Element is waiting at the first missed post.  You press Escape to clear the marker.  Discord waits at the most recent post.

### Both Element (Matrix) and Discord can show emoji as large characters
This happens if a post consists only of emoji characters.  If so, the client chooses a larger version of the same font.

### Both Element (Matrix) and Discord can show previews of links
It's unknown how Discord does it, but Matrix servers store the preview on the server.  The client never accesses the site improving security.  While many IRC users wouldn't like that, some would.  So we should add an option to at least show ***a*** preview even if we have to access the site from the client.  This might be something added later.

### Matrix clients and Discord both let you link a new post to an existing post
Would IRC users like to be able to include a short quote?  This could be both with an without a ping to the original poster.

# The vision
The intention is to end up with a user interface, or UI, largely based on that of cZ.  Internally, we like the idea of maintaining some of the logic in the existing cZ application.  However, the code in there is ancient.  Not only is it relying on the old XUL technology, but it predates the newer JavaScript lannguage features like classes.

For scripting, if we can ensure we don't end up with a security hole, it'd be nice to copy the system used by Konversation and [SMUXI where any executable in the correct folder is effectively a script](https://github.com/ChatZilla-Replacement-Project/.github/edit/main/README.md#from-konversation-and-smuxi).  However, we shouldn't limit ourselves to that.  Instead, we should mimic cZ's existing alias system where an alias like `checknick` might evaluate to `whois $(1); ns info $(1)`.  Note that runs two commands.  Also, many systems may not be able to run JavaScript, though we may not want to maintain the existing cZ SDK.  It is a pain in the neck to work with.

But we should also provide one final option: Plugins could provide more flexibilty for someone wanting to customize the program.  They'd do this by letting the plugin interact with the client by asking it questions.  The system used by Konversation and SMUXI limit the script/plugin to whatever can be passed in text environment variables.  They do let developers use more languages though.

## What we'd develop in
That's way up in the air.  As noted, cZ was written with XUL and JavaScript.  XUL is definitely out as Mozilla doesn't maintain it.  If we use JS, it will be the latest version of JavaScript we can expect in today's browsers.  But that might not meet some of our goals if we require any executable to act like a script.  [There's certainly discussion of porting cZ to a web extension](https://bugzilla.mozilla.org/show_bug.cgi?id=1322442), but they're waiting on some WE extensions to go any further.

cZ did have the ability to run without a browser with help from XulRunner, but that died a LONG time ago.  Mozilla lost interest in XR before they dropped XUL.  There's been no XR replacement.

That leaves abandoning the browser entirely.  Since cZ could run that way, we aren't losing anything.  Instead, we might gain users who wouldn't use our choice of browser.

At least one potential developer on the project works mainly with C# and Windows Presentation Framework.  WPF and .NET do run outside Windows with help from [Wine](https://www.winehq.org/) and [Mono](https://www.winehq.org/), but we'd need to limit ourselves to slightly older versions of .NET and C#.  Java is an option as that developer does work with it and Swing.  But many others represent a learning curve.  Options include C#/GTK#, C#/QtSharp, C++/GTK, C++/Qt, C++/Wx, and more.

# Password storage
We need to keep passwords secure.  So we need to store them encrypted using something like Windows Hello or the various Linux keyrings.  The typical IRC client stores them unecrypted in a text file of some form.

# Hiding or showing parts, joins, and nick changes
In some channels, there can be a lot of server messages about parts, joins, and nick changes drowning out new posts.  There are two main existing strategies with a third that attempts to combine the two.
1. Show all parts, joins, and nick changes
2. Hide all parts, joins, and nick changes
3. Switch between the first two depending on how many people are in a channel

However, there might be another option.  Suppose we show those events, but if there are a lot of people present, we hide the events after a few seconds.  We then group all such events between posts and hide them in an expandable block.  We then let users choose between the various strategies.  We also let them configure the automatic ones.

Regardless of mode, we should always show kicks, ban changes, quiet changes, and channel mode changes.

# Tiny URLs
We should have the ability to expand tinyurls from the short link to the full URL which would be shown in a tooltip in the GUI version.  [If we do a TUI](https://github.com/ChatZilla-Replacement-Project#should-we-include-a-text-interface-option), it might show the full URL in parentheses.  We should also offer in preferences the ability to turn long URLs into the short URL of the user's choice.  This might default to tinyurl.com, but there might be better choices.  See also [Both Element (Matrix) and Discord can show previews of links](https://github.com/ChatZilla-Replacement-Project#both-element-matrix-and-discord-can-show-previews-of-links).

# Integration with the user's desktop
We should attempt to integrate with the desktops for Windows, Gnome, and KDE Plasma along with their forks.
* With Windows, that may mean:
  * offering a system tray icon
  * Taskbar integration to show previews of the various channels and tabs and possibly common tasks.
  * Start menu tiles and common actions
  * Action center notifications if the user wants them
* With Gnome, that means a menu looking like MacOS
* With KDE Plasma, we may offer widgets

# Helping ops be aware of channel activities while ignoring users in other channels where they aren't ops
We should allow users to ignore users—and then choose to ***not*** ignore them in channels where one of them is opped.  So if you're responsible for channel #x, you can choose to ignore select users everywhere except in #x.

On a similar note, maybe users would like to stalk select words on a channel by channel basis.

# Per channel features we want
* Ability to ignore users everywhere—except on channels we are ops
* Stalk words on only select channels
* Ability to notify the user on any event, including new messages
* Pin tabs?

# Dream wishlist items
* We should offer the ability to browse available scripts/plugins.  This might not happen until after version 1.0, but it's something no other IRC client offers.
* As for themes, the built in theme should attempt to mimic the theme provided by the OS.  Should the user want to override that, it'd be nice to let the user browse choices there.  Of particular note: We need to support both dark and light themes.

# Should non-IRC protocols be supported?
Initially, the project would be for IRC only.  But it may have IRC support actually implement as a library system.  If another library were to appear later supporting Matrix, Discord, Jabber, or something else, maybe we should support that.  It's unknown how we'd implement the UI.  Both Pidgin and SMUXI can do this, but Pidgin's libpurple reportedly has some major security holes.  If there's any other problem with Pidgin, it ends up looking more like a client for just Twitter and Messenger rather than IRC.

# Should we include a text interface option?
Some clients for Linux are strictly text based and can run even without a graphical user interface or GUI.  This is limited but some users like it.  If we did this, the commications portion of the product would be a seperate executable that might be an installation option.  Users could then choose to install just one interface or both.  The text interface, sometimes called a TUI, would prevent support of many non-IRC protocols.

# Module Owners
As the organization grows, we'll need to assign owners to those who are the main contacts for each module in the application.  Owners would handle any pull requests and might be the only one with that option.  These owners might be the primary coders for the module.  Examples:
* The main GUI app
* The TUI app (if implemented)
* Support for each OS would need its own owner
* The IRC communications module
* The scripting modules
* The browsers for themes and scripts/plugins
* Other protocol modules
* Providers for:
  * Tiny URLs
  * Paste Bins
  * Image hosts

# Touchscreen Support
It's considered important we support touchscreens even on desktop platforms.  To that end, we'll either create specialized themes or have a touchscreen mode.  When selected, controls will be larger.  When deselected, controls are smaller allowing for denser content.

# Phone/Tablet support?
Eventually, we should grow to support Android and iOS.

# Store/repository versions
We should be listed in as many stores and repositories as possible.  This would include WinGet, Windows Store, Google Store, Amazon Store, iTunes App Store, Ubuntu, Debian, OpenSUSE, Magiea, and more.

# Portable versus installed
Many users like having portable applications.  So we should have a mode where settings and logs are stored in the application directory rather than the user's profile.  Regardless, we should never install the app into the user's profile unless the operating system has a location that's protected from malware that might try to infect our app.  Users going for the portable "installation" will have to take that risk.

# Progressive Web Application
One option is to do a PWA.  These run in the browser, but can be installed by some browsers so they appear to be local apps.  You can also generate an installer and provide what appears to be a normal executable.  We don't want to assume any specific browser, but if we provide one internally, problem solved.  Some of these systems expose what to the operating system appears to be an executable they know how to run.

# Note: Our name is only a placeholder
As such, once we have a better name, expect our GitHub URL to change.  In the meantime, we're on Libera IRC at [#chatzilla-replacement-project](irc://irc.libera.chat/chatzilla-replacement-project) or [#chatzilla-replacement-project (SSL)](ircs://irc.libera.chat/chatzilla-replacement-project) , but that could change too.
