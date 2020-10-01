# Combinatorics.jl

## About

This is (hopefully, eventually, some day) going to be a combinatorics package for [Julia](https://julialang.org)/[OSCAR](https://oscar.computeralgebra.de). The goal is to provide very efficient algorithms in combinatorics, especially for things relevant in representation theory. 

Why would anyone want to do this, especially when there is so much combinatorics already in other computer algebra systems? Well, on the one hand, it's a great way to learn about algorithms, so why not? On the more serious side, have a look at the following examples creating the list (not an iterator) of all partitions of the integer 90 (there are ~56.6 million) in different systems.

In **Sage** (v9.1):

```
sage: time X=Partitions(90).list()
Wall time: 3min 5s #Uses 26.665GiB mem, quitting Sage takes quite a bit of time
```

In **Magma** (v2.25-5):

```
> time X:=Partitions(90);
Time: 32.990 //Uses 15.688GiB mem, Magma UNUSABLE from now on!!
```
In **Julia** (v1.5.2, my implementation):

```
julia> @time partitions(90);
5.447290 seconds (56.63 M allocations: 6.239 GiB, 46.77% gc time) #No problem afterwards
```

In the last one I'm cheating a bit because I'm using 8-bit integers (thus saving memory). But even when using big integers, the Julia implementation is much more efficient:

```
julia> @time partitions(90); #this time with big integers (fmpz)
23.333262 seconds (156.37 M allocations: 15.056 GiB, 47.95% gc time)
```

And having the possibility to also work with special integer types is very useful sometimes. Of course, you can do the same in C. But Julia is a high-level language with a similar simple syntax like Python, so why would anyone still go through such a pain?

## Using

To install the package, do the following In Julia:

```
using Pkg
Pkg.add(url="https://github.com/ulthiel/Combinatorics.jl")
```

Then you can start using the package as follows:

```
using Combinatorics
partitions(10)
```

You can get a list of exported functions using

```
names(Combinatorics)
```

You can get help for a function by putting a question mark in front, e.g.

```
?partitions
```

## Developing

### Setting up the repository

Clone this repository to somewhere on your computer:

```
git clone https://github.com/ulthiel/Combinatorics.jl
```

Enter the directory "Combinatorics.jl", start Julia, hit the "]" key to enter REPL mode, and then add the package to the registry:

```
dev .
```

Exit the REPL mode by hitting the backspace key. Then you can start using the package as usual with

```
using Combinatorics
```

Any changes you make to the code now is not yet available in Julia, you have to restart it—this is simply the way Julia works. This can be annoying when developing. A solution is to load the [Revise](https://timholy.github.io/Revise.jl/v0.6/) package before loading the package.

```
using Pkg
Pkg.add("Revise")
using Revise
using Combinatorics
```

Now, changes you make in the code are immediately active in the Julia session (except for changes to structures, here you need to restart).