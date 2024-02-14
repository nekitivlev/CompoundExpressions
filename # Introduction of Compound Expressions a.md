# Introduction of Compound Expressions and Multilet in Kotlin
## Abstract 
This proposal introducing compound expressions and a `multilet` construct into Kotlin to enhance the language's expressivness and conciseness, particularli in handliing nullable variables, loops and conditional expressions.
## Table of Contents
- Abstract  
- Table of Contents
- Motivation 
- Proposal
    - Compound expressions
        - Bringing C-style loop in Kotlin
            - Proposed Syntax
            - Potential Uses 
            - Benefits   
            - Drawbacks
        - Bringing compound expressions in other control flow operators
            - Proposed Syntax
            - Potential Uses
            - Benefits 
    - Mutlilet
        - Proposed Syntax
        - Potential Uses 
        - Benefits 
## Motivation 
Kotlin developers frequently encounter scenarios requiring multiple null checks or the need to manage several variables simultaneously in loops or conditional expressions. The current syntax, while functional, can lead to nested blocks or repetitive code, affecting readability and maintainability. This proposal aims to address these issues by introducing compound expressions and the `multilet` feature, drawing inspiration from similar constructs in other programming languages.
## Proposal 
### Compound expressions
Allow expressions that enable operations on multiple variables within a single statement, enhancing the conciseness of loops and conditional blocks. 
#### Bringing C-style loop in Kotlin
Kotlin's current for loop syntax is elegant and sufficient for iterating over ranges or collections. However, it lacks the flexibility to define custom initialization, condition, and incrementation steps within the loop declaration. This limitation becomes apparent in scenarios requiring precise control over the iteration process, such as iterating over two variables simultaneously or implementing complex termination conditions. 
Nowadays, when people want to use a loop with functionality similar to c-style for, they use while or write their own for statement. 
Example of how people implement C for loop in Kotlin:
https://discuss.kotlinlang.org/t/any-reason-to-not-keep-the-good-old-for-loop-format/25287/20
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
#### Proposed syntax
```kotlin
for (val i = 0; i < numIterations; i++) {
    // loop-body
}
```
#### Potential uses
1. Сhanging iteration boundaries while traversing a loop 

    https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57
    ```kotlin
    for (val i = 0; i < numIterations; i++) {

        System.out.print(text.charAt(i));

        if (someCondition()) {
            numIterations–-;
        }

    }
    ```
2. Iterate over multiple variables

    https://discuss.kotlinlang.org/t/why-not-multi-for/2241
    ```kotlin
    for (var i in 1..10; var j in 1..10) {
        println("$i $j")
    }
    ```
3. Dynamically changing the step while iterating through a loop

    https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429
    ```kotlin
    for(var i = 0; i < 500; i+= (if (i < 40) 10 else 20)) {
        println("Now at $i")
    }
    ```

#### Benefits
1. **Increased Flexibility:** Allows for more complex iteration patterns without the need for additional control flow statements.
2. **Code Conciseness:** Reduces the need for external initialization and update statements, encapsulating all loop-related logic within the for statement.
3. **Familiar Syntax:** Leverages a loop syntax familiar to many developers, making Kotlin more accessible to newcomers from other languages.
#### Drawbacks
Despite everything said above, there are several problems:
1. Almost everything you need for can be written using while. (https://youtrack.jetbrains.com/issue/KT-1447/Please-add-support-for-traditional-fori10-i32-i-32-loops
)
2. Using c-style for leads to writing less secure code.
#### Bringing compound expressions in other control flow operators

### Multilet
Introduce a multilet construct that allows multiple variables to be checked for nullability and used within a block if none are null.
If we want to pass some clearly non-zero parameters to the function, we can do it like this.  
https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838
```kotlin
val result = a?.let { aNotNull ->
c?.let { cNotNull ->
someFunction(aNotNull, b, cNotNull);
}
}
```
This makes the code less clean and creates a lot of boilerplate code if the function has multiple parameters.
We propose to introduce a new syntax for this case.
#### Proposed Syntax
```kotlin
multilet (a, b, c) { nonNullA, nonNullB, nonNullC ->
// Code executed if a, b and c are not null
}
```
#### Potential uses
1. 1. Checking Multiple Input Sources
```kotlin
multilet (nameField.text, emailField.text, passwordField.text) { name, email, password ->
    validateAndSubmit(name, email, password)
}
```
#### Benefits
1. Code Cleanliness: Reduces nesting and improves code readability by reducing the number of nested let blocks.
2. Template Code Reduction: Reduces repetitive code checks to null.
3. Improved Reliability: Reduces the likelihood of errors due to misuse of nullable variables.
