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

5. Apply your changes

6. Create a branch etc...

```bash
git checkout master
git pull upstream master
git push origin master
git checkout -b [hotfix|feature]/description
```

7. Commit your changes

```bash
git commit -am 'commit message'
```

8. Push your changes

```bash
git push -u origin [hotfix|feature]/description
```

9. Compare and generate a `pull request` on github

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
