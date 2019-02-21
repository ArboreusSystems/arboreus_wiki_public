# AR|BO|RE|US Library module: a_benchmark

The module for making benchmarks of speed of execution of any functions written on Erlang. Module in [Github](https://github.com/ArboreusSystems/arboreus_library/blob/master/lib/universal_erl/src/a_benchmark.erl).

## Install and compile

Follow ["Install and compile"](https://github.com/ArboreusSystems/arboreus_wiki_public/blob/master/library/wiki_install_and_compile.md) article.

## Erlang module usage

* **a_benchmark:do(Module,Function,Parameters,Iterations)** -> do the single function benchmark of speed of execution
* **a_benchmark:set(Module,Function,Parameters,Iterations)** -> do the set of functions and compare all of results by speed of execution
