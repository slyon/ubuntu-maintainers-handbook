# Bug triage

New bugs get reported every day, and existing tickets in Launchpad get updated
with comments, patches, and status changes. The triager's job is to review the
traffic, deal with invalid or trivial issues, ignore stuff that's just noise,
and flag items of importance, urgency, and/or readiness.

Triaging work is shared across the team, with the goal of successfully
reviewing every bug filed against Ubuntu Server-related packages. Each
triaging session focuses on a subset of tickets that changed during a specific
time period, such as the previous day. The triager isn't responsible for
solving the reported problem, only with ensuring it gets the appropriate
attention.

All newly-reported issues will need a triager's review. A review involves
analysing a bug to determine: a) if the bug is valid, and b) if enough
information was provided, and then marking it 'Triaged'. Otherwise, it's set
to a more appropriate state with a comment explaining why, and what the next
actions are (if any).

Older issues generally require no triager action if they're progressing
through their normal workflow. However, the triager should watch for comments
providing new information that may make the issue more actionable.

## Types of issue tickets

Items in the triaging queue tend to fall into a few categories, that are
handled in different ways:

### Process tickets

Bug reports are often used to track status of packaging workflow tasks:

- Sync requests
- Merge requests
- Stable release updates (SRU)
- Main Inclusion Requests (MIR)
- Freeze exception request (FFe, UI-FFe, et al.)
- Package promotion/demotion ("Seed management/changes")

These will generally either be filed by, or assigned to, a team member. If
not, investigate further. For properly owned tickets, 'No action is required'
by the triager, unless something unusually weird is going on -- in which case
'Raise with the Team'. That **raising** could be "bringing it up in
post-standup", "bringing it up in the weekly bug meeting" or "bringing it up
in a chat channel and pinging related developers".

TL;DR -- do not stay alone with the weirdness. Group experience and group
decisions win.

### SRU regression bugs

Problems that look like the result of an SRU update to a server package need
to receive top priority. For such bugs, 'Add to Server-Todo Queue' and 'Raise
with the Team'.

If possible, verify whether rolling back to the prior version of the package
fixes the issue, and whether re-installing the update brings the issue back.
In this case, also tag the bug 'regression-update'.

Be aware that bugs are sometimes described as regressions simply because
they're new to the user, and not due to actually being introduced from an SRU
update. For example, the user could have had a bad config file already, but
the SRU triggers a restart of the service and *that* is when the user notices
the problem and files a bug, thinking it was the update that introduced it.
  
### Security regression bugs

A report of a regression caused by a security update should be passed to the
security team. Tag the bug 'regression-update', mark it "Public Security" and
subscribe `~ubuntu-security`, which will notify them.

You may also wish to ping them in `#ubuntu-security` on `Libera.Chat` to
ensure handover, but since they monitor Public Security bugs this is not
strictly required.

### Severe bugs

Urgently important issues such as ones with potential for widespread breakage,
should immediately 'Add to Server-Todo Queue'.

### High profile bugs

Issues which involve an important customer or VIP, or that turn up frequently
in search results, can generate a lot of "repeat visits" so to speak. Just
'Raise issue with the team', unless it's already well known in which case 'No
action required' by the triager.

### Support requests

Sometimes users report problems that are really just a misunderstanding of how
to use their system. Kindly redirect them to more appropriate venues for help,
and/or lend any obvious advice, but otherwise close the ticket as "Invalid"
due to being 'Not a Bug'.

### Unclear

If the ticket is missing log files, version details, or other information
necessary to decide how to handle the bug, ask the user for what's needed, set
the ticket to "Incomplete" due to 'Not Enough Info.'

### Duplicate

If the issue is clearly the same as another report:

- Mark one as duplicate of the better reported (or older) issue.
- If there are existing tickets that sound very similar, make sure they are
  mentioned in a comment. Ask the reporter(s) to review those and identify
  whether it is indeed a duplicate, and if it is not, then they should
  elaborate on how this new one differs.

