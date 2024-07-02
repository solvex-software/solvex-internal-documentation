`Prefer`:
``

1. Named functions should be used in composition style code, while operators in application style code (do notation/IO).
1. Every operator should be defined in terms of it's named counterpart.
1. always hide the value constructor and getters of new types. use to/from instead
1. name things based on what they require, not what they lack. ex: maximumNonEmpty better than maximumUmbounded
1. modules should contain only things specific to them. ie: foldlazy is specific to catamorphic but foldMonoid is specific to monoids and foldToMonoidSurjective is specific to surjective
1. Never comment code except when the code is written in an unorthodox way for a good reason (ex: It is written in a way that is more efficient than normal due to requirements)
2. Show typeclass should only be used for debugging. Do not use it for displaying things to users, even with a TUI. Doing so is coupling debugging desires with ui desires
1. avoid fractionals that aren't rational
1. No magic numbers except where anonymous functions makes just as much sense
1. Code should be written in the most elegant way possible; it is the job of the compiler to deal with performance
   - Only optimize/go lower level if after profiling/benchmarking your code isn't as efficient as it should be.
1. Helper functions should be created when possible and, if general enough, added to a library
   - Don't use `x mod 2 == 0` but rather turn it into a function `isEven` and add to a library to use from then on in. Even better make `isDivisbleBy` and then define `isEven` as a special case of that.
1. Predicates should always be named `isProperty`
1. Lists/groupings of things should always be named forcibly with an s
   - if you have a group of `fish` then it should be called `fishes`; group of `sheep` is `sheeps`
1. Abide by vscode settings
1. Instead of using `Maybe` to turn partial functions into total functions, use the right resolution type
   - Instead of `Integer` that uses a `Maybe` to handle all negative numbers, use `NonNegativeInteger` instead
1. Prefer `where` to `let`
1. Prefer general to specific
   - Instead of `map` use `fmap`
   - Instead of `
1. Prefer pointfree code
1. Prefer `case` to pattern matching
1. Prefer case matching to guards
1. Prefer guards to if-this-then-else
1. Prefer ADTs to Data Structures in backend code
   - Instead of using arrays, use `Stack`, `List` (real list), etc...
   - Avoid reliance on lists in general
1. Pick the proper ADT container using three questions: Duplicates allowed? Order matters? Special access rules?
   - Make sure when using list comprehensions you don't actually want set builder notation. If you do then make sure to compose it with a `toSet` function.
   - This can be used for everything, use `toBag`, `toSortedList`, etc...after every list comprehension to establish what it is you actually want.
1. Unordered ADTs should be randomized first to avoid client reliance on implementation details
1. Always use Domain Types over ADTs in client code
   - Instead of `area :: Int -> Int -> Int`, write `area :: Width -> Height -> Area`
1. Use the highest level of iteration available
   - Don't use explicit iteration when you can use internal
1. Have definition bodies semantically match type signature
   - area :: Int -> (Int -> Int)
   - area x = \y -> x + y
   - area :: Int -> Int -> Int
   - area x y = x + y
1. Keep lists infinite/as general as possible
   - If you wanted to generate the first five prime numbers, do `take 5 primes`
   - If you have a list with a billion numbers that you want to multiply by 10 but then return the first 5 of them, in eager languages you have make sure to first take the first 5 numbers and then multiply them by 10 so you don't multiply a billion numbers by 10 for no reason. However in a lazy language like Haskell, you can do them in any order. ie: `(map (*10) . take 5) [1..1000000000]` or `(take 5 . map (*10)) [1..1000000000]`
1. Stay semantically meaningful/declarative over imperative/incidental
   - `[x | x <- [1..], odd x]` over `[x | x <- [1, 3..]]`
1. Prefer laziness to eagerness
1. Whenever you are folding, try to fold over a semiring, monoid (0+) or semigroup (1+) if possible.
1. never pattern match over bool, instead use guards
1. Never use if-this-then-else. instead use guards.
1. Don't use don't care patterns if you can help it because you want to maintain exhaustiveness.
1. Never use tuple or either, use ADT instead. 
1. always use records for product types 
1. Never use type synonyms
1. always use records even for a single field (extension to auto create)
1. Good rule of thumb is that Maybe should only be used because the result type not because of an input type 
1. use the highest level of abstraction you can get away with
1. Always prove laws of instances with property-based testing
1. create monoids too even if greater abstractions exist???
1. Stick to always using curried functions
1. Always try to pass the "smaller" of something before the "larger" to take advantage of laziness
    - If you have two maybes you want to check using an alternative, always have the first one be a quicker evaluation
    - If you have an "OR" or "AND" between two expressions, always have the quicker to evaluate expression on the left hand side.
1. Keep typeclasses limited to only what needs to be overriden by each instance
2. Each module should only contain one adt or typeclass
3. Use a re-exporting scheme in the library???
4. Consistent naming scheme
    - an unordered list is called a bag or a multiset but use "UnorderedList" instead.
    - the "default" case should have the regular name ie: "a "List" is an ordered list but just leave its name, a Set is an unordered set, etc..."
1. typeclass methods are not an API, they are the bare minimum requirements for a type to be able to join that Typeclass (along with laws). thus, some typeclass methods are not meant for normal programming usage like `compare` in Ord or to/from Generics.
1. if importing a library that isn't ours, use namespacing
1. binary operators should always be infix? if so then always define associativity and precedence
1. every associative binary function should be defined in terms of a group and then a named fold made for it (ex: Min semigroup defines min function which defines minimum function)
1. name Typeclasses in a way that makes sense to the context. functor is a noun because it's referring to a type function...Option is itself a functor. most things should be adjectives though and relate to fundamental properties or mathematical abstractions
1. use left/right associative function depending on if you need that associativity, otherwise default. use lazy if you can make use of short circuiting and any potential space leaks is worth it. use strict if you don't want space leaks or have to traverse the entire thing or require both values to be evaluated fully. otherwise use strict 
## Naming
1. Spell out acronyms?
1. Data types should be named in order of most specific to least
    - SortedList
    - BinaryTree
    - HashMap
1. Functions should be named in order of least specific to most
   - foldLazyRight
   - mapParallel
1. Camelcase is always used for functions and pascal case for types/constructors
1. due to the expression problem and cyclic module dependencies, put all instances in the type class modules
1. functions should be verbs 
1. constants should be nouns
1. predicates should be `isAdjective` sometimes with an At or Of etc at the end
