# Git Flow

Git Flow is a branching model that helps keep repositories clean, clear, and orderly. With Git Flow, there are five different kinds of branches:

- Feature branches
- Develop branch
- Release branches
- Hotfix branches
- Master branch

Each branch has it's own set of guidelines. Let's start with Feature branches.

## Feature Branches

Feature branches are exactly what they sound like: branches that are created for specific features. For example, if building a slideshow, create a new branch titled "slideshow." Feature branches should never be pushed to the remote. Instead, once a feature is complete, it gets merged in to the develop branch, and the feature branch is deleted.

### Creating a Branch

When starting work on a new feature, create a new branch off of develop.

```
git checkout -b slideshow develop
```

### Commiting to the Branch

From here, write any code needed for the feature, committing as necessary. Typically it's best to commit when finishing a section of the larger feature, rather than one commit for the entire feature. For example, the commit titles may be something like:

- PHP to display the slideshow images
- PHP to display the slideshow thumbnails
- Styles for slides
- Styles for slide thumbnails
- JavaScript function to handle transitioning between slides
- JavaScript to automatically slide ever 5 seconds

Note that all commits in a feature branch should relate directly to that feature. If a bug is found in another area of the project while coding the feature, `checkout develop`, fix the issue, then `merge --no-ff develop` back in to the feature. This is to make sure all commits are clearly organized.

### Merging the Branch in to Develop

Once the feature is finished, merge it back in to develop. Make sure to use the `--no-ff` flag in order to prevent a fast forward merge, to make sure the network tree is maintained.

```
git checkout develop
git merge --no-ff slideshow
```

Once the feature branch has been merged in to develop, it should be deleted, and develop should be pushed.

```
git branch -d slideshow
git push origin develop
```

And that's it for feature branches! Once the feature has been merged in to develop, any adjustments needed will be made in the develop branch.

## Develop Branch

The develop branch is where any bug fixes or adjustments can be made to features. This is the only branch other than master that should be pushed to the remote.

### Creating the Branch

The develop branch only needs created once, typically at the start of a project. To do so, simply use:

```
git checkout -b develop master
```

### Committing to Develop

Commits should only be made to the develop branch when making changes to existing features. For example, if adding pagination arrows to the slideshow, do so in the develop branch.

The commits make look something like:

- PHP to display slideshow pagination arrows
- Styles for slideshow pagination arrows
- JavaScript to handle clicking on slideshow pagination arrows

A few more examples of when a commit would be made to the develop branch may be:

- Fixing bugs
- Changing variables
- Adding tracking scripts
- Adding something to an existing feature

Essentially, any change that don't make sense as an entirely new feature should be made in develop.

## Release Branches

When an update is ready to be pushed live, a new release branch should be created. This branch should not be pushed to the remote.

### Creating the Branch

The name of a new release branch should be `release-` along with a major\* or middle bump to the version number.

```
git checkout -b release-1.1.0
```

\*A major bump should only be made when wide reaching changes have been made. Examples include a new/refreshed design, recoding a site responsively, etc.

### Commiting to the Branch

The very first commit of every release branch should rev the version number in package.json and update the CHANGELOG.md.

In package.json, update the "version" string to the new version. It may look something like:

```
{
  "name": "example-project",
  "description": "An awesome new project",
  "version": "1.1.0",
  "repository": "https://example.com/path/to/the/repo",
  "license": "NO-LICENSE",
  "devDependencies": {
    ...
  }
}
```

Next up, the CHANGELOG.md should be updated detailing the changes that where made for this release. It may look something like:

```
# Changelog

## v1.1.0

- Added a slideshow
- Fixed an issue where content with floated content could sometimes overflow its wrapper

## v1.0.1

- Fixed an issue where navigation drop downs where layered behind the content

## v1.0.0

- Initial Release
```

Finally, make the commit:

```
git commit -a -m "Revved version to 1.1.0"
```

