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
    * syntax: (defn function_name [parameter] (body))
    * (defn greet [name] (string "Hello," name))
  * Multi-arity functions (like construtor in JAVA)
    * use () to include every 
  * Variadic functions
    * eg. (defn hello [greeting & who] (println greeting who))
    * if there are more than two parameters given, remaining args will pass to last parameter and forms a list
  * Anonymous Functions
    * fn: cannot be reused; usually passed to other function
    * syntax: (fn [parameter] (body))
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
* Excercise
  * (identity 2) : ((fn [x] x) 2)
  * (defn always-thing [& args] 100): always return 11

### Sequential Collections
* Vectors
  * indexed
    * eg. (get ["abc" false 99] 0) -> "abc"; (get ["abc" false 99] 1) -> false
  * count
    * eg. (count [1 2 3]) -> 3
  * constructing
    * eg. (vector 1 2 3) -> [1 2 3]
  * adding elements
    * eg. (conj [1 2 3] 4 5 6) -> [1 2 3 4 5 6]
  * Immutability
    * (def v [1 2 3])
    * (conj v 4 5 6) -> [1 2 3 4 5 6]
    * v -> [1 2 3]
* List
  * construct
    * (def card '(10 :ace :Jack 9))
  * List are not indexed; must use "first" and "rest" to get access to items
  * adding elemetns
    * items are added at the front
    * eg. (conj cards :queen) -> (:queen 10 :ace :jack 9)
  * Stack acess
    * can be used as stack with peak and pop
    * (def stack '(:a :b))
    * (peek stack) -> :a
    * (pop stack) -> (:b)


### Hashed Collections
* Sets
  * syntax: (def players #{"a" "b"})
  * add to set
    * conj
  * remove from set
    * disj
  * check for containment
    * {contains? players "d"}
  * (conj (sorted-set) "d" "c" "b" "a") -> #{"a" "b" "c" "d"}
    * A custom comparator can also be used with sorted-set-by 
  * into: putting one collection into another
    * (def new-players ["d" "e"])
    * (into players new-players) -> #{"a" "b" "d" "e"}
    * return the same type as its first arugment
* Maps
  * syntax: (def scores {"Fred" 1400, "Bob" 1240, "Angela" 1024}) // comma is optional since clojure regards it as whitespace
  * add new key-value pairs
    * (assoc scores "Sally" 0)
  * remove key-value pairs
    * (dissoc scores "Bob")
  * lookup by key
    * (get scores "Fred")
  * loolup with default
    * (get scores "Fred" 0): return default if key not found
  * Check containment
    * (contains? scores "Fred")
    * (find scores "Fred")
  * Checking keys/values
    * (keys scores)
    * (vals scores)
  * Build a map
    * (def players #{"Alice" "Bob" "Kelly"})
    * (zipmap players (repeat 0))
  * Combine maps
    * (merge-with + scores {"Fred" 1000})
  * Sorted map
    * (sorted-map "Bravo" 204 "Alfa" 35 "Sigma" 99 "Charlie" 100): sorted by key
* Representing application domain information
  * Field accessor
    * (get person :occupation) == (person :occupation) == (:occupation person)
    * default value: (:age person 18)
  * Update field
    * accos
  * Remove filed
    * dissoc
  * Nested entity
    * (def company {:name WidgetGo :address {:street "St" :city "ct"}})
    * (get-in company [:address :city])
  * Records (like constructor)
    * defined with the list of field names for record instances
    * (defrecord Person [first-name last-name age occupation])
    * (def kelly (->Person "Kelly" "Keen" 32 "Programmer"))
  
  
### [Flow Control](https://clojure.org/guides/learn/flow)
* Flow Control Expressions
  * If
    * (str "2 is " (if (even? 2) "even" "odd"))
  * Truth
    * only false and nil are regarded as false
    * (if false :truthy :falthy) -> :falthy
  * if and do
    * (if (even? 5) (do (println "even") true) (do (println "odd") false))
  * when
    * (when (neg? x) (throw (RuntimeException. (str "x must be positive: " x))))
  * cond
    * each test is evaluated in order; return the first true test
    * (let [x 5] (cond (< x 2) "x is less than 2" (< x 10) "x is less than 10"))
  * cond and else
    * if no test is true, return nil
    * (cond (< x 2) "x is less than 2" (< x 10) "x is less than 10" :else "x is greater than 10")
  * case
    * done in constant time
    * will throw an exception if no value match
    * (def foo [x] (case x 5 "x is 5" 10 "x is 10"))
    * (def foo [x] (case x 5 "x is 5" 10 "x is 10" "x isn't 5 or 10"))
* Iteration for side effects
  * dotimes
    * evaluate expression n times; return nil
    * (dotimes [i 3] (println i))
  * doseq
    * iterate over a sequence
    * (doseq [n (range 3)] (println n))
  * doseq with multiple bindings (like foreach)
    * process all permutations
    * (doseq [letter [:a :b] number (range 3)] (println [letter number])
  * for
  * list comprehension
  * (for [letter [:a :b] number (range 3)] [letter number])

### Namespaces
