---
id: 8af8ad5e-138c-4471-b670-3d3474d07401
title: Erlang
desc: ''
updated: 1602246697398
created: 1602246697398
stub: false
---

# Erlang

## tail recursive efficiency
- Use foldr for simple building of lists (even if it needs reversing)
- simple building of lists i.e. size N input, size N output
- summary of references
  - foldr is generally faster as it avoids lists:reverse and uses the heap space it creates for all processing
  - foldl will be slower, if it needs a lists:reverse as we duplicate the memory allocation for the new list then use processing to garbage collect original list.
  - foldl will always be faster if a lists:reverse is not needed i.e. we don't care about order 

_References_
http://erlang.2086793.n4.nabble.com/Efficiency-of-a-list-construction-td3538122.html#a3538379
https://ferd.ca/erlang-s-tail-recursion-is-not-a-silver-bullet.html


## Advanced stuff about list sizes and sharing
_Reference: http://erlang.org/doc/efficiency_guide/processes.html_