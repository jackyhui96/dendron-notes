---
id: pNrmBimLM3sgVkAbQWftD
title: Mk
desc: ''
updated: 1643448338516
created: 1643272890830
---

# Erlang.mk

## Fixes
### Using older git
* `dep_autopatch_appsrc.erl` has been modified to replace the `-C` flag with `--git-dir=` and append `.git` to the git directory, making the command work with git 1.8.3
* https://github.com/ninenines/erlang.mk/issues/924

### Handling deps that aren't started on boot
* e.g. Post office in the LTS isn't started until the LTS is enabled
```makefile
DEPS_NOT_STARTED_ON_BOOT = post_office

BUILD_DEPS = $(DEPS_NOT_STARTED_ON_BOOT)
REL_DEPS = $(DEPS_NOT_STARTED_ON_BOOT)
```


### Ignore test deps that aren't used in release
```makefile
IGNORE_DEPS = edown test_node_utils
```

## Erlang Tests

### CT Suites
```
Run a single CT test which is defined in a group
    - make ct-http t=http_compress:headers_dupe

Run a single CT test if there are no groups
    - make ct-http c=headers_dupe

Running docker tests (replace all with suite name)
    - make docker-build-ct
    - make docker-test TEST=all

Adding erlang config to erlang.mk
    - add to CT_OPTS: -erl_args -config <path> 
    - need to have erl_args
```

### EUnit
    `make eunit TAGGED_EUNIT_TESTS='{​​​​​​module, <module>}​​​​​​'`
