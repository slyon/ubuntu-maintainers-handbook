# Merge Proposal (MP) reviewing

Check formal content:

* changelog
* patch naming
* version numbers
* patch headers
* etc

## Initial review

### Check the changelog header

* [Follows DEP-3](http://dep.debian.net/deps/dep3/)
* Contains a bug pointer (LP: #12345678)
* Proper version change
* Proper distribution
* Lists all files changed
* Proper author and email

### Ensure Documentation/release Notes are updated

* We always did enqueue things that eventually need to be mentioned in the release notes, this check in the MR review is a reminder about that.
* If the update/merge has implications that need to be documented we always updated documentation alongside changes. Sometimes things get in via a sync or upstream changes, not by us - as we spot these, make sure to spawn a proper backlog tracker for it.

### Check the commits

* Changes are logically split into separate commits
* changelog is the last commit

### Check the files

* Only files inside the debian directory have been modified

## Review template

The following template may be useful when submitting reviews:

```
* Changelog:
  - [ ] Changelog entry has correct version and targeted codename
  - [ ] Correct formatting of changelog items
  - [ ] Bug references correct
  - [ ] Old content and logical tag match as expected (Package Merge)

* Release notes and Documentation
  - [ ] I have checked and added or updated relevant documentation.
  - [ ] I have checked and added or updated relevant release notes.

* Package Merge - indirect changes:
  - [ ] No upstream changes that need adaptating due to Ubuntu's design
  - [ ] No further upstream version/changes to consider
  - [ ] Debian changes are compatible with the Ubuntu implementation
  - [ ] update-maintainer has been run

* Package Merge - old delta:
  - [ ] Dropped changes are ok to be dropped
  - [ ] Nothing else to drop
  - [ ] Changes forwarded upstream/Debian (if appropriate)

* New delta:
  - [ ] No new patches added
  - [ ] Patches match those proposed/committed upstream
  - [ ] Patches correctly included in Debian/patches/series
  - [ ] Patches have correct DEP-3 metadata

* Git/maintenance:
  - [ ] Testcases added or not strictly required for this
  - [ ] Commits are properly split (more important on -dev than on SRUs)

* Build/test:
  - [ ] Build is OK
  - [ ] Verified PPA package installs/uninstalls
  - [ ] autopkgtest against the PPA package passes
  - [ ] sanity checks test fine
```