### Non-actionable comment

If an existing ticket pops up in the queue due to a comment, check if it is
adding information.

- If it's just noise (e.g. "me too!"), 'No action is required' by the triager.
- If it seems to describe a legitimate problem, but one completely unrelated
  to the originally-reported issue, recommend filing a new bug report.
- Otherwise, outline the next steps needed for the bug to make progress so that
  interested parties have some solid guidance on what they can do to help.

### Unreproducible bug

If the issue can't be reproduced (e.g. in an LXC container) then ask the
reporter to provide the 'Missing Steps to Reproduce' it.

### Reproducible bug

If there seems to be enough information to reproduce the bug, try to do so in
an LXC container -- itemise the steps to follow, and how to identify that the
bug has indeed occurred. If it all looks good, subscribe the server team, or
if the issue looks urgent and/or important 'Add to Server-Todo Queue'.

### Already fixed in development

An issue that can be reproduced in a supported Ubuntu release, but not in the
current development version of Ubuntu, may qualify for SRU processing.

- Make sure the reproduction steps are clearly outlined.
- If the issue is minor/trivial, it probably won't be worth SRUing, so should
  be closed as already fixed in development.
- If the issue is a request for a feature (not a bug fix), it may not qualify
  as eligible for SRU. If that's the case, either close it as fixed in
  development, or add bug tasks for the requested releases set as 'Wishlist',
  and close the main bug task as fixed.
- If the issue *is* a bug fix and looks important, then determine which
  supported Ubuntu releases will need the fix and add 'Bug Tasks' as
  appropriate. Even though the issue is fixed in development, leave the main
  task *open* in this case because otherwise Launchpad may not display it in
  reports and lists.

### Already fixed in Debian

If the issue has been solved in Debian, it will likely be worth merging and/or
SRUing the fix.

- Make sure steps to reproduce it are identified.
- If the issue affects the development release, it is a merge opportunity. If
  past feature-freeze, decide if it's worth a freeze exception. Make sure
  there is a merge bug in Launchpad for the package, and consider to
  'Add to Server-Todo Queue'.
- If the issue affects a stable release and looks SRU-worthy, determine which
  supported Ubuntu releases will need the fix and add 'Bug Tasks' as
  appropriate.

### Already fixed upstream

All the steps of the "Already fixed in Debian" category apply here as well. We
can help Debian when appropriate by:

- Filing a Debian bug about it, or chiming in if there is an existing one.
- If you create a PR for Ubuntu that can be used almost as-is, consider
  sending one via Salsa as well.
- Aligning our solution with Debian is not only kind, but also helps to avoid
  long term complex divergence and deltas.

### Unclear

If in doubt, or if none of the above applies, consider bringing it up via chat
-- or if looking for a group discussion (and decision) tag it
`server-triage-discuss`. We try to resolve these bugs together in our weekly
meeting.

## Special cases

A few of our packages have common issue patterns or best practise triaging
actions. This section shall list them so that anyone on triage duty can find
all of them in one place.

### MySQL

MySQL often has low quality bug reports submitted by users not fully aware of
which dependency brought it onto their system. Those often fall into a few
common usage errors.

Furthermore, there are a few long-standing issues that affect many users but
often are reported as new.

