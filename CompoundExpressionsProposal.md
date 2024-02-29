# Compound expressions 

## Abstract

Upon thorough investigation of community discussions, tickets, and 
analogous constructs in other programming languages, it has been 
determined that many of the requested features are already present in 
Kotlin, albeit in different forms. Therefore, this proposal 
concentrates on introducing compound expressions to `if` and `while` 
statements, as these areas appear to be the most beneficial and 
promising for the application of compound expressions in Kotlin.

## Table of contents


- [Abstract](#abstract)


- [Table of contents](#table-of-contents) 


- [Adding compound expressions in `while` proposal](#adding-compound-expressions-in-while-proposal)

    - [Motivation of adding compound expressions in `while`](#motivation-of-adding-compound-expressions-in-while)

        - [Benefits of adding "classic" `for`](#benefits-of-adding-classic-for)

        - [Proposed syntax of "classic" `for`](#proposed-syntax-of-classic-for)

        - [Potential uses of "classic" `for`](#potential-uses-of-classic-for)

        - [Drawbacks of adding "classic" `for`](#drawbacks-of-adding-classic-for)

    - [Proposed syntax of compound expressions in `while`](#proposed-syntax-of-compound-expressions-in-while)

    - [Potential uses of compound expressions in `while`](#potential-uses-of-compound-expressions-in-while)

    - [Benefits of adding compound expressions in `while`](#benefits-of-adding-compound-expressions-in-while)

    - [List of discussions related to compound expressions in `while`](#list-of-discussions-related-to-compound-expressions-in-while)


- [Adding compound expressions in `if` proposal](#adding-compound-expressions-in-if-proposal)

    - [Motivation of adding compound expressions in `if`](#motivation-of-adding-compound-expressions-in-if)

    - [Proposed syntax of compound expressions in `if`](#proposed-syntax-of-compound-expressions-in-if)

    - [Potential uses of compound expressions in `if`](#potential-uses-of-compound-expressions-in-if)

    - [Benefits of adding compound expressions in `if`](#benefits-of-adding-compound-expressions-in-if)

    - [List of discussions related to compound expressions in `if`](#list-of-discussions-related-to-compound-expressions-in-if)

## Adding compound expressions in `while` proposal

### Motivation of adding compound expressions in `while`

The Kotlin community has consistently shown an appetite `for` more 
versatile looping constructs, reminiscent of the "classic" `for` loop 
seen in other programming languages. This interest is evident from 
numerous discussions and custom implementations shared across Kotlin 
forums, such as this detailed example shared on
[Kotlin Discussions](https://discuss.kotlinlang.org/t/any-reason-to-not-keep-the-good-old-for-loop-format/25287/20)

```kotlin
fun main() {
    For(1, { it < 10 }, { it + 1 }) { i ->
        print(i)
    }
    println()
    For(0, { it < 10 }, { it + 2 }) { i ->
        print(i)
    }
    println()
    val array = charArrayOf('o', 'n', '\n', 'o', 'l', 'l', 'e', 'h')
    For(array.size - 1, { it >= 0 }, { it - 1 }) { i ->
        print(array[i])
        // It's meant to read like English
        if (array[i] == '\n') return@For andBreak() 
        // Sadly break alone can't be supported unless you use exceptions
        // Which aren't the best for performance. You'll find an implementation
        // that uses exceptions at the end of this post.
    }
    // However, continue is just return@For, and you can name nested For blocks like so:
    For('a', { it < 'z' }, { it + 1 }) myLoop@{ c ->
        if (c == 's') return@myLoop // continue
        print(c)
    }
}

class BreakScope {
    var isBroken: Boolean = false
    	private set
    
    fun andBreak(): Unit { isBroken = true }
}

inline fun <T> For(init: T, condition: (T) -> Boolean, increment: (T) -> T, body: BreakScope.(T) -> Unit) {
    val scope = BreakScope()
    var counter = init
    while(condition(counter)) {
        scope.body(counter)
        if(scope.isBroken) break
        counter = increment(counter)
    }
}
```

or this one:

```kotlin
private object BreakThrowable: Throwable() {
    override fun fillInStackTrace(): Throwable = this // Good for performance
}
class BreakScope {
    var isBroken: Boolean = false
    	private set
    
    fun Break(): Nothing { 
        isBroken = true 
        throw BreakThrowable
    }
}

inline fun <T> For(init: T, condition: (T) -> Boolean, increment: (T) -> T, body: BreakScope.(T) -> Unit) {
    val scope = BreakScope()
    var counter = init
    while(condition(counter)) {
        try {
        	scope.body(counter)
        } catch(e: BreakThrowable) {
            if(scope.isBroken) // This is to support nested Fors, only the For that got cancelled will actually break
                break
            else
                throw e
        }
        counter = increment(counter)
    }
}

fun main() {
    For(0, { it < 15 }, { it + 1 }) outer@{ i ->
        For(1, { it < 256 }, { it * 2 }) inner@{ j -> 
            println("$i, $j")
            if((i + j) % 2 == 0) this@inner.Break() // should print only i+1 when i is odd and then increment i, when i is even, it should print j=1 and j=2
            if(i * j == 12) this@outer.Break() // should break at i=12 and j=1 since that's the first i+j that is odd which happen to multiply to 12
        }
    }
}
```

### Benefits of adding "classic" `for`

There are several benefits to adding this feature:

1. **Increased Flexibility:** Allows for more complex iteration 
patterns without the need for additional control flow statements.

2. **Code Conciseness:** Reduces the need for external initialization 
and update statements, encapsulating all loop-related logic within the 
for statement.

3. **Familiar Syntax:** Leverages a loop syntax familiar to many developers, making
Kotlin more accessible to newcomers from other languages.

### Proposed syntax of "classic" `for` 

```kotlin
for (val i = 0; i < numIterations; i++) {
    // loop-body
}
```

### Potential uses of "classic" `for`

1. Сhanging iteration boundaries while traversing a loop 

    [Kotlin Discussions](https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57)
    ```kotlin
    for (val i = 0; i < numIterations; i++) {

        System.out.print(text.charAt(i));

        if (someCondition()) {
            numIterations–-;
        }

    }
    ```

2. Dynamically changing the step while iterating through a loop

    [Kotlin Discussions](https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429)
    ```kotlin
    for(var i = 0; i < 500; i+= (if (i < 40) 10 else 20)) {
        println("Now at $i")
    }
    ```

### Drawbacks of adding "classic" `for`

But as we can see the potential use of this feature looks a bit strange. 
Also, when it comes to adding classical `for` in Kotlin people specify as 
potential uses some of the features associated with classical `for` from C, which are 
also present in Kotlin, but require the use of specific syntax. 
Among them:

1. reverse loop:

    example from C
    ```C
    for (int i = array.length - 1; i >= 0; --i) {
        int element = array[i]
        //...
    }
    ```

    But we can do the same in Kotlin:

    ```kotlin
    for (i in array.length - 1 downTo 0) {
        var element = array[i]
        //...
    }
    ```

2. The iteration with a step different from 1:

    example from C:

    ```C
    for (int i = 0; i < array.length; i += 2) {
        val element = array[i]
        //...
    }
    ```

    But we can do the same in Kotlin:

    ```kotlin
    for (i in array.indices step 2) {
        val element = array[i]
        //...
    }
    ```

There are also people in the kotlin community who are against adding such a loop
[KT-1447](https://youtrack.jetbrains.com/issue/KT-1447/Please-add-support-for-traditional-fori10-i32-i-32-loops).
Also if you look at the specification of kotlin you may notice that the `for` loop 
is essentially syntactic sugar and was not designed as what is proposed above 
[Kotlin Specifaction](https://kotlinlang.org/spec/statements.html#loop-statements). That's why we 
decided that it's better to add the possibility of declaring local variables in the
`while` loop, because the `for` loop is intended only for iteration, and for 
everything else there is a `while` loop and all the examples above can be easily 
rewritten with the help of the `while` loop. 

### Proposed syntax of compound expressions in `while`
```kotlin
while (val var1 = <expression1> ,val var2 = <expression2>, val varN = <expressionN>, var1 != null, var2 != null, varN != null) {
  
}
```

### Potential uses of compound expressions in `while`

1. All potential uses of the classic `for`

2. Streaming Data Processing

In cases where the data comes from a stream (such as a file stream or 
network connection) and you want to continue processing while the 
stream is open and accessible. ([Kotlin Discussions]) (https://discuss.
kotlinlang.org/t/why-i-cant-apply-value-inside-while-loop/7762)

```kotlin
val buffer = ByteArray(8192)
val bytesRead : Int
val byteArrayOutputStream = ByteArrayOutputStream()
val inputStream = FileInputStream(file)
while((val byteRead = inputStream.read(buffer)) != -1){

}
```

3. Paged data loading.

If you load data page by page (for example, from an API), where each 
request returns data for the next page as long as the data is 
available.

```kotlin
var page = 1
while (val data = api.loadData(page)) {
    process(data)
    page++
}
``` 

### Benefits of adding compound expressions in `while`

1. **Enhanced Flexibility and Control:** Facilitates complex iteration 
patterns, emulating "classic" `for` loop functionalities within the 
while loop's more versatile framework.

2. **Code Conciseness and Clarity:** Reduces boilerplate by allowing 
direct variable declaration and initialization in the loop condition, 
improving readability.

3. **Safety and Predictability:** Aligns with Kotlin's null safety and 
immutability principles by ensuring variables declared within the loop 
are locally scoped and not subject to unintended modifications.

### List of discussions related to compound expressions in `while`

* [Kotlin Discussions - Any reason to not keep the good old for loop format?](https://discuss.kotlinlang.org/t/any-reason-to-not-keep-the-good-old-for-loop-format/25287/20)

* [Kotlin Discussions - `for` loop with dynamic condition](https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57)

* [Kotlin Discussions - For-loop dynamic step](https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429)

* [KT-1447](https://youtrack.jetbrains.com/issue/KT-1447/Please-add-support-for-traditional-fori10-i32-i-32-loops)

* [Kotlin Discussions - Why I can't apply value inside while loop?](https://discuss.kotlinlang.org/t/why-i-cant-apply-value-inside-while-loop/7762) 

## Adding compound expressions in `if` proposal

### Motivation of adding compound expressions in `if`

Kotlin prides itself on null safety, but the current mechanisms for 
dealing with multiple nullable variables can sometimes lead to less 
clean code and an increase in boilerplate. For instance, when calling 
a function only if certain parameters are not null, developers might 
resort to nested let blocks:

```kotlin
val result = a?.let { aNotNull ->
    c?.let { cNotNull ->
        someFunction(aNotNull, b, cNotNull)
    }
}
```

([Kotlin Discussions](https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838
))

This approach, while functional, introduces additional complexity and verbosity, especially as the number of parameters increases.

#### Current Solutions and Their Limitations

1. Using `let` with `Pair` Container ([Kotlin Discussions](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/2))

    Using `Pair` combined with the `let` extension function to handle 
    two null parameters simultaneously.

    ```kotlin
    fun main(args: Array<String>) {    
        val name: String? = "john"
        val age: Int? = 99
        Pair(name, age).let {
            println("name: $name, age: $age")
        }
    }
    
    fun Pair<String?, Int?>.let(action: (pair: Pair<String?, Int?>) -> Unit) {
        if (this.first != null && this.second != null)
            action(this)
    }
    ```

    While using Pair with let can handle two nullable parameters, it 
    becomes less flexible and more complex with more than two 
    parameters.

    

2. Using of generic functions ([Kotlin Discussions](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/4))

    Creating a generic `ifNotNull` function that executes code only if 
    all parameters are non-null.

    ```kotlin
    inline fun <A, B, R> ifNotNull(a: A?, b: B?, code: (A, B) -> R) {
        if (a != null && b != null) {
            code(a, b)
        }
    }

    fun test() {
        ifNotNull(name, age) { name, age ->
          doSth(name, age)
        }
    }
    ```

    Using of a generic function reduces some boilerplate but 
    requires overloading the function for different numbers of 
    arguments, adding to the codebase's complexity.

3. Using of extension functions ([Kotlin Discussions](https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838/2))

    Using the `callIfNotNull` function as an extension on function 
    references to call only if all parameters are non-null.

    ```kotlin
        inline fun <T1, T2, T3, R> KFunction3<T1, T2, T3, R>.callIfNotNull(a: T1?, b: T2?, c: T3?): R? {
            a ?: return null
            b ?: return null
            c ?: return null

        return this(a, b, c)
    }

    ::someFunction.callIfNotNull(a, b, c)
    ```

    This method simplifies calling functions with nullable parameters but necessitates a separate function definition for each variable count, which is not ideal for code maintenance and readability.

In light of these challenges, we propose the introduction of a syntax 
that allows for the declaration of local variables within `if` 
conditions. 
This approach not only mirrors Kotlin's commitment to null 
safety and concise code but also addresses the mutable state 
issue—ensuring variables within the `if` scope remain unchanged 
throughout their lifecycle. 
For instance, Kotlin's current `?.let {}` 
syntax for handling a single nullable variable translates to a pattern 
where the variable is safely checked for nullity before proceeding:

```kotlin
fun test() {
    name?.let { doSomething(it) }
}

```
compiles to the equivalent java code:

```java 
public final void test() {
    String var10000 = this.name;
    if(this.name != null) {
        String var1 = var10000;
        this.doSomething(var1);
    }
}
```

Swift has a similar problem with null checking multiple vars and solves this by making it easy 
to declare local values within if statements:

```swift
// Swift code 
if let name = name, let age = age {
    doSth(name, age)
}
```

So a similar syntax in Koltin could be the following:

### Proposed syntax of compound expressions in `if`

```kotlin
if (val var1 = <expression1> ,val var2 = <expression2>, val varN = <expressionN>, var1 != null, var2 != null, varN != null) {
}

```
This syntax proposes a straightforward method for declaring and 
checking multiple variables within a single if condition, aiming to 
reduce verbosity and enhance code readability. 
But there are also other suggestions for adding similar functionality, such as:
1. **Extended Safe Call Operator `(?.)`**

    **Description:** 
    Enhance the safe call operator to allow conditional function execution 
    based on the nullability of arguments, simplifying null checks within 
    function calls.

    **Example:**
    ```kotlin
    val result = someFunction(a?, b, c?)
    ```

    **Drawback:** Introduces syntax complexity and potential for    
    oversight, complicating the readability.

2. **Shortcut for Local Variable Declarations `(@localVal)`**
    
    **Description:**
    A shortcut for declaring and checking nullability of local      
    variables within conditions, aiming to reduce boilerplate code.

    **Example:**
    ```kotlin
    if (@localVal name != null && @localVal age != null) { ... }
    ```

    **Drawbacks:** Adds ambiguity and complexity to the language's 
    syntax, potentially hindering readability.

Taking into account everything described above, it was decided that the best option is the option described at the very beginning of this part, namely:
```kotlin
if (val var1 = <expression1> ,val var2 = <expression2>, val varN = <expressionN>, var1 != null, var2 !=null, varN != null) {
}

```
### Potential uses of compound expressions in `if`

1. **Direct Smart Casts for Nullable Types** ([Kotlin Discussions](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/22))

Consider a scenario where you need to determine which of two 
individuals is older, and both are represented by nullable `Person` 
objects. The enhanced `if` syntax facilitates direct checks and smart 
casts, allowing for seamless access to properties like `age` without 
additional null checks:

```kotlin
fun whoIsOldest(person1: Person?, person2: Person?) {
    if (val p1 = person1, val p2 = person2, val age1 = p1.age, age2 = p2.age) {
        when {
            age1 > age2 -> print("$p1 is oldest")
            age1 < age2 -> print("$p2 is oldest")
            else -> print("$p1 and $p1 are the same age")
        }
    } else {
        print("Your need two people to compare ages")
    }
}
```

The benefit however is that is that you can use earlier values in later 
expressions. In the example above p1 and p2 have already been null checked so we 
can access their age property directly.
And because the expressions can be anything that returns a nullable type it can 
also be used with `safe-casts`:

```kotlin
if (val child = person as? Child, val car = child.favouriteToy as? Car) {
    car.race()
    print("$child is racing their toy $car")
}
```

A additional improvement that could be made which is also available in swift is 
allowing boolean expressions alongside the nullable expressions. It’s a fairly 
common use case to check if something is non-null and then perform an additional 
check to see if it is appropriate to use.

```kotlin
if (val childAge = person.child?.age, childAge >= 6 && childAge < 18) {
    print("$person has to drop their child at school each weekday")
}
```

### Benefits of adding compound expressions in `if`

1. **Enhanced Code Clarity:** Directly declaring variables within `if` 
conditions leads to cleaner, more understandable code.

2. **Reduced Boilerplate:** Eliminates the need for nested `let` blocks or 
separate variable checks, streamlining null handling.

3. **Improved Safety and Consistency:** Localizing variable declarations 
within `if` conditions ensures immutability and reduces the risk of 
unintended side effects, aligning with Kotlin's emphasis on safety and 
predictability.


### List of discussions related to compound expressions in `if` 
* [Kotlin Discussions - Feature Request: Null Check for Arguments in Function Invoke](https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838)

* [Kotlin Discussions - Kotlin null check for multiple nullable var’s](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946)

* [StackOverflow - Kotlin call function only if all arguments are not null](https://stackoverflow.com/questions/50742094/kotlin-call-function-only-if-all-arguments-are-not-null)