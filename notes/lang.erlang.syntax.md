---
id: 14c34d7c-644d-4cb8-9df3-d94cefa8fa74
title: Syntax
desc: ''
updated: 1611141607481
created: 1609935081566
---

# Syntax

## Modules
```erlang
%%% This is a module-level comment
%%% @doc This tag includes officiel EDoc documentation.
%%% It can be useful for people to consule
%%% @end
%%% Generate documentation with rebar3 edoc

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% Let's start with Module Attributes %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%% This is an attribute or function-specific comment
%% attributes start with a `-', functions with letters.
%% This file should be saved as `sample.erl'
-module(sample).

%% Functions are described in the form Name/Arity, and must
%% be exported through an `-export([...]).' module attribute
-export([f/0, f/1]).
-export([x/0]).         % multiple export attributes can exist

%% You can "import" functions from another module, but
%% for clarity's sake (and because there's no namespaces)
%% nobody really does that
-import(module, [y/0]).

%% .hrl files contain headers, and are imported directly
%% within the module.
%% The following includes a private header file from src/
%% or a public header file from include/ in the current app
-include("some_file.hrl").
%% The following includes a public header file from the
%% include/ file of another application
-include_lib("appname/include/some_file.hrl").

%% specify an interface you implement:
-behaviour(gen_server).

%% Define a record (a tuple that compilers handles in a
%% special way)
-record(struct, {key = default :: term(),
		 other_key     :: undefined | integer()}).

%% Just C-style macros
-define(VALUE, 42).        % ?VALUE in this module becomes `42'
-define(SQUARE(X), (X*X)). % function macro
-define(DBG(Call),         % a fancy debug macro: ?DBG(2 + 2)
	io:format("DBG: ~s (~p): ~p~n",
		  [??Call, {?MODULE, ?LINE}, Call])).

%% Conditionals
-ifdef(MACRO_NAME).        % opposite: -ifndef(MACRO_NAME).
-define(OTHER_MACRO, ok).
-else.                     % other option: -elif(NAME).
-define(MACRO_NAME, ok).
-endif.

%% Type definitions
-type my_type() :: number() | boolean().
-type my_container(T) :: {[T], [T], my_type(), mod:type()}
-export_type([my_type/0, my_container/1]).

%% you can also define custom attributes:
-my_attribute(hello_there).
-author("Duke Erlington").

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%%% And now modules for code and functions %%%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

%% @doc A function with 0 arguments returning an atom
-spec f() -> term(). % optional spec
f() -> ok.

-spec f(number()) -> float().
f(N) -> N + 1.0.

%% Pattern matching with clauses
x([]) -> [];  % base recursive clause for a list
x([_H|T] -> [x | T]. % replace list element with `x' atom

%% @private variable binding rules
same_list(X = [_|_], X) -> true;
same_list([], []) -> true;
same_list(_, _) -> false.

%% Operators in the language
operators(X, Y) ->
    +X, -Y, % unary
    X + Y, X - Y, X * Y, X / Y,   % any numbers
    X div Y, X rem Y,             % integers-only
    X band Y, X bor Y, X bxor Y,  % binary operators
    X bsl Y, X bsr L,             % bit shifting
    not X,                        % boolean not
    X andalso Y, X orelse Y,      % shortcircuit boolean operators
    X < Y, X > Y, X >= Y, X =< Y, % comparison
    X == Y, X /= Y,               % equality (float == int)
    X =:= Y, X =/= Y,             % strict equality (float =/= int)
    X ++ Y, X -- Y,               % append Y to X, delete Y from X
    X ! Y.                        % send message Y to process X

%% Using guards. Valid guard expressions at:
%% erlang.org/doc/reference_manual/expressions.html#guard-sequences
comfortable({celsius, X}) when X >= 18, X =< 26 -> % AND clauses
    true;
comfortable({celsius, _}) ->
    false.

incomfortable({celsius, X}) when X =< 18; X >= 26 -> % OR clauses
    true;
incomfortable({celsius, _}) ->
    false.

%% difference with 'andalso' and 'orelse'
conds(X) when (is_number(X) orelse is_integer(X))
	       andalso X < 9 ->
    %% equivalent (A AND B) OR C
    true;
conds(X) when is_number(X); is_integer(X), X < 9 ->
    %% - parentheses impossible with , or ;
    %% - equivalent to A OR (B AND C)
    true;
conds(T) when element(1, T) == celsius; is_integer(T) ->
    %% element/2 extracts an element from a tuple. If `T' is
    %% not a tuple, the call fails and `is_integer/1' is tried
    %% instead
    true;
