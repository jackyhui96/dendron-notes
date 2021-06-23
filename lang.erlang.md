---
id: 8af8ad5e-138c-4471-b670-3d3474d07401
title: Erlang
desc: ''
updated: 1624463106237
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

## Implementation of Erlang Maps
- https://medium.com/@jlouis666/breaking-erlang-maps-1-31952b8729e6
- uses sorted array http://www.mathcs.emory.edu/~cheung/Courses/323/Syllabus/Map/ordered-map.html

## Advanced stuff about list sizes and sharing
_Reference: http://erlang.org/doc/efficiency_guide/processes.html_

## GB Tree stuff
_Reference: http://erlang.2086793.n4.nabble.com/gb-trees-and-dict-performance-td4715001.html_

## When to use ok tuple
```erlang
-spec {ok, some_value} || {error, reason}
```
_Reference: https://medium.com/@bruno_sapienza/when-to-return-the-ok-in-elixir-10c3c336870#:~:text=it's%20common%20to%20return%20tagged,related%20value(s)%20like%20the_

## Data Comparisons
https://www.theerlangelist.com/article/sequences


## Good resources
https://adoptingerlang.org/docs/cheat_sheets/
http://beam-wisdoms.clau.se/en/latest/

## Behaviours
Not all OTP behaviours are listed here, only thee most frequently-used ones.

### Applications
|Trigger|Called By|Handled By|Return|Description
|---|---|---|---|---|
|`application:start/1-2`|client or booting VM|`start(Type, Args)`|<code>{ok, pid()} &#124; {ok, pid(), State}</code>|should start the root supervisor
|`{start_phases, [{Phase, Args}]}` in app file|kernel booting the app|`start_phase(Phase, Type, Args)`|<code>ok &#124; {error, Reason}</code>|Optional. Can isolate specific steps of initialization
|`application:stop/1`|app shutting down|`prop_stop(State)`|`State`|Optional. Called before the supervision tree is shut down
|`application:stop/1`|app shutting down|`stop(State)`|`term()`|called once the app is done running to clean things up
|Hot code update|SASL’s release handler|`config_change(Changed::[{K,V}], New::[{K,V}], Removed::[K])`|`ok`|Called after a hot code update using the VM’s relup functionality, if the configuration values changed

### Supervisors
|Trigger|Called By|Handled By|Return|Description
|---|---|---|---|---|
|`supervisor:start_link/2-3`|parent process|`init(Arg)`|<code>ignore &#124; {ok, {SupFlag, [Child]}}</code>|Specifies a supervisor. Refer to official documentation

