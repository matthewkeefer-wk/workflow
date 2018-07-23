Dependencies
===============================
[Back to Team Agreement](README.md)

This is the full story. The TL;DR is [here](../../README.md#dependency-management).

skaardb is primarily a Go repo that also generates Javascript (JS) code with Dart bindings, as well as frugal-generated messaging API code (currently, Go, Dart, and Python).

To ease dependency management, flexible [SemVer ranges](http://semver.org/) are recommended for all Workiva repo's with version >=1.0.0. Please comment exceptional cases appropriately.

## Go

Make sure [dep is installed](../../README.md#install-dep-using-homebrew). 

A subset of the Go code is transpiled to JS using [GopherJS](https://github.com/gopherjs/gopherjs). GopherJS is consumed by skaardb _and_ installed as an executable. The main complication here is that [GopherJS does not support being vendored](https://github.com/gopherjs/gopherjs/issues/415), so the [Makefile](../../Makefile) targets accommodate this to ease development while still tracking GopherJS using standard dependency management tools.

Code dependencies and build tools are vendored in the [vendor](../../vendor) directory and committed to this repo. To vendor the dependencies and install the build tools specified by the [Gopkg.toml](../../Gopkg.toml) and/or [Gopkg.lock](../../Gopkg.lock), run
```bash
$ make vendor
```
This will add any missing dependencies to the vendor directory, generate the [Gopkg.lock](../../Gopkg.lock) file if it is missing, and also prune unneeded items. The vendor directory (without GopherJS) and the lock file are committed to the repo. Certain vendored files are also not committed via specification in the [gitignore file](../../.gitignore).

Because of the dependencies that `make vendor` can change, `make vendor` also conservatively runs `make build-tools`, `make gopherjs`, and `make generate-thrift-all`.

See the [Usage section of the dep README](https://github.com/golang/dep#usage) and the [spec for the Gopkg.toml](https://github.com/golang/dep/blob/master/docs/Gopkg.toml.md). In particular, if a dependency is new, then save the associated import statement(s) to at least one Go source file before running `make vendor` to avoid premature pruning by `make vendor`.

#### IMPORTANT

If you use the `dep` tool directly, such as `dep ensure -update [some/repo/I/need/to/update]`, then be sure to run `make vendor` when you are done to make sure everything else is brought up to date.

The vendor directory is checked for accuracy, but not updated, in Smithy CI, so make sure to commit the correct and up-to-date vendored dependencies (by running `make vendor` before pushing).


## Dart

Dart code is in the `lib` directory and dependency management is the standard one provided by [pub](https://www.dartlang.org/tools/pub). The version control in the [pubspec.yaml](../../pubspec.yaml) must be compatible with publishing skaardb to to Workiva's [pub server](https://pub.workiva.org/packages/skaardb) for Dart client consumption. The [pubspec.lock](../../pubspec.lock) is currently committed to the repo.

#### IMPORTANT

`pub get` will pull Dart dependencies in Smithy CI, and in some edge cases will change dependencies specified in the [pubspec.lock](../../pubspec.lock).


## Parsimony, Frugal, GopherJS, and Other Build Tools

Build tools such as parsimony, frugal, and gopherjs are installed on the GOPATH (with versions taken from the Gopkg.lock) using
```bash
$ make build-tools
```
Note that—
  - [GopherJS currently **cannot** be vendored](https://github.com/gopherjs/gopherjs/issues/415), and so `make build-tools` installs it on the GOPATH at the commit specified in the [Gopkg.toml](../../Gopkg.toml). (Note that indirect dependencies of GopherJS installed on the GOPATH by `go get -u github.com/gopherjs/gopherjs` are **not** version controlled.)
  - Other critical build tools (e.g., frugal) are specified in the [Gopkg.toml](../../Gopkg.toml), vendored, and installed by `make build-tools` from skaarbd's vendor directory. (Build tools like frugal also appear as an imported library.)
  - Certain non-critical 3rd-party build tools are not specified in the [Gopkg.toml](../../Gopkg.toml) (e.g., `go2xunit`), and their versions are tracked by the Smithy builder version that includes them.


## Updating GopherJS-Generated Javascript Code

The GopherJS-generated JS code needs to be updated when changes are made to transpiled Go code.

1. Ensure the branch is up-to-date with master:
```bash
$ git pull origin master
```
2. Build the GopherJS-generated Javascript code: 
```bash
$ make gopherjs
```
The GopherJS transpiled JS code and its Dart bindings are found [here](../../lib). Note that `make gopherjs` also runs the [constpiler](../../cds/tools/constpiler/constpiler.go) that generates Dart bindings from Go constants.

#### IMPORTANT

The GopherJS-generated `.js` and `.js.map` files for the Dart bindings are not committed to the Git repository, so if you wish to consume the bindings from your local copy of skaardb, you'll need to run the `make gopherjs` command.

If you want to commit the GopherJS-generated JS files so that you can consume the bindings from a Git branch, you can force add the files to override the [.gitignore](../../.gitignore) settings for them: `git add -f lib/*.js*`.


## Adding More Methods to the Dart Bindings (bindings.go case)

1. Write a top-level method in [bindings.go](../../dart-bindings/bindings.go).
2. Add an entry to the bindings map in the [bindings.go](../../dart-bindings/bindings.go) main method.
3. Update the GopherJS-generated javascript code (see above).
4. Write a public API in the dart code that uses
   `context['skaardbBindings'].callMethod()` to leverage the method(s) written in [bindings.go](../../dart-bindings/bindings.go) that were transpiled into javascript. Use the existing methods in [bindings.dart](../../lib/bindings.dart) as a model.
5. Merge the PR to skaardb. This will update the Dart [pub package](https://pub.workiva.org/packages/skaardb) on the subsequent tag.
6. Consume the new tagged version of skaardb in your Dart package.

For advice on consumption by Dart, see [dart-bindings/README.md](../../dart-bindings/README.md).

#### IMPORTANT

You don't wan't to break consumers' builds or block them from consuming new functionality, so be sure to provide an adequate deprecation period for breaking changes, following Workiva's [Wdesk Client-side Versioning Policy](https://github.com/Workiva/ApplicationFrameworks/blob/master/WdeskVersioning.md).


## Updating Frugal-Generated Code

Frugal-generated code is managed using Workiva's [parsimony tool](https://github.com/Workiva/parsimony), as specified in the [parsimony.yml](../../parsimony.yml). We track the version of parsimony in the [Gopkg.lock](../../Gopkg.lock) and vendor it like other build tools. 

To generate code for all languages, run
```bash
$ make generate-thrift-all
```
In particular, the frugal-generated Go code is committed to the repo [here](../../frontend/messaging/gen), and the frugal-generated Dart code is included in the [Dart bindings](../../lib/src/frugal_gen) for client consumption. Python code is used for testing, for example, in ["thin" load testing clients](../../qa/loadtest/src/locust_main.py). Java generated code is built, packaged, and made available for installation into JVM projects via artifactory.

### Building Java Locally
In order to build and package the generated Java code locally, you will need to set up your maven environment with credentials to our internal artifactory server. This process is documented on the [Dev Portal](https://dev.workiva.net/docs/internal-software/dev-tools/dev-environment#artifactory-and-maven).

#### IMPORTANT

Frugal-generated code is **not** updated in Smithy CI, so make sure you updated and commit the generated code when needed. Also, be sure to follow Workiva's [Wdesk Client-side Versioning Policy](https://github.com/Workiva/ApplicationFrameworks/blob/master/WdeskVersioning.md) that prohibits tightly coupled server+client releases. Deprecate wisely to avoid coupled releases and to accommodate "rollback" combinations of new/old server against new/old client.