conds(T) when element(1, T) == celsius orelse is_integer(T) ->
    %% this can never work: if element/2 fails, the whole
    %% `orlese' expressoin fails and `is_integer/1' is skipped
    true.

%% Conditionals
conditional('if', Light) ->
    if Light == red -> stop;
       Light == green; Light == yellow -> go_fast;
       true -> burnout % else clause!
    end;
conditional('case', {Light, IsLate}) ->
    case Light of
	green -> go;
	yellow when IsLate -> go_fast;
	_ -> stop
    end;
conditional(pattern, green) -> go;
conditional(pattern, yellow) -> slow;
conditional(pattern, red) -> stop.

%% List and binary comprehensions
comp(ListA, ListB) ->
    [X*X || X <- ListA, X rem 2 == 0], % square even numbers
    [{X,Y} || X <- ListA, Y <- ListB], % all possible pairs
    << <<X:8>> || X <- ListA >>.       % turn list into bytes
comp(BinA, BinB) -> % now with binaries
    << <<X*X:32>> || <<X:8>> <= Bin, X rem 2 == 0 >>,
    [{X,Y} || <<X:32>> <= BinA, <<Y:8>> <= BinB],
    [X || <<X:8>> <= BinA].

%% Anonymous and higher order functions
higher_order() ->
    If = fun(Light) -> conditional('if', Light) end,
    Case = fun(Light) -> conditional('case', {Light, true}) end,
    lists:map(If, [green, yellow, red]),
    lists:map(Case, [green, yellow, red]),
    If(red), % can be called literally
    lists:map(fun(X) -> X*X end, [1,2,3,4,5]).

try_catch() ->
    try
	some_call(),     % exceptions in this call are caught as well
	{ok, val},       % common good return value to pattern match
	{error, reason}, % common bad return value to pattern match
	% any of these expression aborts the execution flow
	throw(reason1), % non-local returns, internal exceptions
	error(reason2), % unfixable error
	exit(reason3)   % the process should terminate
    of  % this section is optional: exceptions here are not caught
	{ok, V} ->
	    do_something(V),
	    try_catch(); % safely recurse without blowing stack
	{error, R} ->
	    {error, R} % just return
    catch % this section is optional: various patterns
	throw:reason1 -> handled;
	reason2 -> oops; % never matches, `throw' is implicit type
	error:reason2 -> handled;
	exit:reason3 -> handled;
	throw:_ -> wildcard_throws;
	E:R when is_error(E) -> any_error;
	_:_:S -> {stacktrace, S}; % extract stacktrace
    after -> % this is an optional 'finally' block
	finally
    end.
```

## Processes and Signal
```erlang
%% Start a new process
Pid = spawn(fun() -> some_loop(Arg) end)
Pid = spawn('name@remote.host', fun() -> some_loop(Arg) end)
Pid = spawn(some_module, some_loop, [Arg])
Pid = spawn('name@remote.host', some_module, some_loop, [Arg])
%% Spawn a linked process
Pid = spawn_link(...) % 1-4 arguments as with spawn/1-4
%% Spawn a monitored process atomically
{Pid, Ref} = spawn_monitor(fun() -> some_loop(Arg) end)
{Pid, Ref} = spawn_monitor(some_module, some_loop, [Arg])
%% Spawn with fancy options
spawn_opt(Fun, Opts)
spawn_opt(Node, Fun, Opts)
spawn_opt(Mod, Fun, Args, Opts)
spawn_opt(Node, Mod, Fun, Args, Opts)
%% Options must respect the following spec; many are advanced
[link | monitor |
 {priority, low | normal | high | max} |    % don't touch
 {fullsweep_after, integer() >= 0} |        % full GC
 {min_heap_size, Words :: integer() >= 0} | % perf tuning
 {min_bin_heap_size, Words} |
 {max_heap_size,                    % heap size after which
   Words |                          % the process may be killed. Use
   #{size => integer() >= 0,        % to indirectly set max queue sizes
     kill => boolean(),
     error_logger => boolean()}}

%% send an exit signal to a process
exit(Pid, Reason)

%% Receive a message
receive
    Pattern1 when OptionalGuard1 ->
	Expression1;
    Pattern2 when OptionalGuard2 ->
	Expression2
after Milliseconds -> % optional
    Expression
end

%% Naming processes
true = register(atom_name, Pid)
true = unregister(atom_name)
Pid | undefined = whereis(atom_name)

%% Monitor
Ref = erlang:monitor(process, Pid)
true = erlang:demonitor(Ref)
true | false = erlang:demonitor(Ref, [flush | info])

%% Links
link(Pid)
unlink(Pid)
process_info(trap_exit, true | false)
```

## Behaviours