* Due to that, we've found that a good first step in triaging MySQL is
  checking for duplicates.

  * In the days of `mysql-5.7` (Xenial/Bionic) we tagged the common core bugs
    that one would duplicate new bugs to. Those are available as
    [mysql-5.7 triage tag](https://bugs.launchpad.net/ubuntu/+source/mysql-5.7/+bugs?&field.tag=triage).
  * Since `mysql-8.0` we no longer use that tag, instead it turned out to be
    more reliable to just look at recent
    [mysql-8.0 bugs by heat](https://bugs.launchpad.net/ubuntu/+source/mysql-8.0/+bugs?orderby=-heat&start=0)
    to spot the duplication candidates.
* If not a duplicate, then still please update the bug title from the usual
  Apport "failed on postinst" to whatever the bug really is about for better
  recognition of the issue in any kind of overview that just lists the titles.

### Virtualization controlled through libvirt  

If these reports are about the inability to access devices or "permission
denied" issues, the user often does not realise that libvirt applies an
AppArmor profile to the guest for enhanced security.

If not available in the bug report (dmesg of the time of occurrence) ask the
reporter to check for AppArmor denials at the time the problem triggers.

## Process and policy

### Direct team subscriptions

We subscribe `~ubuntu-server` directly to a bug to track our community bug
backlog while the bug meets the following criteria:

1. Anything that, if the bug turns out to be valid, is something that would be
   under the `~ubuntu-server` remit to fix (common use cases but not obscure
   ones -- although nothing stops an individual volunteering to work on an
   obscure use case).
1. By definition, if it's something that we wouldn't fix and request
   volunteers for even if we had time, then it doesn't warrant a subscription.
1. This subscription is for the Ubuntu Server triage community and is not for
   tracking internal Canonical customer requests. Whether a Canonical customer
   has made a request about a particular bug makes no difference, and provides
   no additional priority under this process. A Canonical customer bug may
   still be subscribed if it qualifies under these criteria.
1. If the bug is assigned to someone on our team, leave the team subscribed.

When the bug no longer meets these criteria, we unsubscribe from it.

### Tagging `server-todo`

This is our tag, which we use to represent "valid and we should work on it".
I.e., better than just the usual "valid" backlog.

We want to assign bugs from this queue regularly. To avoid losing traction
there is a weekly bug housekeeping meeting (see below) to ensure no bug gets
blocked or forgotten for too long.

The goal is to have this list at around 30-40 bugs most of the time. If it
drops lower, we can refill the list with candidates from the `~ubuntu-server`
subscribed bugs. However, if the list grows significantly out of this range it
becomes unrealistic to expect those issues to be handled in time, and we
should communicate that to the reporters.

Qualification for `server-todo`:

* Whatever we think that we want to work on soon. For example:

  * An important new technology for Ubuntu-Server users.
  * Great community engagement that provides debugging and/or patches.

* We want to *avoid* bugs where the next step will take significantly longer
  than one day to complete, unless the bug is particularly important. For
  example:

  * An Ubuntu-only feature that is important for our users -> OK to be in the
    list despite likely needing more time.
  * A valid crash report, but a corner case affected only one user. All low
    hanging fruits and obvious checks are done, therefore the next debug step
    is estimated to take at least a week -> this might be OK for the backlog,
    but not really for `server-todo`.
  
  Make sure it is clear if the bug needs work in development or needs SRUs, by
  defining bug tasks accordingly. These bug tasks can help in identifying
  current vs. obsolete bugs.

* Only bugs that qualify for the backlog qualify here. If they aren’t suitable
  for the backlog (e.g. not actionable by us) then they get dropped from both
  `server-todo` and the backlog.

  * If there are any updates to the case they will reappear in the triage queue
    and can be reevaluated then.

### Daily bug expiration

The tooling will help to report these to the triager.

* **Server subscription expiration** -- default after **180 days**
  
  If nobody touched a bug for 180 days (~= 1 release cycle) it is reasonable
  to check for changed conditions. Quite often, for example, a patch one was
  waiting on might be available now, or a newer release fixed the bug already.
  
  Essentially, anything that is listed here needs to be fully re-triaged to
  ensure the list reflects the current status. After the 180 days you will also
  have metrics on how many more people are affected by the bug
  (importance/#affected). Most commonly, it turns out that:

  * Recent releases upstream (or even already in Ubuntu) have the fix ->
    
    * Re-triage, consider tagging `server-todo` for SRU.
    
  * The bug should have been supported by the community but nothing happened ->
    
    * Re-triage importance, consider dropping `~ubuntu-server` subscription.

  * A bug that was formerly considered a "real case" no longer qualifies (e.g.
    alternative solutions have taken hold as *the* way to do it) ->
    
    * Re-triage importance, consider dropping `~ubuntu-server` subscription

  If you're unsure, add the `server-triage-discuss` tag and bring it up at the
  next standup.

Overall, we want to be honest in the bug reporter, to try to understand why an
issue was not worked on, and to explain it if possible. Also, if we drop
`server-todo` or the `~ubuntu-server` subscription for any of the reasons
above, always add an explanatory comment. If reporters disagree with our
re-triage they will report on the bug and it will show up in the daily triage
duty the next day to be reconsidered with their point of view taken into
consideration.

### Weekly bug housekeeping

In addition to the daily triage (and our ongoing dedication to resolving bugs
we picked up that way) the Server Team has introduced a weekly bug housekeeping
session. In that session we go through various lists, ensuring that no bugs or
issues are forgotten, blocked or stalled for too long.

There are a few additional steps we take, which change over time based on
current priorities. For example, looking for good candidates to do MREs in the
future, or trying to assign our remaining cleanup on the Discourse
documentation feedback backlog. While these may change, there is a core
structure to what we always look at in this meeting:

1. Check the `server-todo` tagged bug list:

   1. Get list via `ustriage`:

      ```bash
      clear; ustriage --no-show-triage --extended --show-tagged --tag server-todo -S savebugs/todo-$(date -I'seconds').yaml -C $(ls -1t savebugs/* | head -n 1)
      ```
      
      The list of last week's bugs helps to identify new/closed cases and is
      [tracked in the helpers repository](https://git.launchpad.net/~ubuntu-server/+git/ubuntu-helpers/tree/savebugs)

   1. Check size (see min/max above) of the `server-todo` tagged bug list.
   1. Ensure assigned bugs make reasonable progress:
   
      1. Discuss blockers/reasons if there was no progress.
      1. Notice, enjoy and celebrate progress that was made.

   1. Ensure unassigned bugs find an owner:
   
      1. Ensure long term unassigned bugs are re-reevaluated (is there a
         reason why they are not tackled?)

1. Look at [update-excuses by team](https://people.canonical.com/~ubuntu-archive/proposed-migration/update_excuses_by_team.html#ubuntu-server)
   to spot anything that needs our attention to migrate. If there are any team
   members assigned to analyse the case and ensure things are progressing.
1. Look at our [merges schedule](http://pinot.endarchy.org:4200/merges-schedule)
   to identify if we have fallen behind on any of them.

> Future outlook:
>
> As capacity permits, we want (in the future) to start also looking at the
> [sponsoring queue](http://reqorts.qa.ubuntu.com/reports/sponsoring/index.html).

## Awareness of the triage

We have several stakeholders to keep up-to-date on things we've found during
triage. We also want to keep the community generally informed, as well as
raising issues within the team to ensure they are not being forgotten.

For the community we send a mail to `ubuntu-server@lists.ubuntu.com` that
summarises how many bugs we've triaged, and touches on the noteworthy cases.
This can also be used to CC additional people that (for case-specific reasons)
should be aware of a case.

An example of that would be if a security fix caused an upgrade-regression
which would make us CC the uploader and/or ubuntu-security. This mail should
also contain relevant information from [documentation triage](DocTriage.md).

Furthermore, on cases that need immediate attention (or at least awareness)
we might:

* Bring them up in the daily standup (if they need a discussion/decision that
  one can't do alone).
* Ping a subject matter expert via IRC/Mattermost.

In some cases, a package maintainer might already be aware and following the
case. To avoid endless re-pings on such a case the agreement is that if the
maintainer is personally subscribed (i.e. with their launchpad username, not
just indirectly via teams like
[Ubuntu Virtualization](https://launchpad.net/~ubuntu-virt))
then we consider the maintainer to be aware and we will not do extra
pings/mentions/CC.

## Triage rotation

According to load we might shift things, but generally every day Tuesday to
Friday one team member is assigned to triage duty.

Monday is often more work and includes more low quality bugs since it includes
all of the weekend. Therefore, Monday is rotated through all eligible bug
triagers. This is organised internally in the team's Jira, and automatically
creates a Task with the "bug-triage" label assigned to the person on rotation.

## Tooling

The [ustriage](https://snapcraft.io/ustriage) tool is available as a snap
and serves as our triage tool. It is maintained publicly on GitHub
as [ubuntu server triage](https://github.com/canonical/ubuntu-server-triage).

It has options to identify bugs for the triage of the day as well as serving
as a helper to check our tagged bugs, ensuring that nothing falls through the
cracks. The README.md of the linked project has more details and use case
examples.

## Outdated/deprecated

This info is kept around for a while in case one encounters older bugs that
still use those tags or processes. Eventually these sections will be removed.

### Tagging `server-next` (deprecated)

Since early 2022 we have had enough control over the backlog bugs that the
former set of `server-next` + `server-todo` bugs was reduced to just
`server-todo`. The reason for this was that we found we had the capacity to
work on bugs that didn't fulfil the rather strict rules we used to have for
`server-next`.

> Since the backlog is bigger than what can be achieved in a short time, there
> is extra classification via the tag `server-next`. That tag is set by the
> triager (or anyone else working on doing the Root-Cause-Analysis or a Fix) to
> reflect that this is an issue that shall be tackled by the Team's resources
> "next".
>
> Another reason to add `server-next` in some cases is to preserve high quality
> contributions of the community. An example might be a report that the user
> already bisected and created a patch for - in those cases the benefit
> diminishes by bit rot way too fast, so handling that next helps to retain
> the work the reporters did. And vice versa it might encourage one or the
> other to provide more high quality bugs.
>
> The goal is to have this list around ~20 bugs most of the time, if dropping
> below we can refill with candidates from the *~ubuntu-server* subscribed
> bugs. But if it grows significantly out of this range it is non-realistic to
> expect those issues to be handled in time, we should communicate so to the
> reporters.
>
> The rules of the `server-next` tag are as follows:
>
> 1. Must not tag unless bug is actionable. Doesn't mean it must have a patch,
> only that a developer has enough information to work on the bug, even if it
> means more debugging.
> 2. Tag only if one of these two things are true:
>    1. Delays will discourage this excellent community contribution.
>    2. If you believe it affects a major use case for Ubuntu server users. In
>       this case you should also set the bug Importance.
> 3. The set of all bugs tagged `server-next` must be kept small. If it grows,
>    the lowest priority bugs tagged `server-next` must be removed until the
>    list isn’t too big.
> 4. This tag is for the Ubuntu Server triage community and is not for tracking
>    internal Canonical customer requests. Whether a Canonical customer has
>    made a request in relation to a particular bug makes no difference and
>    provides no additional priority under this process. A Canonical customer
>    bug may still be tagged if it qualifies under these criteria.
> 5. If the bug is assigned to or otherwise owned by someone on our team, there
>    is no need to tag it.
> 6. Remove the tag when the bug is assigned to or otherwise owned by someone
>    on our team.

> * **Server-next expiration** - default after **60 days**
>
>   If we considered a bug actionable and added it to server-next, but then no
>   update happened in 60 days that usually means something went wrong. Often
>   bugs are blocked on external constraints. This needs to be evaluated as a
>   case-by-case decision. Most common cases are, that it turns out:
>
>   * that the bug is not solvable/reasonable the way it was planned 
      -> re-triage, maybe drop server-next.
>   * that it is actually fixed or otherwise progressed without update
      -> update bug
>   * that we failed to give it the required focus
      -> add the server-triage-discuss tag to the bug and bring it in the next 
>     standup

