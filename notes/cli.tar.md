---
id: 69cc4b72-a98e-4133-8dcc-2b45d2456101
title: Tar
desc: null
updated: 1595952505022
created: 1652817063414
---

# Overview
- creates and manipulates streaming archive files

![tar bomb](assets/2020-07-06-13-40-10.png)

# Synopsis
```
tar [bundle-flags <args] [<file> | <pattern> ...]
```
# Options

- -c: create new archive
- -d: find difference bwt files in the archive
- -v: verbose
- -f: specify filename
- -x: extract file
- -j: Open up a bzip2 file
- -z: file archive through gzip
- -C: change directory before adding

# Examples

```
## Create tgz
tar -czvf archive.tgz source_file

## Create tar.gz 
tar -cvzf archive.tar.gz source_file

## Open a tar
tar -xvf yourfile.tar

## Open a bz2 file
tar -vxjf mm_binary.tar.bz2

## Open a tar.gz
tar -xvzf archive.tar.gz 
```
