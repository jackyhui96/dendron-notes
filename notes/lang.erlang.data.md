---
id: fbc7b495-4e18-4547-a795-9afa2805635a
title: Data
desc: ''
updated: 1609935021488
created: 1609934378913
---

# Data Types

|Name|Description|Dialyzer|Example Syntax|
|-- | -- | -- | -- |-- |
|integer|number without decimals|`integer(), pos_integer(), non_neg_integer()`|`1, 2, 3, -213, 16#01FF, 2#101011`|
|float|number with decimals|`float()`|`1.0, -1.0, 123.12, 1.0e232`|
|number|either floats or integers|`number()`|`1.0, 1`|
|atom|literals, constants with their own name for value|`atom()`|`abc, 'abc', some_atom@erlang, 'atom with spaces'`|
|boolean|atoms true or false|`boolean()`|`true, false`|
|reference|unique opaque value|`reference()`|`make_ref()`|
|fun|anonymous function|`fun(), fun((ArgType) -> RetType)`|<code>fun(X) -> X end, fun F(0) -> []; F(N) -> [1 &#124; F(N-1)] end</code>|
|port|opaque type for a file descriptor|`port()`|`N/A`|
|pid|process identifier|`pid()`|`<0.213.0>`|
|tuple|group a known set of elements|`tuple(), {A, B, C}`|`{celcius, 42}, {a, b, c}, {ok, {X, Y}}`|
|map|a dictionary of terms|`map(), #{KType => VType}, #{specific_key := VType}`|`#{a => b, c => d}, Existing#{key := Updated}`|
|nil|an empty list|`[]`|`[]`|
|list|recursive structure for a list of terms|`list(), [Type]`|<code>[a, b, c], [a &#124; [b &#124; [c &#124; []]]], "a string is a list"</code>|
|binary|a flat byte sequence|`binary()`|`<<1,2,3,4>>, <<"a string can be a binary">>, <<X:Size/type, _Rest/binary>>`|
Term ordering: `number < atom < reference < fun < port < pid < tuple < map < nil < list < binary`
