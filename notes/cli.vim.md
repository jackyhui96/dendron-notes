---
id: e30182bb-dec6-4f35-b19e-400478c4e0a3
title: Vim
desc: ''
updated: 1652951803670
created: 1603196018803
---

# VIM

## Regex Replace
Find each occurrence of 'foo' (in all lines), and replace it with 'bar'.
```vim
:%s/foo/bar/g
```
Change each 'foo' to 'bar', but ask for confirmation first.
```vim
:%s/foo/bar/gc
```
Change only whole words exactly matching 'foo' to 'bar'; ask for confirmation.
```vim
:%s/\<foo\>/bar/gc
```

## Navigation
### Moving to matching braces
The `%` key can be used for the following :

To jump to a matching opening or closing parenthesis, square bracket or a curly brace: `([{}])`
To jump to start or end of a C-style comment: `/* */`.
To jump to a matching C/C++ preprocessor conditional: `#if`, `#ifdef`, `#else`, `#elif`, `#endif`.
To jump between appropriate keywords, if supported by the ftplugin file, for example, between `begin` and `end` in a Pascal program.


## Pasting verbatim
Do this so that pasting doesn't go weird, when it sees a comment
```vim
:set paste
:set nopaste
```

## Line numbers
```vim
:set nu
:set number
```
