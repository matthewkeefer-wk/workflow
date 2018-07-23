Code Review
===============================
[Back to Team Agreement](README.md)

This must be performed by an independent developer (i.e., not an authoring developer). Unsure of something? Don't be afraid to discuss with the original dev(s), another dev, or QA.

* Check out the [guide to high-quality code reviews](https://docs.google.com/presentation/d/1b3oJrtdjCOyeH4N5Od0jDmEOT4449SXFiYgNoUOg2io/edit#slide=id.p)
* We require two +1s and a QA+1 (a +10 counts as a +1 and a QA+1) on the last commit of every PR before it is merged.
* If you think a PR could affect security (or Aviary flags the PR as a security-related PR), it must also have a separate "security +1" on the last commit in addition to two +1s.
   * The security +1 can come from one of the devs who +1'd the PR in the first place.
* Github will auto suggest what individuals would be experienced to do a code review (based on contribution history).  You can ping these people, or the team directly for a heads up to review the code.
* Code should be "semantically transparent", i.e., readable, well formatted, and as DRY (don't repeat yourself) as possible given performance or other constraints
* Use the "Start a Review" when you anticipate there being more than one comment
* Reviewers should be timely in their reviews 
* Follow [ego-less](https://en.wikipedia.org/wiki/Egoless_programming) mentality - it is not YOU we are reviewing… it is the CODE
* Refer to and reference our [Code Standards](CODE_STANDARDS.md) during the review
* Understand the code
   * A +1 means you feel comfortable supporting customers using this code
   * Mentally walk through what the change is doing
* No bugs are introduced
   * Look for corner cases
   * Impacts to other features/services
   * Ensure dark code isn’t exposed
* Ensure code readability
   * If a reviewer is having trouble understanding it then everyone that sees that code in the future will probably also have trouble
   * "Tricky" areas of the code are well commented
   * Comments have been added/updated for new/existing classes, structs, and functions
* Look for scenarios that would indicate a security review is necessary
   * Refer to [Development Security Review Guidelines](https://wiki.atl.workiva.net/pages/viewpage.action?spaceKey=SECURITY&title=Development+Security+Review+Guidelines)
* Automated Testing
   * Effective automated tests have been added/updated and kept as lightweight as practical
   * Unit tests are properly guarding against regressions
   * Code coverage on all appropriate lines.
      * Use the [codecov plugin](https://chrome.google.com/webstore/detail/codecov-extension/keefkhehidemnokodkdkejapdgfjmijf?hl=en-US) to see the coverage in github
      * Shoot for a high percentage of code coverage (see [discussion](https://stackoverflow.com/questions/90002/what-is-a-reasonable-code-coverage-for-unit-tests-and-why))
* Automated tools that must pass
   * DartMedic
   * Dart Semver Audit
   * Aviary
   * Rosie
   * Smithy/Skynet
* Semver is properly followed
   * [Client side](https://github.com/Workiva/ApplicationFrameworks/blob/master/WdeskVersioning.md)
   * Server Side - frugal versioning is our main way of versioning communication between services 
* Blog post on Code Review - [We are Ruthless On Code Reviews](https://w-dev-blog.appspot.com/posts/2016/03/31/we-are-ruthless-on-code-reviews/index.html)

## UX

Tickets that include UX work should get a "UX +1" from the responsible UX Designer prior to merging.

* The earlier you can show something to your UXD, the fewer surprises will crop up just before trying to release.
* @mention UXers on PRs that include UX work.
   * The UXer should be able to preview either a
      * Ngrok
      * Deployment to a sandbox URL
      * Screenshot / Screen capture
   * The UXer can then verify the AC was met to the spec previously delivered and provide a "UX +1" 

## Rosie and Github Approvals
Rosie is transitioning from using +1’s in comments on pull requests as valid reviews. Instead, we will be taking advantage of GitHub’s approval feature.

<b>What this means for you</b>
Going forward, all code and “special” (security, opseng, etc.) reviews will need to be applied using this feature. To apply a special review, simply type “Security +1”, or any other phrase that triggers your special review in the comment field of the review.
Note: You must select the approval radio button (option button) when submitting your review. If you select Comment or Request Changes, Rosie will not consider your review as a +1, regardless of what you include in the comment field of the review.
