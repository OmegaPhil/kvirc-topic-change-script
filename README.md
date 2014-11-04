Topic Change Script sends you mail via a configured separate mail command when desired channels change their topic.

Last updated on 4.11.14 for v1.8.


Installation
============

v1.8+ requires KVIrc 4.3.1 r6393 or higher due to a KVIrc Script change - for all I know I'm the only user of this script, if you have an earlier version of KVIrc and want to use this script, please open an issue on Github (see 'Bugs And Feature Requests' later) and I will try to work something out.

To load the script into KVIrc (which then persists until you uninstall) and run its startup alias, in a KVIrc console window:

    /parse <path to script file, speechmark-delimited if the path contains spaces>
    /TopicChangeScript::Startup

Once the script is installed, TopicChangeScript::Startup is automatically called when KVIrc is started.


Dependencies
============

A mail command of your choice - I use [sendemail](http://caspian.dotconf.net/menu/Software/SendEmail/), a perl script currently packaged in Debian. This script must be told how to invoke it (see later).


Uninstallation
==============

In a KVIrc console window:

    /TopicChangeScript::uninstall::uninstall


General Configuration And Usage
===============================

The 'Scripts' menu is created on the main KVIrc menubar, which then hosts the Topic Change Script menu:

![Script menu](https://f92fac806bf10a96c0b8-8a0a46e5f1a5cc9854958bc3503f0f88.ssl.cf1.rackcdn.com/media_entries/7544/script-menu.png)

'List all monitored channels' echos monitored channels out to the current window, 'Monitor channel for topic changes' launches the following dialog to allow you to manually add a channel (see also the channel right-click menu later):

![Monitor channel dialog](https://f92fac806bf10a96c0b8-8a0a46e5f1a5cc9854958bc3503f0f88.ssl.cf1.rackcdn.com/media_entries/7545/monitor-channel-dialog.png)

'Remove channel from monitoring for topic changes' launches the following dialog:

![Remove channel dialog](https://f92fac806bf10a96c0b8-8a0a46e5f1a5cc9854958bc3503f0f88.ssl.cf1.rackcdn.com/media_entries/7546/remove-channel-dialog.png)

Finally, 'Configure email command...' launches the following dialog, working the same way as my other scripts:

![Configure email command dialog](https://f92fac806bf10a96c0b8-8a0a46e5f1a5cc9854958bc3503f0f88.ssl.cf1.rackcdn.com/media_entries/7547/configure-email-command-dialog.png)

It isn't likely to happen, but for safety's sake as this command is executed through a shell, strongly-quote at least the message substitution (single quotes) so that a malicious channel hop+ can't make you execute whatever he wants (the topic contents are sent in the message body). 

The bottom command should be selectable and copyable once [this feature request](https://svn.kvirc.de/kvirc/ticket/1468) has been merged into KVIrc. In the meantime, the command is:

    /usr/bin/sendemail -f "me@mymailhost.org" -t "to@destinationhost.org" -s "mymailserver.co.uk" -xu "SMTPAuthUsername" -xp "SMTPAuthPassword" -o tls=no -u '%s' -m '%m'

Obviously replace with what you want, and test it in a shell if things appear not to work (you can also see sendemail complain in '~/.xsession-errors' when this script tries to run a bad invocation).


Channel Menu Integration
========================

To monitor a channel for topic changes, right-click the channel window and go Topic Change Script -> Receive email when topic changes:

![Channel menu](https://f92fac806bf10a96c0b8-8a0a46e5f1a5cc9854958bc3503f0f88.ssl.cf1.rackcdn.com/media_entries/7548/channel-menu.png)

Pop up the menu again and the menu entry allows you to stop receiving email from the channel.


Commands
========

The following commands are available:

    /TopicChangeScript <command>

    <no command>
        Returns the on/off state of the script
        
    help, h
        Returns this usage information
        
    on
        Turns script on
        
    off
        Turns script off

    startup
        Load script up

    listnotifychans
        Echoes all channels where a topic change triggers an email

    addnotifychan <channel>
        Adds a channel to be emailed about when the topic changes

    deletenotifychan <channel>
        Deletes a channel from the topic monitoring list


Alias/Scripting Usage
=====================

The script is fully commented so should be fairly accessible for those wanting to see how to take its use further - for alias usage, see comments preceeding the alias, or run the alias without parameters for help/errors.


Development
===========

Try out my modification of the [geany](http://www.geany.org/) IDE, extending it to syntax highlight, parse KVIrc Script for aliases, events, variables, shortcut for loading scripts into KVIrc etc: [Github documentation](https://github.com/OmegaPhil/geany-kvircscript/wiki/README---KVIrc-Script-Integration).


Bugs And Feature Requests
=========================

Please create an issue on the [Github issue tracker](https://github.com/OmegaPhil/kvirc-topic-change-script/issues).


Contact Details
===============

OmegaPhil+KVIrc.Script@gmail.com
