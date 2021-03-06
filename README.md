# pipe-transform

## Usage

Pipe transform uses syntax of list comprehension:

```erlang
[pipe||Arg, ...]
```

Arg (first element) is passed as is, the rest are transformed into function calls.

Arg and every call result become first argument of the next call:

```[pipe||x, fn(y)]        => fn(x, y)```
```[pipe||x, fn(y), fn(z)] => fn(fn(x, y), z)```

Functions are called from left to right

## Supported calls

* `f` - local function
* `m:f` - external function

## Example

```erlang
-module(foo).
-compile({parse_transform, pipe_transform}).

-export([f/0]).

f()  -> [pipe||1, inc, mul(2)].

inc(X) -> X + 1.

mul(X, K) -> X * K.
```
