# Merge Proposal (MP) reviewing

Check formal content:

* changelog
* patch naming
* version numbers
* patch headers
* etc

## Initial review

### Check the new changelog stanza

* Contains a bug pointer like `(LP: #12345678)` to 
* Correctly formatted entries according to the [changelog policy](https://www.debian.org/doc/debian-policy/ch-source.html#debian-changelog-debian-changelog) and our [hints](PackageMerging.md#fix-the-changelog) for merges
* Lists all changes made - the changelog shall be a complete representation
* Proper version - check against [Version Strings](VersionStrings.md)
* Proper release - `dch` or habits could have selected the wrong one
* Proper author and email

### Ensure Documentation/release Notes are updated

* We always did enqueue things that eventually need to be mentioned in the release notes, this check in the MR review is a reminder about that.
* If the update/merge has implications that need to be documented we always updated documentation alongside changes. Sometimes things get in via a sync or upstream changes, not by us - as we spot these, make sure to spawn a proper backlog tracker for it.

### Check for indirect changes

* Some changes can imply that the packaging needs to be adapted. Check content and release notes if there are any changes like that.
* When merging from Debian or Upstream it is worth checking if there are even newer versions that would be worth it to go for.
  * Bad things happen, check upstream if a release has been withdrawn or needs an immediate fix-up due to unintentional breakage.
* Ensure that the changes in Debian do not imply that we need to update the delta we carry (do not be fooled by applying cleanly)
* Ensure update maintainer has been run

### Check the old delta

* Ensure that everything we dropped really can be dropped
  * vice versa, there could be more that could be dropped (often needs a little test to verify which is suggested to the owner of the MR and only rarely done by the reviewer)
* Are all changes either:
  * Forwarded to Debian or Upstream so that everyone benefits and we can some day make this a sync again.
  * Or if they are Ubuntu only choices, marked like that so the next packager is not wondering if we want to keep or submit it?

### Check the new delta

* Do the patches [Follows DEP-3](http://dep.debian.net/deps/dep3/)
  * You can use dep3changelog to verify the headers, as well as generate a changelog entry.
* Do the patches match what is (proposed) upstream
  * If not strictly required for the change we want to make, avoid going sideways with code we need to support but not matching the future evolution of the project (hard to maintain well).
* Are the patches applied the right way according to `debian/source/format`?

### Check for Git/maintenance

* Changes are logically split into separate commits (to ease future merges and cherry picking to other releases)

### Check for Build and Test

* Ensure the build in the PPA is ok on all architectures it is meant to build
* If this is an SRU consider checking that the SRU template in the bug is OK. Test instructions especially are often only understandable for the reporter. We want them to be good before SRU review.
* If applicable relative to the changes made, consider if tests should be added, adapted or extended
* Too many cases have been caught late and then intertwined in proposed-migration. Testing autopkgtest on the PPA helps to be confident before entering the archive
* Depending on the case the test PPA might be used to install and sanity check the builds


## Review template

The following template may be useful when submitting reviews:

```
Review Symbols:
x = OK
- = not OK - reasons outlined in the lines below
? = question - asked in the lines below
N = not applicable to this case

* Changelog:
  - [ ] Changelog entry has correct version and targeted codename
  - [ ] Correct formatting of changelog items
  - [ ] Bug references correct
  - [ ] Old content and logical tag match as expected (Package Merge)

* Release notes and Documentation
  - [ ] Added, updated or enqueued relevant documentation.
  - [ ] Added, updated or enqueued relevant release notes.

* Package Merge - indirect changes:
  - [ ] No upstream changes that need adapting due to Ubuntu's design
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
  - [ ] Commits are properly split (more important on -dev than on SRUs)

* Build/Test:
  - [ ] Build is OK
  - [ ] This is an SRU, the validation instructions are ok
  - [ ] Testcases added or adapted (N/A if not strictly required or already present)
  - [ ] autopkgtest against the PPA package passes (if possible, evidence was provided already)
  - [ ] Verified PPA package installs/uninstalls
  - [ ] sanity checks test fine
```
