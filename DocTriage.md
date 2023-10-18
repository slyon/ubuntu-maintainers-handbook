# Documentation triage

In order to maintain a line of communication with the community and keep
Ubuntu Server's documentation up to date, doc triage has been added as a task
to do during [bug triage](BugTriage.md).

## Tooling

[Discourse Triage](https://snapcraft.io/dsctriage) (`dsctriage`) is used for
working with documentation hosted on Discourse. Documentation for the tool is
located on [GitHub](https://github.com/lvoytek/discourse-triage).

`dsctriage` can be installed with:

```bash
sudo snap install dsctriage
```

As a part of daily triage, running the base command will show relevant
comments for the previous day (or over the weekend).

```bash
dsctriage
```

To run the previous day's triage, provide the relevant date or previous day of
the week, such as:

```bash
dsctriage 2023-04-27
```

or

```bash
dsctriage friday
```

## Types of updates

Documentation updates fall into a few categories that require different levels
of action.

### New pages

When someone creates a new page, which in Discourse is a new Topic under the
relevant category, this will show up as a `+` next to the page title and author
name. For example:

```text
+Changing package files [Lena Voytek, 2023-01-11]
```

If this shows up, the page should be checked to see if it is a candidate for
the official documentation. If so, note this in the report.

### Page edits

If a given page has been modified in any way, a `*` will show up alongside the
page title and the name of the editor. This looks like:

```bash
*Ubuntu Server tutorials [Sally Makin, 2023-04-12]
```

In this case, check what the edit was and note it in the report. If it has any
obvious issues, especially if it is a part of the official documentation, make
sure to note that too.

Also keep in mind when this page was created, as it may need to be triaged as
a new post too if it was published within the provided time frame.

### Community comments

When a community member comments on a page, it will show up with a `+`
alongside a link and author name for the comment. A `*` may show up instead if
the comment was modified. This line will show up as part of a tree of replies
under its given page name.

Multiple updates to a conversation may also have happened, such as:

```bash
SSHd now uses socket-base… [Steve Langasek] 
├─ 77972 [Paride Legovini] 
│  └─ 80966 [Saxl] 
│     └─ 81043 [Leszek A. Szczepanowski] 
│        └─ 83849 [Nebulabox] 
│           └─ 84773 [Michael Utech] 
│              └─ +88070 [Piradix, 2023-04-05] 
├─ +88748 [Dave Ruedeman, 2023-04-19] 
└─ +88948 [Darren Embry, 2023-04-23] 
└─ *88978 [Steve Langasek, 2023-04-23] 
```

Look through the added and updated comments by clicking the attached links. If
a community member has an unanswered question, either reply with the relevant
information or note in the report that it needs a reply. For suggestions to
change the docs, if they are valid, update the page accordingly or note it
down so someone with relevant permissions can do so.

If no action can be taken immediately, or finding the information will take
some time, reply to the community member to inform them that we will get back
to them and thank them for taking the time to leave a comment. This helps to
set expectations and prevents our community members from feeling ignored (even
if we cannot provide an answer straight away).

### Team responses

Responses to community comments by someone on the team will look the same as
other comments. In this case, check to make sure the conversation was resolved,
and provide extra input if needed.

