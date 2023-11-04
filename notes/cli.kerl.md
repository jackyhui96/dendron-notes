---
id: c00a4301-e3a1-44d7-b5d9-b2435b020a51
title: Kerl
desc: ''
updated: 1670509805152
created: 1611320860843
---

# Kerl

## Activate erlang release
```sh
. <PATH_TO_KERL_INSTALLS>/<VSN>/activate
## e.g.
. /usr/local/erl_rel/22.3/activate

## find erl path
. $(dirname $(which erl | grep -Po ".*(?=/bin/erl)"))/22.3/activate
```

## Installing erlang
* install kerl (https://github.com/kerl/kerl/releases/tag/1.8.1) and erlang
    * run pre-req steps
        ```bash
        yum install gcc ncurses-devel automake autoconf openssl-devel

        ## for debugging with observers
        yum install compat-wxBase3-gtk2.x86_64 compat-wxGTK3-gtk2.x86_64 compat-wxGTK3-gtk2-devel.x86_64 compat-wxGTK3-gtk2-gl.x86_64 compat-wxGTK3-gtk2-media.x86_64 wxBase.x86_64 wxBase3.x86_64 wxGTK.x86_64 wxGTK-devel.x86_64 wxGTK-gl.x86_64 wxGTK-media.x86_64 wxGTK3.x86_64 wxGTK3-devel.x86_64 wxGTK3-gl.x86_64 wxGTK3-media.x86_64 wxGTK3-webview.x86_64

        ## ensure you have wx installed
        which wx-config
        ```
    * run `kerl build git <git_url> <tag> <name>`
    * run `kerl install <name> <target_path>`
    * run `. <install_path>/activate`
    * add the above to `.bashrc`

## Deactivate erlang release
kerl_deactivate
