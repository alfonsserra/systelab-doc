# Versioning

Version numbers indicate the level of changes that are introduced by the release. The use of [semantic versioning](https://semver.org/) helps you understand the potential impact of updating to a new version.

Version numbers have three parts: major.minor.patch. For example, version 5.2.9 indicates major version 5, minor version 2, and patch version 9.

The version number is incremented based on the level of change included in the release.

Major releases contain significant new features, some but minimal developer assistance is expected during the update. When updating to a new major release, you may need to run update scripts, refactor code, run additional tests, and learn new APIs.

Minor releases contain new smaller features. Minor releases are fully backward-compatible; no developer assistance is expected during update, but you can optionally modify your apps and libraries to begin using new APIs, features, and capabilities that were added in the release. We update peer dependencies in minor versions by expanding the supported versions, but we do not require projects to update these dependencies.

Patch releases are low risk, bug fix releases. No developer assistance is expected during update.

# Branching

Currently, two popular development approaches can be considered for branching: Git flow and trunk-based development. Both have their own pros and cons.

In most cases we are going to use Git flow for our projects, but for the libraries, trunk-based development could be the best option to iterate quickly.


## Git FLow

In the Git flow development model, one main development branch is considered.

Feature branches are created from de development branch and once they are done, pull requests are created.

Once the pull requests are accepted and merged to the main branch, and it’s decided that the main branch has reached enough maturity to be released,
a separate branch is created to prepare a final version.
In this branch the application is tested and fixing is done. After this, the branch is merged with the master branch and tag it with the release version.
In the meantime, new features can be developed on the develop branch.

## Trunk-based Development Workflow

In the trunk-based development model, all developers work on a single branch with open access to it.

Short-lived feature branches are created in order to develop new features, and once code on their branch compiles and passes all tests, the developers merge it straight to master. It ensures that development is truly continuous and prevents developers from creating merge conflicts that are difficult to resolve.

# Angular libraries

## Branching
Trunk-based development model has been selected for branching.

### Feature branches

Feature branches should be named according to the following pattern:

feature-{IssueShortTitle}

where {ShortTitle} is written using [UpperCamelCase](https://es.wikipedia.org/wiki/CamelCase)

Examples
- feature-DisableDragAndDrop
- feature-RoleDirective

### Release branches

After a release, it is needed to manage a release branch.

Release branches will be named as release-Major.Minor.x, for example release-5.12.x

Rules to 'Require pull request reviews before merging' must be applied to every release branch. You can use wildcards in order to do so: release-* will do the work

#### Branching procedure

For a new change:

- If it is minor change, the contributor should create a new release branch, for example 5.13.x
- If it is major change (this is usually something that you should do from the master branch), the contributor should create a new release branch, for example 6.0.x.
- You do not need to create a new branch for a patch change.

In order to add changes to a release branch:

 - Create a new feature branch from the release branch.
 - Commit the changes to the new feature branch.
 - Create a Pull Request from the feature branch to the release branch.
 - Once the Pull Request is approved it is time to merge the changes. Will be the submitter the responsible for merging.
 - Finally, the feature branch could be removed.

> In Angular, before creating the PR, be sure to update, as needed, the npm library version in the package.json file.

## Bug fixing policy

When addressing a bug detected on a branch, it should be fixed at least on:
- The release branch where needed
- The master branch

Detected bugs should be tracked as repository issues with the 'Bug' tag. So, their history should indicate for which versions the defect has been fixed.

## Releasing

### Release

The submitter should create a new release, with the tag version vX.Y.Z and release title X.Y.Z.

For Angular libraries, Travis will publish the library to npm.

### Application Release

> Application, should never rely on libraries that the source code is not on a release branch. So, it will be each project responsibility to check that the library is in a release branch, or otherwise create it.



