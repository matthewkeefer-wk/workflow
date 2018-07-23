Code Standards
===============================
[Back to Team Agreement](README.md)

## General Tips

* Follows appropriate [style guide](https://github.com/Workiva/styleguide) for the language
   * When possible match the style of the file you are working in
   * When possible utilize the language specific linting scripts to automatically detect style issues (which should also be part of the smithy build process)
      * Golang - [gofmt](https://golang.org/cmd/gofmt/)
      * Dart - [Over React Format](https://github.com/Workiva/over_react_format#using-it) - [example from wdesk_sdk](https://github.com/Workiva/wdesk_sdk/blob/2.36.3/tool/dev.dart#L83)
* Write self documenting code
   * Create descriptive variable and function names
   * Add comments when what you are doing isn’t completely obvious 
   * Functions should do one thing
* TODOs or FUTURE comments in code should be cleaned up before code is merged or accompanied by a JIRA ticket for follow up work 
* Commented out code should not be merged
* Include docstrings on all exported symbols. 
* Keep the console and logs clean - (i.e. remove unneeded print/debug statements and ensure no RTEs occur on client or server side)
* Avoid the use of [Magic Strings](http://deviq.com/magic-strings/)
* APIs should include documentation 
   * Use the [documentation portal](https://dev.workiva.net/docs/api/) to document the API (i.e. add a docs.yml to the repo)
   * docs.yml examples from [wTranslate](https://github.com/Workiva/wTranslate/blob/master/docs.yml) and [wCRDT](https://github.com/Workiva/wCRDT/blob/master/docs.yaml)

## Languages

* Dart
   * Refer to [Effective Dart](https://www.dartlang.org/guides/language/effective-dart/style)
   * Memory management [best practices](https://dev.workiva.net/docs/teams/platform/application-frameworks/front-end-dev-training/memory-management) should be followed
   * Test ids have consistent names and added as we add functional tests
* Go
   * Read the Workiva [Go Best Practices](https://docs.google.com/document/d/1hReRG1wvEZS5BV1H3a9Q4eZV6xV651BF3CfbDVjWMa0)
   * Refer to [Effective Go](https://golang.org/doc/effective_go.html) and [Go Proverbs](https://go-proverbs.github.io/)):
      * A little copying is better than a little dependency.
      * Code to [interfaces](https://golang.org/doc/effective_go.html#interfaces_and_types)! Having to stand up networked resources for unit tests is not fun.
      * Unit testing is hard, write as functionally as possible to ease injectability.
   * Turn on **gofmt** in your IDE.
* Bash
   * Use [GNUMake](https://www.gnu.org/software/make/manual/make.html) to do your work in a cross platform fashion.


## Commits

* Write [good commit messages](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html).
* Include the what and most importantly the why
* Include the ticket number
   * Optional - setup a git commit-msg hook that does this for you - [example](https://github.com/Workiva/workiva-scripts/blob/master/dev_scripts_v2/git_hook_commit_msg.sh)
* Optional - verify your commits (added security) - [article](https://github.com/blog/2144-gpg-signature-verification)

## Tracing

* Consider adding tracing spans to a function in the following scenarios:
    * RPCs (e.g. thrift and frugal)
    * Sending data to persistence or other services (e.g. S3, RDS, SQS)
    * Potentially expensive operations (lots of complexity) - use your judgement

## IDE

Many developers use VSCode for daily development with the following extensions:
  - [Spell Checker](https://marketplace.visualstudio.com/items?itemName=streetsidesoftware.code-spell-checker)
  - [Go-lang Plugin](https://marketplace.visualstudio.com/items?itemName=lukehoban.Go)
  - [Highlighting for Thrift and Frugal files](https://marketplace.visualstudio.com/items?itemName=cduruk.thrift)
  - [Better icons library](https://marketplace.visualstudio.com/items?itemName=robertohuertasm.vscode-icons)
  - [Golang TDD](https://marketplace.visualstudio.com/items?itemName=joaoacdias.golang-tdd)
  - [JSON Tools](https://marketplace.visualstudio.com/items?itemName=eriklynd.json-tools)
  - [Plant UML](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml)
  - [Git Lens — git blame annotations, code lens, and more](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
  - [Git History](https://marketplace.visualstudio.com/items?itemName=donjayamanne.githistory)
  - [Find Go Interface Implementations](https://github.com/Workiva/vscode-go-interfaces)

A suggested settings file is located at `.vscode/init_settings.json` and can be enabled by renaming the file to `settings.json`.

Other editors are acceptable as well including:

* IntelliJ
* vim
* atom

If you have plugins / tips for these or other editors feel free to add content above

## Additional Reading

* [The Pragmatic Programmer](https://en.wikipedia.org/wiki/The_Pragmatic_Programmer)
* [Clean Code](https://www.amazon.com/Clean-Code-Handbook-Software-Craftsmanship/dp/0132350882)

If you have any other books/articles please add them to this list! (i.e. create a PR to this file)

