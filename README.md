# [Clojure](https://clojure.org/)


## [Learn Clojure](https://clojure.org/guides/learn/clojure)

### [Syntax](https://clojure.org/guides/learn/syntax)
* Literals
  * Numeric types
  * Character types
  * Symbols and idents
  * Literal collections
* Evaluation
  * Structure and Semantics: prefix expression
    * eg. (+ 1 2) -> 3
  * Delaying evaluation with quoting
    * '(+ 1 2) -> (+ 1 2)
* REPL
  * \*1 for last result
  * doc: used to check documentation (like man in shell script)
  * apropos
  * find-doc
  * dir: see full functions under particular namespace
  * source: documentation + source file
* Clojure Basics
  * def: define a variable
    * eg. (def x 7) 
  * println/print vs prn/pr


### [Functions](https://clojure.org/guides/learn/functions)
* Creating Functions
  * defn: define a function
    * structure: (defn function_name [parameter] (body))
    * (defn greet [name] (string "Hello," name))
  * Multi-arity functions (like construtor in JAVA)
    * use () to include every 
  * Variadic functions
    * eg. (defn hello [greeting & who] (println greeting who))
    * if there are more than two parameters given, remaining args will pass to last parameter and forms a list
  * Anonymous Functions
    * fn: cannot be reused; usually passed to other function
    * structure: (fn [parameter] (body))
  * Anonymous function syntax
    * shorter structure for anonymous functions
    * eg. #(+ 1 %), #(+ %1 %2) : % for a parameter; %1 %2 ... for multiple parameters; %& for remaining parameters
  * Element to Vector
    * (fn [x] ([x]))
    * #(vector %)
* Applying Functions
  * apply
    * (apply f '(1 2 3)) or (apply f 1 2 '(3)); the final argument must be a sequence
    * eg. (defn plot [shape coords] (apply plotxy shape coords))
* Local and Closures
  * let (local scope)
    * syntax: (let [name value] (code that uses name))
    * eg. (let [x 1 y 2] (+ x y))
  * Closures (fn)
    * can capture values beyond the lexical scope
* Java Interop
  * Invoking Java code
    * new Widget("foo") : (Widget. "foo")
    * rnd.nextInt() : (.nextInt rnd)
    * object.field : (.-field object)
    * Math.sqrt(25) : (Math/sqrt 25)
    * Math.PI : Math/PI
  * Java Methos vs Functions
    * Java methods are not Clojure functions
    * cannot store them or pass them as arguements
    * can wrap them in functions when necessary


### Sequential Collections

### Hashed Collections

### Flow Control

### Namespaces
