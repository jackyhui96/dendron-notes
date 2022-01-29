---
id: ac615334-69f5-4f93-9ec1-7baf7006485e
title: Test
desc: ''
updated: 1647959690991
created: 1610988868765
---

# Erlang Tests





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

## Check which process has the most binaries
f(Bins).
Bins = fun() ->
    lists:sort(
    fun({K1,V1},{K2,V2}) -> {V1,K1} =< {V2,K2} end,
    lists:foldl(
        fun(P, A) ->
        {binary, Bins} = erlang:process_info(P, binary),
        [{P, length(Bins)}|A]
        end, [],
        processes()
        )
    )
end.

## Profiling and Benchmarking witihin remote shell
```erlang
eprof:start(), eprof:start_profiling([list_to_pid("<0.2415.0>")]).
timer:sleep(10000), eprof:start_profiling(), eprof:analyze(total).
```
