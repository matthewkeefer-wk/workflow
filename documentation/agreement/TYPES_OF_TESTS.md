Types of Tests
===============================
[Back to Team Agreement](README.md)

## Unit

* Does this method or class behave as I intended?
* Tests are automatically executed by Continuous Integration (CI) - both smithy and skynet
   *  should run tests to ensure this repo “working”
* Cover as many lines as possible
   * Explain in the code review why uncovered lines are missed
* Test happy path, sad path, edge cases, exception cases
* All tests should be independent of other tests
* Use Mocks only for asserting calls, Dummy/Fake/Stub/Discard for trivial cases. [article](https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub/27151309#27151309)
   * Mock implementation of interfaces

## Integration

* Do these classes|libraries|applications work together as I expect?
* Skynet 
* Smoke Tests
   * Created by QA/SDET
   * Used to verify general app stability

## Functional / End to End

* For the SkaarDB repo the functional tests exist in the top level customer facing repo(s) - such as datatables
   * It is important to understand what these tests are and what value they provide.
* Does my application work as expected when a user interacts with it?
* Added for all new UI components 
* Creation is the responsibility of the developer
* QA/SDET members are available to them to help teach/coach and define what tests should be covered

## Collaborative Testing

* Use test blitzes when:
   * A large amount of code is changing (large PR)
   * Prior to the feature being released (i.e. on wk-dev, sandbox)
   * Possibility for a far reaching impact
   * Prior to removing features from Beta
   * Prior to moving a feature from behind a feature flag and into beta. Need to assure all beta blockers have been fixed prior to giving access to our beta customers.
* Arrange with QA/SDET 

## Additional Information 
* Blog post: [What Kind of Test is That?](https://w-dev-blog.appspot.com/posts/2015/12/07/what-kind-of-test-is-that/index.html)
