---
id: 79ff0322-976d-4f93-b5f1-f76fc9e39c75
title: Grep
desc: ''
updated: 1609237875468
created: 1609237858255
---

# Grep

## Advanced Perl Patterns
```sh
Extension         Meaning
---------         -------
(?:...)           Cluster-only parentheses, no capturing
(?#...)           Comment, discard all text between the parens
(?imsx-imsx)      Enable/disable pattern modifiers
(?imsx-imsx:...)  Cluster-only parens with modifiers
(?=...)           Positive lookahead assertion
(?!...)           Negative lookahead assertion
(?<=...)          Positive lookbehind assertion
(?<!...)          Negative lookbehind assertion
(?()...|...)      Match with if-then-else
(?()...)          Match with if-then
(?>...)           Match non-backtracking subpattern ("once-only")
(?R)              Recursive pattern
```

_Reference:_
https://caspar.bgsu.edu/~courses/Stats/Labs/Handouts/grepadvanced.htm