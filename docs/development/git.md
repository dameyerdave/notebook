# Git

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
name: 'Issue Report'
about: 'You want to report an issue.'
labels: 'Issue'
---

## Issue Report

### Summary of Issue 
<!-- (just a few sentences) -->

### Actual Behavior

### Expected Behavior

### Steps to Reproduce
```

