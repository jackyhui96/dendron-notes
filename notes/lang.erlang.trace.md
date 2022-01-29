---
id: VpcygsSZNUISZBahExllB
title: Trace
desc: ''
updated: 1643450656650
created: 1643450641790
---

# Erlang Tracing
```erlang
f(),
Self = self().
F = fun(F, SelfPid) ->
        receive
          stop ->
            ok;
          Msg ->
            %% SelfPid ! Msg,
            io:format("jacky: ~p~n", [Msg]),
            F(F, SelfPid)
        end
    end.
Tracer = proc_lib:spawn(fun() -> F(F, Self) end).
f(Match), Match = [{'_', [], [{return_trace}]}].
erlang:trace_pattern({pub_websocket_handler, subscribe, '_'}, Match, [local]).
erlang:trace(all, true, [call, {tracer, Tracer}, timestamp]).
ok.

erlang:trace(all, false, [call, timestamp, {tracer, Tracer}]).
Tracer ! stop.
ok.



f(),
Self = self().
F = fun(F, SelfPid) ->
        receive
          stop ->
            ok;
          Msg ->
            %% SelfPid ! Msg,
            io:format("jacky: ~p~n", [Msg]),
            F(F, SelfPid)
        end
    end.
Tracer = proc_lib:spawn(fun() -> F(F, Self) end).
f(Match), Match = [{'_', [], [{return_trace}]}].
erlang:trace_pattern({'_', '_', '_'}, Match, [local]).
erlang:trace(all, true, [call, {tracer, Tracer}, timestamp]).
erlang:trace(all, false, [call, {tracer, Tracer}, timestamp]).
Tracer ! stop.
```

## Garbage collection
```
trace_gc_calls_for_fun(Fun) ->
    Self = self(),
    TracerPid = garbage_collect_tracer_process_init(Self),
    Result = Fun(),
    TracerPid ! completed,
    Result.

garbage_collect_tracer_process_init(Pid) ->
    TracerFun = 
        fun() -> 
            erlang:trace(Pid, true, [garbage_collection, timestamp]),
            trace_fun(Pid)
        end,
    spawn(TracerFun).

trace_fun(Pid) ->
    InitialAcc = {undefined, undefined,{0,0,0}},
    erlang:trace(Pid, true, [garbage_collection, timestamp]),
    trace_fun(Pid, InitialAcc).

trace_fun(Master, {OldHeapStartSize, StartTimestamp, {GcTime, MajorGc, MinorGc} = Acc}) -> 
            receive 
                {trace_ts, _, gc_start, Info, Timestamp} -> 
                    OldSize = proplists:get_value(old_heap_block_size, Info),
                    trace_fun(Master, {OldSize, Timestamp, Acc});
                {trace_ts, _, gc_end, Info, Timestamp} -> 
                    OldSize = proplists:get_value(old_heap_block_size, Info),
                    case OldSize of
                        OldHeapStartSize ->
                            DiffTime = timer:now_diff(Timestamp, StartTimestamp),
                            % file:write_file("garbage_collect.log", io_lib:format("Pid:~p, Time:~p~n", [Master, DiffTime]), [append]),
                            trace_fun(Master, {OldHeapStartSize, StartTimestamp, {GcTime+DiffTime, MajorGc, MinorGc+1}});
                        _ ->
                            DiffTime = timer:now_diff(Timestamp, StartTimestamp),
                            % file:write_file("garbage_collect.log", io_lib:format("Pid:~p, Time:~p~n", [Master, DiffTime]), [append]),
                            trace_fun(Master, {OldSize, StartTimestamp, {GcTime+DiffTime, MajorGc+1, MinorGc}})
                    end;
                completed ->
                    Log = io_lib:format("Pid:~p, GC Total Time(micros):~p, Major GCs:~p, Minor GCs:~p~n", [Master, GcTime, MajorGc, MinorGc]),
                    file:write_file("garbage_collect.log", Log, [append])
            end.
```
