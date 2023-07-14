Merge Proposal Reviewing
========================

 check formal content (changelog, patch naming, version numbers, patch headers, ...)

Initial Review
--------------

### Check the changelog header:

 * Follows dep-3 http://dep.debian.net/deps/dep3/
 * Contains bug pointer (LP: #12345678)
 * Proper version change
 * Proper distribution
 * Lists all files changed
 * Proper author & email

### Check the commits:

 * Changes are logically split into separate commits
 * changelog is the last commit

### Check the files:

 * Only files inside the debian directory have been modified

Review Template
---------------

The following template may come useful when submitting reviews:

```
* Changelog:
  - [ ] changelog entry correct version and targeted codename
  - [ ] correct formatting of changelog's items
  - [ ] bug references correct
  - [ ] old content and logical tag match as expected (Package Merge)

* Package Merge - Indirect changes:
  - [ ] no upstream changes that need adaptation due to Ubuntu's design
  - [ ] no further upstream version/changes to consider
  - [ ] debian changes are compatible with the Ubuntu implementation
  - [ ] update-maintainer has been run

* Package Merge - Old Delta:
  - [ ] dropped changes are ok to be dropped
  - [ ] nothing else to drop
  - [ ] changes forwarded upstream/debian (if appropriate)

* New Delta:
  - [ ] no new patches added
  - [ ] patches match what was proposed/committed upstream
  - [ ] patches correctly included in debian/patches/series
  - [ ] patches have correct DEP3 metadata

* Git/Maintenance:
  - [ ] testcases added or not strictly required for this
  - [ ] commits are properly split (more important on -dev than on SRUs)

* Build/Test:
  - [ ] build is ok
  - [ ] verified PPA package installs/uninstalls
  - [ ] autopkgtest against the PPA package passes
  - [ ] sanity checks test fine
```
