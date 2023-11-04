---
id: a1a0eeiaf9nw20ek21q31wc
title: Erl
desc: ''
updated: 1687963580044
created: 1655882490236
---

# erl

## Examples
```bash
## Compile and run sequential Erlang program as a common script and then exit
erlc <FILES> && erl -noshell '<MYMODULE:MYFUNCTION(ARGUMENTS)>, init:stop().'

## Connect to a running Erlang node:
erl -remsh <NODENAME>@<HOSTNAME> -sname <CUSTOM_SHORTNAME> -hidden -setcookie <COOKIE_OF_REMOTE_NODE>

## Tell the Erlang shell to load modules from a directory
erl -pa <DIRECTORY_WITH_BEAM_FILES>

## one liner file http server
erl -s inets -eval 'inets:start(httpd,[{server_name,"NAME"},{document_root, "."},{server_root, "."},{port, 1111},{mime_types,[{"html","text/html"},{"htm","text/html"},{"js","text/javascript"},{"css","text/css"},{"gif","image/gif"},{"jpg","image/jpeg"},{"jpeg","image/jpeg"},{"png","image/png"}]}]).'
```