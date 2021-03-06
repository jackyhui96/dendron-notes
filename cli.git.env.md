---
id: d0d5e5fb-fd00-4d0f-90a6-dbf3158497de
title: Env
desc: variables relevant for command
updated: 1599319533298
created: 1599319533298
---

# Git Environment

## gitignore file
- A blank line matches no files, so it can serve as a separator for readability.
- A line starting with `#` serves as a comment.
- An optional prefix `!` which negates the pattern; any matching file excluded by a previous pattern will become included again. If a negated pattern matches, this will override lower precedence patterns sources.
- If the pattern ends with a slash, it is removed for the purpose of the following description, but it would only find a match with a directory. In other words, `foo/` will match a directory `foo` and paths underneath it, but will not match a regular file or a symbolic link `foo` (this is consistent with the way how pathspec works in general in git).
- If the pattern does not contain a slash `/`, git treats it as a shell glob pattern and checks for a match against the pathname relative to the location of the .gitignore file (relative to the toplevel of the work tree if not from a `.gitignore` file).
- Otherwise, git treats the pattern as a shell glob suitable for consumption by `fnmatch(3)` with the `FNM_PATHNAME` flag: wildcards in the pattern will not match a `/` in the pathname. For example, `Documentation/*.html` matches `Documentation/git.html` but not `Documentation/ppc/ppc.html` or `tools/perf/Documentation/perf.html`.
A leading slash matches the beginning of the pathname. For example, `/*.c` matches `cat-file.c` but not `mozilla-sha1/sha1.c`.

### example .gitignore
```sh
#OS junk files
[Tt]humbs.db
*.DS_Store

#Visual Studio files
*.[Oo]bj
*.user
*.aps
*.pch
*.vspscc
*.vssscc
*_i.c
*_p.c
*.ncb
*.suo
*.tlb
*.tlh
*.bak
*.[Cc]ache
*.ilk
*.log
*.lib
*.sbr
*.sdf
ipch/
obj/
[Bb]in
[Dd]ebug*/
[Rr]elease*/
Ankh.NoLoad

#Tooling
_ReSharper*/
*.resharper
[Tt]est[Rr]esult*

#Project files
[Bb]uild/

#Subversion files
.svn

# Office Temp Files
~$*
```


