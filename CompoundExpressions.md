

Example from https://discuss.kotlinlang.org/:
https://discuss.kotlinlang.org/t/anonymous-code-blocks-in-kotlin-versus-java/3250/5
Person want to write this code in Kotlin:
```kotlin
val parser = matchingParsers[0] ?:  {
	LOG.info("Log something here")
	return null
}

parser.parse(...)
```
instead of this:
```kotlin
val parser = matchingParsers[0] ?: run {
	LOG.info("Log something here")
	return null
}

parser.parse(...)
```
But he can't do this, because in Kotlin we can't use anonymous code blocks.

Another example from https://discuss.kotlinlang.org/:
https://discuss.kotlinlang.org/t/anonymous-code-blocks-in-kotlin-versus-java/3250/9
Person want to write this code in Kotlin:
```kotlin
val iter = list.iterator()
while (iter.hasNext()) {
    val a = iter.next()
    a ?: {iter.remove();continue} // remove null element and continue loop.
    //do something else
}
```
instead of this:
```kotlin
val iter = list.iterator()
while (iter.hasNext()) {
    val a = iter.next()
    if (a == null) {
        iter.remove()
        continue
    }
    //do something else
}

```
But with using of this feature https://youtrack.jetbrains.com/issue/KT-1436/Support-non-local-break-and-continue he can write this code:
```kotlin
val iter = list.iterator()
while (iter.hasNext()) {
    val a = iter.next()
    a ?: run {iter.remove();continue} // remove null element and continue loop.
    //do something else
}
```
Therefore, I think that the example is not relevant, since it is essentially the same.
But this thread about anonymous code blocks.



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

pros of adding "old-style" loops:
1. reverse loop:
```kotlin
for (int i = array.length - 1; i >= 0; --i) {
    val element = array[i]
    ...
}
```
Now we can do in this way:
```kotlin
for (i in array.length - 1 downTo 0) {
    val element = array[i]
    
}
```
2. The iteration with a step different from 1:
```kotlin
for (int i = 0; i < array.length; i += 2) {
    val element = array[i]
    ...
}
```
answer from Andrey Breslav about adding "old-style" loops:
https://youtrack.jetbrains.com/issue/KT-1447/Please-add-support-for-traditional-fori10-i32-i-32-loops


Discussion about "why assignments are not expressions, and only expressions are allowed in this context":
https://discuss.kotlinlang.org/t/assignment-not-allow-in-while-expression/339

Interesting example from this discussion:
https://discuss.kotlinlang.org/t/scoped-variable-assignment-used-inside-if-statement/17232
```C++
if (auto controller = getController())
{
controller.do();
}
else
{
// controller ptr is invalid here and outside if statement
}
```
But solution from this thread is:
```kotlin
when(val controller = getController()){
   null -> doSomething() 
   else -> controller.do() 
}
```
Accordingly, the question arises about the need for scopes and compound expressions in if-else statements.



## Benefits of adding compound expressions to a for loop
###  changing iteration boundaries
https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57
```kotlin
for (val i = 0; i < numIterations; i++) {

  System.out.print(text.charAt(i));

  if (someCondition()) {
    numIterations–-;
  }

}
```
### multiple variables iteration
https://discuss.kotlinlang.org/t/why-not-multi-for/2241

```kotlin
for (var i in 1..10; var j in 1..10) {
    println("$i $j")
}
```
### dynamic step
https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429
```kotlin
for(var i = 0; i < 500; i+= (if (i < 40) 10 else 20)) {
    println("Now at $i")
}
```




Abstracting from cycle for, this is why compound expressions can be useful:
https://discuss.kotlinlang.org/t/why-i-cant-apply-value-inside-while-loop/7762




