# What we are
ChatZilla, aka cZ, was one of the best IRC clients ever.  Unfortunately, it had problems.  The biggest of which is how it was based on Mozilla's older XUL technology which is no longer supported.

## What made cZ better than other IRC clients?
* It could shorten irc:// urls by replacing the full host name (the irc.libera.chat part) with just a name for the network.  So instead of `irc://irc.libera.chat/chatzilla`, you'd get `irc://libera/chatzilla`.
* It could replace known emoticons with graphical emoji on incomming messages.  So `:)` would be rendered as this: ![:)](http://chatzilla.hacksrus.com/common/image/face-smile.png)
* Tabs could be renamed by the user or a script.
* The topic bar could expand as needed.
* The input box had two sizes.  In the small size, it would treat the user pressing Return/Enter as a signal to send.  However, in the larger size, the Return/Enter key would put a newline into the text.  In either case, the newline would be sent in the text.  Other clients split the text into multiple texts at each newline.

# What we like in other clients
While cZ is our favorite existing client, there are a few features in other clents we'd like to offer in our product.  First and foremost, most of those clients have built in support for SASL and Bouncer logins.  cZ does have SASL script, but nothing for logging into your bouncer.

## From HexChat, Y-Chat,, and other X-Chat forks
* X-Chat on Windows could let users change formatting by reclicking on selected text or with a special formatting toolbar.

## From Konversation
* One of Konversation's biggest selling points is something that all KDE programs have: An editable main toolbar.

## From Quassel and SMUXI
* These clients can connect to a remote routing server.  This is kind of like a private bouncer built right in.  You could have your client computers X and Y.  But they both connect to "server" routing to the real IRC server.

# Note: Our name is only a placeholder.  As such, once we have a better name, expect our GitHub URL to change.
