---
id: fde0884c-1f69-404e-9906-7f44903cdfb4
title: Git
desc: null
updated: 1698143900454
created: 1613950849582
---

## Examples
```sh
## Clone example
git clone ssh://git@github.com/<user>/<repository name>.git

## Compare file with git branch
git diff mybranch.. myfile

## Diff and show file names changed
git diff --name-only SHA1 SHA2

## Remove something that you no longer want tracked, but keep file locally
git rm -r --cached file

## rebase onto origin/master always preferring working branch if conflict (theirs)
git rebase -s recursive -X theirs origin/master

## reset the date to now, when rebasing
git rebase --ignore-date

## reset the date to now, when rebasing
git rebase --reset-author-date

## reset the author
git commit --amend --reset-author

## push up the branch
bash -c "`git push 2>&1 | grep -Po 'git push.*'`"
```

## Patches
```sh
## Create a patch for current branch to target branch
git format-patch integration --stdout > patch_name.patch

## Apply patch to current branch
git am < patch_name.patch
```