## Сalls methods only if some parameters are not null
Now it looks like this, and accordingly has many disadvantages such as:
- makes the code less clean
- creates a lot of boilerplate code if a function takes many parameters
https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838
```kotlin
val result = a?.let { aNotNull ->
c?.let { cNotNull ->
someFunction(aNotNull, b, cNotNull);
}
}
```
## other methods available now
### 1. Using `let` with `Pair` Container 
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/2
- **Description**: Using `Pair` combined with the `let` extension function to handle two null parameters simultaneously.
- **Example**:
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
- **Drawbacks**: Less flexible and increases complexity with more than two parameters.
### 2. `ifNotNull` Function
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/4
- **Description**: Creating a generic `ifNotNull` function that executes code only if all parameters are non-null.
- **Example**:
```kotlin
inline fun <A, B, R> ifNotNull(a: A?, b: B?, code: (A, B) -> R) {
    if (a != null && b != null) {
        code(a, b)
    }
}
...
    fun test() {
        ifNotNull(name, age) { name, age ->
            doSth(name, age)
        }
    }
```
- **Drawbacks**: Need to overload the function for different numbers of arguments.
### 3. `callIfNotNull` Function
https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838/2
- **Description**: Using the `callIfNotNull` function as an extension on function references to call only if all parameters are non-null.
- **Example**:
```kotlin
inline fun <T1, T2, T3, R> KFunction3<T1, T2, T3, R>.callIfNotNull(a: T1?, b: T2?, c: T3?): R? {
    a ?: return null
    b ?: return null
    c ?: return null

    return this(a, b, c)
}

::someFunction.callIfNotNull(a, b, c)
```
- **Drawbacks**: Requires defining a separate function for each variable count.

## Proposed designs
### 1. Extended Safe Call Operator (`?.`)
https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838
- **Description**: Using the null-check operator (`?`) for conditional function calls.
- **Example**: `val result = someFunction(a?, b, c?)`.
- **Drawbacks**: Can be easily missed when reading code, adds complexity to the syntax.


### 2. Shortcut for Local Variable Declarations (`@localVal`)
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/12
- **Description**: A syntactic shortcut for creating local variables for null checks.
- **Example**: `if (@localVal name != null && @localVal age != null) {...}`.
- **Drawbacks**: Increases syntax complexity and ambiguity.
### 3. Similar to previous, but without `@localVal` and with using of commas
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/22
- **Description**: A syntactic shortcut for creating local variables for null checks, but without `@localVal` and with using of commas.
- **Example**:
```
if (val var1 = <expression1> ,val var2 = <expression2>, val varN = <expressionN>) {
  // Do something with var1, var2, varN
}
```  
- **Drawbacks**: Increases syntax complexity and ambiguity.
### 4. `let` Keyword Similar to Swift
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/14
- **Description**: Introducing a new `let` keyword similar to its use in Swift for creating local immutable variables within a block.
- **Example**: `if let email = emailField?.text, let password = passwordField?.text {...}`.
- **Drawbacks**: May add new complexity to the language and requires changes to the compiler.



https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/22
https://discuss.kotlinlang.org/t/feature-request-null-check-for-arguments-in-function-invoke/19838/8


## Potential uses of null-checking local variable functionality
### 1. `if` Statement
#### 1. Smartcastes to types without `?`
https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/22
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
### 2. `while` Loop
#### 1. Streaming Data Processing
In cases where the data comes from a stream (such as a file stream or network connection) and you want to continue processing while the stream is open and accessible.
```kotlin
while (val line = stream.readLine()) {
    // Processing every line
}
```
We can write similar code with existing Kotlin syntax:
```kotlin
generateSequence { stream.readLine() }.forEach { line ->
    
}


```

#### 2. Paged Data Loading
If you load data page by page (for example, from an API), where each request returns data for the next page as long as the data is available.
```kotlin
var page = 1
while (val data = api.loadData(page)) {
    process(data)
    page++
}

```


## Multilet
### Profits of adding multilet
1. Code Cleanliness: Reduces nesting and improves code readability by reducing the number of nested let blocks.
2. Template Code Reduction: Reduces repetitive code checks to null.
3. Improved Reliability: Reduces the likelihood of errors due to misuse of nullable variables.
### Possible syntax
```kotlin
multilet (a, b, c) { nonNullA, nonNullB, nonNullC ->
// Code executed if a, b and c are not null
}
```
### Possible usage 
1. Checking Multiple Input Sources
```kotlin
multilet (nameField.text, emailField.text, passwordField.text) { name, email, password ->
    validateAndSubmit(name, email, password)
}

