---
id: ac615334-69f5-4f93-9ec1-7baf7006485e
title: Test
desc: ''
updated: 1620648199647
created: 1610988868765
---

# Erlang Tests


## CT Suites
```
Run a single CT test which is defined in a group
    - make ct-http t=http_compress:headers_dupe

Run a single CT test if there are no groups
    - make ct-http c=headers_dupe
```

## EUnit


## Test Tips
https://medium.com/erlang-battleground/the-missing-testing-tip-628686ebbbda

## Config
Test if valid erlang config
```sh

find target -type f -name "*sys.config"  | \
ls _rel/config/dte_web_com/dte/releases/config/*.config | erl -noshell -eval '
    Input = list_to_binary(io:get_chars("", 1000000)),
    Files = binary:split(Input, [<<"\n">>, <<" ">>], [global, trim_all]),
    io:format("Testing File ~p~n",[Files]),
    CheckFun = 
        fun(FileName) ->
            case file:consult(FileName) of
                {ok,_} ->
                    io:format("Erlang config '~p' - OK~n",[FileName]);
                {error, {Line, _Mod, Reason}} ->
                    io:format("Unable to parse ~p at line ~p with reason ~p~nINVALID CONFIG~n", [FileName, Line, Reason]),
                    halt(1);
                _ ->
                    io:format("Unable to parse ~p ~nINVALID CONFIG~n", [FileName]),
                    halt(1)
            end
        end,
    [CheckFun(File) || File <- Files]
' -eval 'init:stop()'
```
