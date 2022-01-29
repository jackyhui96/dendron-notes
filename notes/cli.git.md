---
id: fde0884c-1f69-404e-9906-7f44903cdfb4
title: Git
desc: null
updated: 1652951684080
created: 1613950849582
---

## Examples
```sh
## Clone example
git clone ssh://git@github.com/<user>/<repository name>.git

## Compare file with git branch
git diff mybranch.. myfile
```

## Patches
```sh
## Create a patch for current branch to target branch
git format-patch integration --stdout > patch_name.patch

## Apply patch to current branch
git am < patch_name.patch
```
