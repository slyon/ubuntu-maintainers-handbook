# Bug report responses

A common way people engage with Ubuntu is through the bug reporting system. A
poor experience here will sour their entire view of Ubuntu, so it's important
to recognise that you are acting as an ambassador for the Ubuntu team when you
respond to bug reports.

## General considerations

The first thing to remember is that the people reporting bugs are taking time
out of their schedule to help make Ubuntu better. That's a commendable act in
and of itself, regardless of how well they've done it.

Be respectful and empathetic in your responses. Bugs cause aggravation and
stress, and the bug reporter is probably in a less-than-stellar mood. Take a
gentle, tactful, dignified approach, disarm their frustrations, and try not to
take things personally. Mostly, aggravated people want their aggravations to
be acknowledged and understood.

Your responses should:

* Avoid "blame" words. For example, "You didn't do X" infers blame. Instead,
  try: "Could you try doing X?". Phrasing it as a request rather than an
  accusation puts people at ease and makes them more likely to engage with our
  processes.
  
  **Make them deputies to the solution rather than the source of the problem.**
  
* Keep things short and simple. Too much information confuses and intimidates
  people, and makes them less likely to engage.
  
* Be concise, but also assume that they don't have the same knowledge you do.
  Point them to easily digestible information that will help them do what's
  needed. By submitting a bug report they have shown they want to help, so
  make it easy for them to do what will help you.
  
* Pull calls-to-action out from the rest of the text. Rather than an action in
  the middle of a paragraph, start a separate paragraph containing only the
  instructions: 
  
  "Please do X and add the results as a comment."
  
  Calls to action should ideally be at the end of your response.
  
* Put instructions in bullet points. This makes it easy for the person to check
  the list and make sure everything has been done before they reply.
  
* Your response should be empowering, meaning that it gives them a positive
  path of action for solving their problem. Let them decide for themselves if
  it merits the effort.

* Thank them for their help!

## Common bug report responses

Here are some ideas for standard responses you can give for common themes in
bug reports. Feel free to use and modify to your tastes.

* [Not a bug](#not-a-bug)
* [Not enough info](#not-enough-info)
* [Missing steps to reproduce](#missing-steps-to-reproduce)
* [Filesystem corruption](#filesystem-corruption)
* [Fixed in later Ubuntu release](#fixed-in-later-ubuntu-release)
* [Please file in Debian](#please-file-in-debian)
* [Upstream bug](#upstream-bug)
* [Please test my PPA](#please-test-my-ppa)

### Not a bug

Thank you for taking the time to report bugs and help make Ubuntu better.

This looks like a local configuration issue rather than a bug in the software itself. Please check your configuration to make sure it's correct. If you need help configuring, you can get community support in the Ubuntu channels on libera.chat, or in http://www.ubuntu.com/support/community

I'm marking this "Invalid" because it doesn't appear to be a bug, but if I'm wrong, please change it back to "New" and add some more info to point me in the right direction. Use this link as a guide: http://www.chiark.greenend.org.uk/~sgtatham/bugs.html

### Not enough info

Thank you for taking the time to report bugs and help make Ubuntu better.

To act on this report, I'll need some more information, specifically:
* What impact this bug is having on users
* Specific, minimal steps to reproduce it (assume the reader isn't familiar with the software)
* Specific configuration (also, please make sure that it's the software and not the configuration causing the problem)

Use this link as a guide: http://www.chiark.greenend.org.uk/~sgtatham/bugs.html

Please add a comment with the extra information, and then set the bug status back to "New".

### Missing steps to reproduce

Thank you for taking the time to report bugs and help make Ubuntu better.

Could you provide the exact steps needed to reproduce the issue? Please write them under the assumption that the person investigating the bug may not be as familiar with the software as you are (for example, provide explicit preliminary steps to set up a minimum working configuration, if possible in an LXC container or virtual machine).

Please write the steps in a comment, and then change the bug status back to "New", so that we can begin working on it.

### Filesystem corruption

Thank you for taking the time to report bugs and help make Ubuntu better.

This failure looks like it's being caused by a corrupted file system. You should check your system immediately with the following steps:
* From the boot menu, select "Memory check"
* Boot from the installer CD, hold the right Shift key after the BIOS checks to get to the GRUB menu, and run "Check disc for errors"

If it detects file system corruption, the safest option is usually to back up whatever you can and reinstall the system.

You can also try `sudo apt-get clean` and then try reinstalling the package.

If you need more help, you can get community support in the Ubuntu channels on libera.chat, or in http://www.ubuntu.com/support/community

I'm marking this "Invalid" because it doesn't appear to be a bug, but if I'm wrong, please change it back to "New" and add some more info to point me in the right direction. Use this link as a guide: http://www.chiark.greenend.org.uk/~sgtatham/bugs.html


### Fixed in later Ubuntu release

Thank you for taking the time to report bugs and help make Ubuntu better.

This bug has been fixed in the current Ubuntu development release, which is why I'm marking it "Fix Released" (the bug status follows what's in the development release).

In order for the fix to be backported to earlier Ubuntu releases, it must qualify as a high-impact bug: https://canonical-sru-docs.readthedocs-hosted.com/en/latest/reference/requirements/#what-is-acceptable-to-sru

If it's important to have it fixed in an earlier Ubuntu release, please do as many steps as you can from https://canonical-sru-docs.readthedocs-hosted.com/en/latest/howto/standard/ and update this bug ticket with your progress.

The SRU team will review and advise you on the next steps to get it in place.

### Please file in Debian

**Also add tags: needs-upstream-report bitesize**

Thank you for taking the time to report bugs and help make Ubuntu better.

This bug is present in Debian too. It would be best to have it fixed in Debian, and then Ubuntu will pick it up on the next merge.

Could you please file a bug with Debian as well? Thanks!

### Upstream bug

Thank you for taking the time to report bugs and help make Ubuntu better.

Please could you check the latest upstream version to see if this is a bug in Ubuntu, Debian, or in the upstream project itself? If it turns out to be upstream, this bug would best be submitted and addressed upstream first by the software authors, and then it will be picked up by Ubuntu.

If you do end up filing an upstream bug, please link to it from here. Thanks!

### Please test my PPA

I've uploaded a test fix as a PPA: https://launchpad.net/~user/+archive/ubuntu/ppa-name

Since I can't verify the fix myself, can you please test the package available from here before I request an archive upload?

To make sure we properly squash this bug, we follow this procedure:

* You add the PPA to your affected system (follow the instructions "Adding this PPA to your system" from the link above).
* You re-run your test procedure to make sure it actually fixes the problem.
* You add a comment here saying that the fix works.
* I request that the fix be uploaded officially.
* The SRU team moves the package to proposed.
* You verify that the fix in proposed also works (to make sure nothing broke along the way).
* The SRU team moves the package to release.
* The bug is squashed, and everyone gets the update!

Thanks for your help!

## Web browser tools

Firefox can be extended with a script to paste in standard response text such
as those listed above. This script, called 'stock-replies', is part of the
"Launchpad Greasemonkey Scripts" package:

  https://launchpad.net/launchpad-gm-scripts

A Discourse post about the tool and how to install and use it can be found here:

  https://discourse.ubuntu.com/t/stock-replies-script/14103
