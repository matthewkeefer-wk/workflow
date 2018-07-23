Testing Process
===============================
[Back to Team Agreement](README.md)

## Testing Template

```markdown
Performing QA plus one
- [ ] Pulled master before testing  
- [ ] Consumer testing was successful in datatables and text_doc_client 
- **Skynet**
    - [ ] Skynet passed on latest commit
    - [ ] Skynet passed on first run
        - reason for rerun 
- **Semver**
    - [ ] Patch
    - [ ] Minor
    - [ ] Major
- **Acceptance Criteria**
    - [ ] *Description*
- **Regression testing**
    - [ ] *Description*
- **Test Coverage**
    - [ ] Unit Tests added
    - [ ] Integration Tests added
```

## QA+1

* This must be performed by QA or an independent developer (i.e., not an authoring developer).
* First make sure the code reviews (2/2) have taken place.  See [code review](CODE_REVIEW.md) section for more details.
* Code coverage is within tolerance for the repo (diff and total, see repo's settings at [https://codecov.workiva.net](https://codecov.workiva.net))
* Any impact of changes on internal/external consumers has been sufficiently addressed (Does next version in [marv](https://w-rmconsole.appspot.com/marv/Workiva/skaardb/) need updating to communicate a breaking change?)
* Followup tickets/action items for outstanding or unaddressed issues, e.g., existing bugs revealed, problems with dependencies out of our control, planned refactors, follow up automated tests to write, etc.
* Current master has been merged in (use `git pull origin master` before pushing the branch), especially if the branch's last commit is very old and/or the changes are not isolated from concurrent commits to master (NOTE this is enforced by Rosie "Recent smithy run" function)
* All automated checks have passed, including unit, integration, and functional tests
* Detail of what was tested manually (if anything) and which regression areas and edge cases were examined/discovered
* Should automated tests have been created here or in a followup ticket?
   * NOTE: For Production level software we are required to have an audit trial of our testing for each packaged release we give to customers. If automated testing is not completed as part of the ticket, the manual testing for a given area will need to be preformed and documented for every release until said tests are automated.
* In General Follow These Steps:
   * Pull down the code and if necessary deploy it
   * Thoroughly test it according to the testing instructions
      * Corner cases
      * How it works with other features
      * Verify new/modified functional tests pass locally
   * After standard testing instructions - try other ways to "break" it
   * Cases where passing CI is sufficient
      * Unit tests
      * Documentation (i.e. *.md files)
      * Dark features (i.e. not customer facing in any way).  It is up to the developer and the reviewers of the code to ensure this is in fact a dark feature.
* If QA is not merging the PR, then please notify QA if there is anything important about the PR that QA should be aware of (e.g., release ramifications). Also, please make sure that automated testing has been properly addressed!
* Recall that a +10 is a QA+1 plus a +1 code review.

## Additional Information 
* [Types of Tests](TYPES_OF_TESTS.md)
