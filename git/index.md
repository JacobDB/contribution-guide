# Git

[Git Flow](git-flow.md) | [Style Guide](style-guide.md) | [Resources](resources.md)

In this section, you'll learn how to manage branches and write commits.

## Quick Notes

### Git Flow

```
# Feature Branch

git checkout -b feature-name develop # create a new branch from develop

# Develop Branch

git checkout develop           # switch to the develop branch
git merge --no-ff feature-name # merge the new feature (don't fast forward!)
git branch -d feature-name     # delete the feature branch
git push origin develop        # push the develop branch

# Release Branch

git checkout -b release-1.0.0 develop       # create a new branch from develop with the version number
# update package.json with the new version number
# update the CHANGELOG.md detailing the changes in this version
git commit -a -m "Revved version to v1.0.0" # commmit the version string change
# fix any remaining bugs, update changelog, commit as needed

# Master Branch

git checkout master                  # switch to the master branch
git merge --no-ff release-1.0.0      # merge the new release (don't fast forward!)
git tag -a v1.0.0                    # create a new tag with the version number
git checkout develop                 # switch to the develop branch
git merge --no-ff release-1.0.0      # merge the new release (don't fast forward!)
git branch -d release-1.0.0          # delete the release branch
git push origin master --follow-tags # push the master branch, with tags
git push origin develop              # push the develop branch

# Hotfix Branch

git checkout -b hotfix-1.0.1 master         # create a new branch from master, bumping the minor version by 1
# update the package.json with the new version number
# update the CHANGELOG.md detailing the hotfix
git commit -a -m "Revved version to v1.0.1" # commit the version string change
```

### Commit Messages

- Titles should be concise, describing the change in a general way
- Descriptions should contain specific notes on what was changed and why
- If fixing a bug, include "; Fixes #1" at the end of the Messages

#### Good Commits

```
Fixed a typo in _header.scss
```

```
PHP for the main navigation
- Set up a call to wp_nav_menu
- Created a new walker navWalker() to change the sub-menu class to -sub-list
```

```
Updated jQuery to v1.12.0; Fixes #47
Added the "jQuery.htmlPrefilter()" function to sanitize inputs
```

#### Bad Commits

```
Fixed a thing
```

```
Really fixed a thing this time
This was stupid
```

```
Ugh!
```
