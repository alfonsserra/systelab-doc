# Versioning

Systelab libraries version numbers indicate the level of changes that are introduced by the release. This use of [semantic versioning](https://semver.org/) helps you understand the potential impact of updating to a new version.

Version numbers have three parts: major.minor.patch. For example, version 5.2.9 indicates major version 5, minor version 2, and patch version 9.

The version number is incremented based on the level of change included in the release.

Major releases contain significant new features, some but minimal developer assistance is expected during the update. When updating to a new major release, you may need to run update scripts, refactor code, run additional tests, and learn new APIs.

Minor releases contain new smaller features. Minor releases are fully backward-compatible; no developer assistance is expected during update, but you can optionally modify your apps and libraries to begin using new APIs, features, and capabilities that were added in the release. We update peer dependencies in minor versions by expanding the supported versions, but we do not require projects to update these dependencies.

Patch releases are low risk, bug fix releases. No developer assistance is expected during update.

# Branches

## Working branches

Working branches should be named according to the following pattern:

{BaseBranch}-{Type}{Issue#}-{IssueShortTitle}

Where:
- {BaseBranch}: Name of the maintenance branch or master used to create the working branch
- {Type}: Letter indicating the type of issue addressed on the branch
    - F: New feature
    - B: Bug
- {Issue#}: GitHub issue number associated to the feature or defect to be addressed on the branch. That would allow better tracking between branches and change description.
- {ShortTitle}: Short title of the change. Written using [UpperCamelCase](https://es.wikipedia.org/wiki/CamelCase)

Examples
- master-B12-DisableDragAndDrop
- 4.1.x-F68-RoleDirective


## Maintenance branches

After a feature release, it is needed to manage a maintenance branch.

First, if you wish to continue to release maintenance fixes for the feature release made before the recent one, then you must create another branch to track commits for that previous release.

To do this, the feature branch is copied to another branch named with the previous release version number.

Maintenance branches will be named as Major.Minor.x, for example 5.12.x

Rules to 'Require pull request reviews before merging' must be applied to every maintenance branch. You can use wildcards in order to do so: \[1-9]\*.* will do the work

### Branching procedure

For a new change:

- If it is minor change, the contributor should create a new maintenance branch, for example 5.13.x
- If it is major change (this is usually something that you should do from the master branch), the contributor should create a new maintenance branch, for example 6.0.x.
- You do not need to create a new branch for a patch change.

In order to add changes to a maintenance branch:

 - Create a new working branch from the maintenance branch.
 - Commit the changes to the new working branch.
 - Create a Pull Request from the working branch to the maintenance branch.
 - Once the Pull Request is approved it is time to merge the changes. Will be the submitter the responsible for merging.
 - Finally, the working branch could be removed.

> Before creating the PR, be sure to update, as needed, the npm library version in the package.json file.

### Bug fixing policy

When addressing a bug detected on a branch, it should be fixed at least on:
- The maintenance branch where needed
- The master branch

Detected bugs should be tracked as repository issues with the 'Bug' tag. So, their history should indicate for which versions the defect has been fixed.

# Releasing

## Library Release

The submitter should create a new release, with the tag version vX.Y.Z and release title X.Y.Z.

Travis will publish the library to npm.

## Application Release

> Application, should never rely on libraries that the source code is not on a maintenance branch. So, it will be each project responsibility to check that the library is in a maintenance branch, or otherwise create it.