After updating the package.json and CHANGELOG.md, any additional commits should only contain bug fixes. If additional features need added at this point, they'll need to wait for the next release.

### Merging the Branch in to Master (& Develop)

Once all bugs have been fixed, the release is ready to be merged in to the master branch. Make sure to use the `--no-ff` flag in order to prevent a fast forward merge, to make sure the network tree is maintained.

```
git checkout master
git merge --no-ff release-1.1.0
```

Once the branch has been merged, a new tag will be added to mark the release.

```
git tag -a v1.1.0
```

This will open Vim, prompting for a title and description for the tag. The title should be "Release v1.1.0", and the message should be the list that was entered in to the CHANGELOG.md.

```
Release v1.1.0
- Added a slideshow
- Fixed an issue where content with floated content could sometimes overflow its wrapper
```

The next step is to merge the release branch in to develop, and delete it. Make sure to use the `--no-ff` flag in order to prevent a fast forward merge, to make sure the network tree is maintained.

```
git checkout develop
git merge --no-ff release-1.1.0
git branch -d release-1.1.0
```

Finally, push the commits to both develop and master to the remote. Make sure to use the `--follow-tags` flag when pushing master in order to push the tag that was created.

```
git push origin develop
git push origin master --follow-tags
```

## Hotfix Branches

Hotfix branches shouldn't be used often. Their purpose is to quickly patch live code when a critical bug is found.

### Creating the Branch

The name of a new hotfix branch should start with `hotfix-` along with a minor bump to the version number.

```
git checkout -b hotfix-1.1.1
```

### Committing to the Branch

The very first commit of every hotfix branch should rev the version number in package.json.

```
{
  "name": "example-project",
  "description": "An awesome new project",
  "version": "1.1.1",
  "repository": "https://example.com/path/to/the/repo",
  "license": "NO-LICENSE",
  "devDependencies": {
    ...
  }
}
```

Finally, make the commit:

```
git commit -a -m "Revved version to 1.1.1"
```

Following commits should only contain bug fixes. A commit message may look something like:

```
Fixed slide layering
Incorrect z-index was causing the first slide in the list to always be layered on top
```

Finally, the CHANGELOG.md should be updated detailing the fixes that where made for this hotfix. It may look something like:

```
# Changelog

## v1.1.1

- Fixed slide layering

## v1.1.0

- Added a slideshow
- Fixed an issue where content with floated content could sometimes overflow its wrapper

## v1.0.1

- Fixed an issue where navigation drop downs where layered behind the content

## v1.0.0

- Initial Release
```

Commit the changelog, and then move on to merge the hotfix in to both master & develop.

```
git commit -m "Updated the changelog for hotfix 1.1.1"
```

### Merge the Branch in to Master (& Develop)

Once all bugs have been fixed, the hotfix is ready to be merged in to the master branch. Make sure to use the `--no-ff` flag in order to prevent a fast forward merge, to make sure the network tree is maintained.

```
git checkout master
git merge --no-ff hotfix-1.1.1
```

Once the branch has been merged, a new tag will be added to mark the hotfix.

```
git tag -a v1.1.1
```

This will open Vim, prompting for a title and description for the tag. The title should be "Hotfix v1.1.1", and the message should be the list that was entered in to the CHANGELOG.md.

```
Release v1.1.1
- Fixed slide layering
```

The next step is to merge the hotfix branch in to develop, and delete it. Make sure to use the `--no-ff` flag in order to prevent a fast forward merge, to make sure the network tree is maintained.

```
git checkout develop
git merge --no-ff hotfix-1.1.1
git branch -d hotfix-1.1.1
```

Finally, push the commits to both develop and master to the remote. Make sure to use the `--follow-tags` flag when pushing master in order to push the tag that was created.

```
git push origin develop
git push origin master --follow-tags
```

## Master Branch

Commits should never be made directly in the master branch. Changes are only made to the master branch when a new release is issued.