### gen_server
|Trigger|Called By|Handled By|Return|Description
|---|---|---|---|---|
|`gen_server:start_link/3-4`|supervisor|`init(Arg)`|<code>{ok, State [, Option]} &#124; ignore &#124; {stop, Reason}</code>|Set up the initial state of the process
|`gen_server:call/2-3`|client|`handle_call(Msg, From, State)`|<code>{Type::reply &#124; noreply, State [, Option]} &#124; {stop, Reason [, Reply], State}</code>|Request/response pattern. A message is received and expects an answer
|`gen_server:cast/2`|client|`handle_cast(Msg, State)`|<code>{noreply, State [, Option]} &#124; {stop, Reason, State}</code>|Information sent to the process; fire and forget
|`Pid ! Msg`|client|`handle_info(Msg, State)`|same as `handle_cast/2`|Out-of-band messages, including monitor signals and `'EXIT'` messages when trappig exit
|Setting an Option value to `{continue, Val}`|the server itself|`handle_continue(Val, State)`|same as `handle_cast/2`|Used to break longer operations into triggerable internal events
|`gen_server:stop/1,3`|client or supervisor|`terminate(Reason, State)`|`term()`|Called when the process is shutting down willingly or through errors. If the process does not trap exits, this callback may be omitted
|`sys:get_status/2-3`, crash logs|client, the server itself|<code>format_status(normal &#124; terminate, [PDict, State])</code>|<code>[{data, [{"State", Term}]}]</code>|Used to add or remove information that would make it to debugging calls or error logs
|N/A|supervisor|`code_change(OldVsn, State, Extra)`|`{ok, NewState}`|called to update a stateful process if the proper instructions are given during a hot code upgrade with releases
### gen_statem
#### Process management
|Trigger|Called By|Handled By|Return|Description
|---|---|---|---|---|
|`gen_statem:start_link/3-4`|supervisor|`init(Arg)`| <code>{ok, State, Data [, Actions]} &#124; ignore &#124; {stop, Reason}</code>|Sets the initial state and data for the state machine
|N/A|internal|`callback_mode()`|<code>[state_functions &#124; handle_event_function [, state_enter]]</code>|Defines the type of FSM and whether entering a state triggers a special internal event
|`gen_statem:stop/1,3`|client or supervisor|`terminate(Reason, State, Data)`|`term()`|Called when the process is shutting down willingly or through errors. If the process does not trap exits, this callback may be omitted
|`sys:get_status/2-3`, crash logs|client, the server itself|<code>format_status(normal &#124; terminate, [PDict, State, Data])</code>|`[{data, [{"State", Term}]}]`|Used to add or remove information that would make it to debugging calls or error logs
|N/A|supervisor|`code_change(OldVsn, State, Data, Extra)`|`{ok, NewState, NewData}`|called to update a stateful process if the proper instructions are given during a hot code upgrade with releases

#### State handling and transitions
Handled by either `handle_event/4` or `StateName/3` functions, based on the value of `callback_mode()`. 
The function signatures are either:
* `handle_event(EventType, EventDetails, State, Data)`
* `State(EventType, EventDetails, Data)`

If the value of `State` is not a list, even though `callback_mode()` defined `state_functions`, then `handle_event/4` will be called. All possible return values for either functions are one of:
* `{next_state, State, Data}`
* `{next_state, State, Data, [Actions, ...]}`
* `{stop, Reason, Data}`
* `{stop, Reason, Data, [Actions, ...]}`

Various short forms exist, such as `keep_state_and_data`, `{keep_state, Data}`, `{repeat_state, Data}`, and many more. Refer to the documentation for their content.

The `Actions` value is any combination of the following list (non-inclusive): `postpone`, `{next_event, EventType, EventDetails}`, `hibernate`, `{timeout, Delay, EventDetails}`, `{state_timeout, Delay, EventDetails}`, `{reply, From, Reply}`. Consult the documentation for more options.

|Trigger|Called By|Event Type|Event Details|Description
|---|---|---|---|---|
|`gen_statem:call/2-3`|client|`{call, From}`|`term()`|Request/response pattern. A message is received and is expected to receive an answer
|`gen_statem:cast/2`|client|`cast`|`term()`|Information must be sent to the process; fire and forget
|`Pid ! Msg`|client|`info`|`Msg`|Out-of-band messages, including monitor messages and 'EXIT' signals that are trapped
|`{timeout, T, Msg}`|`Action` return value|`timeout`|`Msg`|A specific timeout that can be set and received internally when the state machine has not received a new event in `T` milliseconds
|`{state_timeout, T, Msg}`|`Action` return value|`state_timeout`|`Msg`|A specific timeout that can be set and received internally when the state machine has not transitioned to a new different state in T milliseconds
|`{next_event, internal, Msg}`|`Action` return value|`internal`|`Msg`|Internal messages that can be generated by a state machine wanting to trigger itself without looking like external calls

## Interpreting erl_crash dump
_Reference: http://erlang.org/doc/apps/erts/crash_dump.html_

## Docker erlang stuff

### run erlang using docker container
```sh
docker run -it --rm --name erlang-inst1 -v "$PWD":/usr/src/myapp -w /usr/src/myapp erlang:23-alpine erl
```
