# Git guidelines

Before contributing to this project you should read the guidelines below.

## Branching strategy

The branching strategy is based on [Microsofts branching strategy](https://learn.microsoft.com/en-us/azure/devops/repos/git/git-branching-guidance?view=azure-devops).

There should only be a base branch for main. Any other branch should follow the guidelines below.

![image.png](/assets/branching.png)

Branching strategy example

The following branch names are preferable:

- bugfix/workitem-description
- feature/workitem-description

The branch should accurately describe the type of change. Any new features should always begin with feature/. Any fixes without any new features should always begin with bugfix/.

The workitem is optional but is encouraged as work items are useful for tracking the specified task for a sprint.

**Try to keep every branch as small in scope as possible to avoid a long running branch! Which could lead to not getting merged at all!**

However when a project has had it’s first go-live release the project is moved into it’s management phase. Versioning of the code is now imperative to be able to work on a upcoming Major or Minor release while still being able to hotfix the version in a live environment.

![image.png](/assets/releasing.png)

To do this efficiently we create release branches. Instead of branching any new feature or bugfix directly to the main branch, we first create a release branch for the version. For example **release/v1.1.0**. All features and bugfixes for the version v1.1.0 will then be branched of this release branch to then create the pull request to the release branch. This ensures that the main branch always is the branch currently running in the live environment. As such we can efficiently create a hotfix which requires fast deployment to the live environment.

## Commit conventions

The commit messages follows the [Conventional Commits 1.0.0](https://www.conventionalcommits.org/en/v1.0.0/#specification) standard. Below follows a quick summary of the conventions for this project.

[Commitlint](https://commitlint.js.org/) is enabled through husky hooks and is essential to ensure meaningfullness to commit messages.

### Summary

The Conventional Commits specification is a lightweight convention on top of commit messages. It provides an easy set of rules for creating an explicit commit history;
which makes it easier to write automated tools on top of.
This convention dovetails with [SemVer](http://semver.org/),
by describing the features, fixes, and breaking changes made in commit messages.

The commit message should be structured as follows:

---

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

---

The commit contains the following structural elements, to communicate intent to the
consumers of your library:

1. **fix:** a commit of the *type* `fix` patches a bug in your codebase (this correlates with `[PATCH](http://semver.org/#summary)` in Semantic Versioning).
2. **feat:** a commit of the *type* `feat` introduces a new feature to the codebase (this correlates with `[MINOR](http://semver.org/#summary)` in Semantic Versioning).
3. **BREAKING CHANGE:** a commit that has a footer `BREAKING CHANGE:`, or appends a `!` after the type/scope, introduces a breaking API change (correlating with `[MAJOR](http://semver.org/#summary)` in Semantic Versioning).
A BREAKING CHANGE can be part of commits of any *type*.´

### Types

| Type | Intent | Description |
| --- | --- | --- |
| feat | Features | A new feature |
| fix | Bug fixes | A bug fix |
| docs | Documentation | Docume­ntation only changes |
| style | Styles | Changes that do not affect the meaning of the code (white­-space, format­ting, missing semi-c­olons, etc) |
| refactor | Code Refact­oring | A code change that neither fixes a bug nor adds a feature |
| perf | Perfor­mance improv­ements | A code change that improves perfor­mance |
| test | Tests | Adding missing tests or correcting existing tests |
| build | Builds | Changes that affect the build system or external depend­encies (example scopes: gulp, broccoli, npm) |
| ci | Continuous integr­ations | Changes to our CI config­uration files and scripts (example scopes: Travis, Circle, Browse­rStack, SauceLabs) |
| chore | Chores | Other changes that don’t modify src or test files |
| revert | Reverts | Reverts a previous commit |

### Specif­ication

1. Commits **MUST** be prefixed with a type, which consists of a verb, feat, fix, etc., followed by a colon and a space.
2. The type feat **MUST** be used when a commit adds a new feature to your applic­ation or library.
3. The type fix **MUST** be used when a commit represents a bug fix for your applic­ation.
4. An optional scope **MAY** be provided after a type. A scope is a phrase describing a section of the codebase enclosed in parent­hesis, e.g., fix(pa­rser):
5. A descri­ption **MUST** immedi­ately follow the type/scope prefix. The descri­ption is a short descri­ption of the pull request, e.g., fix: array parsing issue when multiple spaces were contained in string.
6. A longer commit body **MAY** be provided after the short descri­ption. The body **MUST** begin one blank line after the descri­ption.
7. A footer **MAY** be provided one blank line after the body. The footer **SHOULD** contain additional meta-i­nfo­rmation about the pull-r­equest (such as the issues it fixes, e.g., fixes #13, #5).
8. Breaking changes **MUST** be indicated at the very beginning of the footer or body section of a commit. A breaking change **MUST** consist of the uppercase text `BREAKING CHANGE`, followed by a colon and a space. Optionally a `!` **CAN** be appended after the type/scope
9. A descri­ption **MUST** be provided after the `BREAKING CHANGE:` , describing what has changed about the API, e.g., `BREAKING CHANGE:` enviro­nment variables now take precedence over config files.
10. Types other than feat and fix **MAY** be used in your commit messages.

### Examples

### Commit message with description and breaking change footer

```
feat: allow provided config object to extend other configs

BREAKING CHANGE: `extends` key in config file is now used for extending other config files
```

### Commit message with `!` to draw attention to breaking change

```
feat!: send an email to the customer when a product is shipped
```

### Commit message with scope and `!` to draw attention to breaking change

```
feat(api)!: send an email to the customer when a product is shipped
```

### Commit message with both `!` and BREAKING CHANGE footer

```
chore!: drop support for Node 6

BREAKING CHANGE: use JavaScript features not available in Node 6.
```

### Commit message without body

```
docs: correct spelling of CHANGELOG
```

### Commit message with scope

```
feat(lang): add Polish language
```

### Commit message with body and footer

```
fix: prevent racing of requests

Introduce a request id and a reference to latest request. Dismiss
incoming responses other than from latest request.

Remove timeouts which were used to mitigate the racing issue but are
obsolete now.
```