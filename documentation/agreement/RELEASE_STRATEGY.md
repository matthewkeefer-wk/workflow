Release Strategy
===============================
[Back to Team Agreement](README.md)

* Spreadsheets has a daily rotating (between DM's and QA/SDETs) release "manager" that is responsible for monitoring all of the automatically generated release PRs associated with Spreadsheets (skaar and dt), as well as the release pipelines that are kicked off.
* Refer to the [SkaarDB Pipeline](https://w-rmconsole.appspot.com/repo/Workiva/skaardb/pipeline_template/)
* Refer to the [Spreadsheet Signals Plans](https://wf-skynet.appspot.com/signals?group=5081205232107520)
   * [spreadsheets_pentest_smoke_test](https://wf-skynet.appspot.com/signals/773306074)
   * [spreadsheets_wk-dev_smoke_test](https://wf-skynet-hrd.appspot.com/signals/825176053)
* Every day at 9AM CDT, Rosie will automatically cut a release off of the master branch
* We can also cut a tag whenever we need one via Marv
* If a regression occurs the first thing that will be done is revert the offending PR and re-tag a patch release.
* On the subsequent patch/followup work, the one who breaks a deploy or causes a regression is responsible for writing tests to assert that breakage doesn't happen again
   * The fix PR needs to contain the tests to assert the breakage doesn't happen again, as that would specify what's needed and when it's needed.
   * Prefer the lowest testable layer to verify the deploy won't break again

## Additional References

* [Release Pipeline](https://dev.workiva.net/docs/teams/release-management/release-pipeline)
* Release Management Documentation ([dev portal](https://dev.workiva.net/docs/teams/release-management), [wiki](https://wiki.atl.workiva.net/display/RM/Release+Management+Home))
* Blog post: [A Reference Workflow for Your Critical Software Delivery](https://w-dev-blog.appspot.com/posts/2017/05/26/a-reference-workflow-for-your-critical-software-delivery/index.html) 
