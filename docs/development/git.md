# Git

## Install github cli

```bash
brew install hub
```

## Contribute to git repo

1. `Fork` the repo to your github account
2. Clone the forked repo

```bash
git clone https://dameyerdave@github.com:dameyerdave/repo.git
```

3. Change the directory to the repo

```bash
cd repo
```

4. Add an `upstream`

```bash
git remote add upstream https://dameyerdave@github.com:original_user/repo.git
```

5. Prepare vscode to not format/pretty/lint

`.prettierrc`

```json
{}
```

`.vscode/settings.json`

```json
{
    "editor.formatOnSave": false,
    "python.linting.Pylintnabled": false,
    "python.linting.flake8enabled": false
}
```

6. Create a branch etc...

```bash
git checkout master
git pull upstream master
git push origin master
git checkout -b [hotfix|feature]/description
```

7. Apply your changes

8. Commit your changes

```bash
git commit -am 'commit message'
```

9. Push your changes

```bash
git push -u origin [hotfix|feature]/description
```

10. Compare and generate a `pull request` on the upstream repo

## Syncing a fork

1. Fetch the branches and their respective commits from the upstream repository

```bash
git fetch upstream
```

2. Check out your fork's local `master` branch

```bash
git checkout master
```

3. Merge the changes from upstream/master into your local master branch

```bash
git merge upstream/master
```

## Tagging

### Create (and push) a tag

```bash
git tag -a v1.4 -m 'my version 1.4'
git push origin --tags
```

### Delete a tag

```bash
git tag -d v1.4
```

### Checkout a tag

```bash
git checkout -b v1.4 v1.4
```

## Create issue templates

1. Create a folder called `.github/ISSUE_TEMPLATE` in your repository

```bash
mkdir -p .github/ISSUE_TEMPLATE
```

2. Create as many templates you want using the following markdown template

```md
---
name: API Bug Report
about: You want to report a bug in the API.
title: "[TITLE]"
labels: Bug, API
---

### Summary

<!-- Summarize the bug encountered concisely -->

### Steps to reproduce

<!-- How one can reproduce the issue - this is very important -->

### Example page (Optional)

<!-- If possible, please provide the URL of the page here that exhibits the problematic behavior -->

### What is the current *bug* behavior?

<!-- What actually happens -->

### What is the expected *correct* behavior?

<!-- What you should see instead -->

### Relevant screenshots and/or logs

<!-- Paste any relevant screenshots -->
```

## Completely remote file fom git repo

&rarr; see [here](https://itextpdf.com/en/blog/technical-notes/how-completely-remove-file-git-repository)

### Keep the file locally

```bash
git rm --cached $FILE
echo $FILE >> .gitignore
git add .gitignore
git commit --amend --no-edit
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push --force-with-lease origin master
```

### Delete the file locally

```bash
git rm $FILE
git commit --amend --no-edit
git reflog expire --expire=now --all && git gc --prune=now --aggressive
git push --force-with-lease origin master
```

## Revert last local commit (keep changes)

```bash
git reset --soft HEAD~1
```

## Revert last local commit (delete changes)

```bash
git reset --hard HEAD~1
```

## Remove a file from the previous commit

```bash
git reset --soft HEAD~1
git reset HEAD path/to/unwanted_file
git commit -c ORIG_HEAD  
```

## Revert to a previous commit (delete changes)

This can be used to go back in history and restart committing from there on.

```bash
git reset --hard 'your last working commit hash'
git clean -f -d
git push -f
```

## Delete commits in between (locally only)

&rarr; See [here](https://www.clock.co.uk/insight/deleting-a-git-commit)

```bash
git rebase --onto <branch name>~<first commit number to remove> <branch name>~<first commit number to keep> <branch name>
```

> To get the `commit number` use `xpgl` from [this git repo](https://github.com/dameyerdave/devutils).

## Delete branch

### List branches

```bash
git branch    <-- lists local branches
git branch -r <-- lists remote branches
git branch -a <-- lists local and remote branches
```

### Delete branch locally

```bash
git branch -d localBranchName
```

### Delete branch remotely

```bash
git push origin --delete remoteBranchName
```

### Get a list of files included in a commit

```bash
git show --pretty="" --name-only bd61ad98
```