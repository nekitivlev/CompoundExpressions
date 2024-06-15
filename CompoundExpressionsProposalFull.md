# Compound expressions

A compound expression in programming languages is an expression that combines multiple operations or expressions into a single statement, allowing for the concise execution
of several actions. This allows developers to execute multiple related actions. The idea
of compound expressions is present in many programming languages. Such expressions
are very useful in contexts that require complex conditional logic and other complex code
constructions.


Kotlin provides compound expressions in many expressions, thanks to
scope functions, but in control flow expressions, they are practically nonexistent.
Here is an example of one of the few uses of compound expressions in control flow
expressions in Kotlin, which will also be useful for understanding the concept discussed
below:

<div id="listing-1"></div>

```kotlin
fun main() {
    println("Please enter a number:")
    when (val input = readlnOrNull()?.toIntOrNull()) {
        null -> println("That's not a valid number.")
        0 -> println("The number is zero.")
        in 1..Int.MAX_VALUE -> println("The number is positive: $input")
        else -> println("The number is negative: $input")
    }
}
```
<div style="text-align: center; margin-top: 5px;">
    <em>Listing 1:</a> Kotlin <code>when</code> statement with compound assignment</em>
</div>

As it can be seen in the [listing 1](#listing-1) on line 3, it is possible to use compound assignments in
Kotlin in ```when``` statements. First, we read a number and write its value to the val input.
Then we use input as a variable, which we check in different when branches. Thus, the
expression inside the parentheses of the when statement is compound. Unfortunately,
only one variable can be declared inside these parentheses. Also, if we declare a variable
inside the when parentheses, we can’t add any expressions inside these parentheses.

## Compound expressions in control flow expressions in other languages

### C++

In C++, compound expressions are quite powerful, especially within control flow struc-
tures. They often leverage the comma operator, which allows the execution of multiple
expressions where each expression is evaluated and the result of the last expression is
returned.

<div id="listing-2"></div>

```C++
for (int i = 0, j = 100; i < j; i++, j--) {
// Loop body
}
```
<div style="text-align: center; margin-top: 5px;">
    <em>Listing 2: C++ <code>for</code> loop</em>
</div>

On the [listing 2](#listing-2), we consider the C++ for loop, where the comma operator is used to
manage two variables simultaneously in the loop’s initialization and progression expres-
sions. i is incremented, and j is decremented with each iteration of the loop. This kind
of compound expression is very helpful in situations when we need to update multiple
counters or indices synchronously. C++ also supports complex conditions inside the if
statement and other control flow constructions, where we can execute some expressions
before checking the condition.


<div id="listing-3"></div>

```C++
if (int x = f(), y = g(); x > y) {
    std::cout << "x is greater than y";
}
```

<div style="text-align: center; margin-top: 5px;">
    <em>Listing 3: C++ <code>if</code> statement with compound assignments</em>
</div>

On the [listing 3](listing-3), we consider the C++ if statement, where the comma operator is used
to define two variables before the condition within the if, and a semicolon is used to
separate the variable declaration from the expression being checked.

This use of initialization statements in if conditions is a feature introduced in [C++17](https://en.cppreference.com/w/cpp/language/if),
enhancing the language’s ability to handle compound expressions cleanly.

<div id="listing-4"></div>

```C++
switch(int x = f(); x) {
    case 20:
        std::cout << "The value is doubled to 20." << std::endl;
        break;
    default:
        std::cout << "The value is not doubled to 20." << std::endl;
        break;
}
```

<div style="text-align: center; margin-top: 5px;">
    <em>Listing 4: C++ <code>switch</code> statement with compound assignments</em>
</div>

On the [listing 4](listing-4), we consider the C++ switch statement, where the initialization of the
variable x is before the condition that is checked in the switch construction. The initial-
ization of the variable x and the condition to be checked are separated by a semicolon.
This use of initialization statements in switch conditions is a feature introduced in [C++17](https://en.cppreference.com/w/cpp/language/switch), enhancing the language’s ability to handle compound expressions cleanly.


<div id="listing-5"></div>

### Java
Java has a classic ```for``` loop.

```java
for(int i=0; i < n; i++){

}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-5">Listing 5:</d> Java <code>for</code> loop</em>
</div>

On this listing 5, we are considering a classic for loop from Java, it has three different
sections, just like for loop from C++ ([2](#listing-2)).

### Go

Go supports compound assignments in [```if``` statements](https://go.dev/ref/spec##If_statements). A simple expression may
precede an expression that is checked inside an ```if``` statement.


<div id="listing-6"></div>

```go
if x := f(); x < y {
    return x
} else if x > z {
    return z
} else {
    return y
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-6">Listing 6:</d> go <code>if</code> statement with compound expression</em>
</div>

### JavaScript

JavaScript has a [comma operator](https://www.geeksforgeeks.org/javascript-comma-operator/) that is very similar in functionality to the comma operator in C++. It calculates the value of left-to-right expressions and returns the value of
the rightmost expression as the result. This makes it possible to use compound expressions in control flow statements in JavaScript.

<div id="listing-7"></div>

```javascript
let x = 1, y = 2;
if ((x++, y++, x + y > 5)) {
    console.log("Result is greater than 5");
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-7">Listing 7:</d> JavaScript <code>if</code> statement with compound expression</em>
</div>

On the [listing 7](#listing-7), we consider JavaScript if statement with compound expression, on line
2 we can see that before checking x+y>5 we increment x and y. We use the comma
operator to sequentially execute the expression inside the brackets on line 1.

<div id="listing-8"></div>

```javascript
for (let a = 0, b =5; a <= 5; a++, b--) {
    console.log(a, b);
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-8">Listing 8:</d> JavaScript <code>for</code> statement with compound expression</em>
</div>

On the [listing 8](#listing-8), we consider JavaScript for statement with compound expression, on
line 1 we can see that define a and b and then increment a and decrement b inside the
for loop. We use the comma operator to define two variables inside one definition block
and change their values inside one iteration block of the for statement.

### Swift

Swift’s approach to compound expressions in control flow statements, especially in if
statements includes optional binding mixed with boolean conditions. This mechanism
helps to make if statements more safe and clear, because helps to avoid null pointer
exceptions which is a common problem in a lot of languages, and also makes code clear.

<div id="listing-9"></div>

```swift
if let x = getX(), let y = getY(), x > y {
    print("x is greater than y")
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-9">Listing 9:</d> Swift <code>if</code> statement with compound expression</em>
</div>

On the [listing 9](#listing-9), we consider Swift if statement with compound expression, on line 1 we
can see that we use let statements inside if statement to safely unwrap optional values
returned by getX() and getY(). If both values are non-null and x is greater than y, the
body of the if statements executes.

Each of these examples shows that in different languages we have different approaches
and syntactic features for handling compound expressions in control flow statements.
They also reflect each language’s overall design goals and philosophies. These things
can be different in different languages. Therefore, we cannot blindly transfer constructs
from these languages to Kotlin.

## Existing solutions for compound expressions in control flow statements in Kotlin

Some people love the classic ```for``` loop so much that they resort to writing their own for
loop in Kotlin using existing language constructs in Kotlin:

<div id="listing-10"></div>

```kotlin
fun main() {
    For(1, { it < 10 }, { it + 1 }) { i ->
        print(i)
    }

    val array = charArrayOf('o', 'n', '\n', 'o', 'l', 'l', 'e', 'h')

    For(array.size - 1, { it >= 0 }, { it - 1 }) { i ->
        print(array[i])
        if (array[i] == '\n') return@For andBreak()
    }

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

inline fun <T> For(init: T, condition: (T) -> Boolean, increment: (T) -> T,
    body: BreakScope.(T) -> Unit) {
        val scope = BreakScope()
        var counter = init
        while(condition(counter)) {
            scope.body(counter)
            if(scope.isBroken) break
            counter = increment(counter)
        }
    }
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-10">Listing 10:</d> go <code>if</code> statement with compound expression</em>
</div>

On the [listing 10](#listing-10), we consider [one of the implementations](https://discuss.kotlinlang.org/t/any-reason-to-not-keep-the-good-old-for-loop-format/25287/20) for statement proposed by
the Kotlin community using the existing language features. This code gives a flexible
loop construct in Kotlin. For its implementation, higher-order functions are used that allow
breaking out of the loop in a more controlled way by encapsulating the break logic within
a BreakScope. However using higher-order functions makes the code inefficient, so this
solution cannot be called a good one. It is also important to note that in some control flow
expressions such as when there is a limited use of compound expressions.

We can declare a variable and also assign a value to it within when declaration. Also, the ability to declare a variable inside when statement brackets make it possible to create
something similar in essence to if from C++ with one nested variable creation inside if
parentheses. Because if is syntactic sugar over when in Kotlin.

<div id="listing-11"></div>

```kotlin
if(int x = y(); x){
    std::cout << "x is null":
}else{
    std::cout << "x is not null";
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-11">Listing 11:</d> C++ <code>if</code> with compound assignment</em>
</div>

On the [listing 11](#listing-11), we consider C++ if statement with the compound declaration of vari-
able x in line 1. After that, this variable is checked for equality to null, and then a
message corresponding to the result of the check is displayed.

<div id="listing-12"></div>

```kotlin
when(val x = y()){
    null -> println("x is null")
    else -> println("x is not null")
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-12">Listing 12:</d> Kotlin <code>when</code> with compound assignment</em>
</div>

On the [listing 12](#listing-12), we consider Kotlin when statement with the compound declaration of
variable x in line 1. After, this variable is checked for equality to null in line 2, and if it is
equal to null, the expression from line 2 is printed, otherwise from line 3.

## Problems with working with several nullable variables 
Kotlin prides itself on null safety, but the current mechanisms for dealing with multiple
nullable variables can sometimes lead to less clean code and an increase in boilerplate.
For instance, when calling a function only if certain parameters are not null, developers
might resort to nested let blocks:

<div id="listing-13"></div>

```kotlin
val result = a?.let { aNotNull ->
    c?.let { cNotNull ->
    someFunction(aNotNull, b, cNotNull)
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-13">Listing 13:</d> nested <code>let</code> blocks with several nullable variables</em>
</div>

On the [listing 13](#listing-13), we consider an example where the user needs to use two nested let
blocks to check and use two variables in one function call. Such solutions add unnecessary complexity and verbosity as the number of parameters increases.

## Existing solutions to the problem in working with multiple nullable variables

* #### [Using ```let``` with Pair container](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/2) 

<div id="listing-14"></div>

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
<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-14">Listing 14:</d> <code>let</code> with <code>Pair</code> container</em>
</div>

On the [listing 14](#listing-14), we consider a solution to the problem described earlier by using an
extension function on Pair. Paired objects in combination with let are used to simultaneously check two parameters that can be null. This approach, as discussed
in the [Kotlin discussions](https://discuss.kotlinlang.org/t/kotlin-null-check-for-multiple-nullable-vars/1946/2), provides less flexibility and increases complexity when
there are more than two parameters.

* #### Using of generic functions

<div id="listing-15"></div>

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

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-15">Listing 15:</d> generic function solution</em>
</div>

On the listing 21, we consider a solution to the problem described earlier by using
the generic function ifNotNull. This function executes only if all parameters are
non-null. Using a generic function reduces some boilerplate but requires overloading the function for different numbers of arguments, adding to the codebase’s
complexity.

* #### Using of extension functions

<div id="listing-16"></div>

```kotlin
inline fun <T1, T2, T3, R> KFunction3<T1, T2, T3, R>.callIfNotNull(a: T1?,
b: T2?, c: T3?): R? {
    a ?: return null
    b ?: return null
    c ?: return null

return this(a, b, c)
}

::someFunction.callIfNotNull(a, b, c)
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-16">Listing 16:</d> extension function solution</em>
</div>

On the [listing 22](#listing-22), we consider an extension callIfNotNull on function references
to call only if all parameters are non-null. This method simplifies calling functions
with nullable parameters but necessitates a separate function definition for each
variable count, which is not ideal for code maintenance and readability.

## Solutions to similar problems in other languages
Swift has a similar problem with null-checking multiple variables and solves
this by making it easy to declare local values within if statements:

<div id="listing-17"></div>

```swift
if let name = name, let age = age {
    doSth(name, age)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-17">Listing 17:</d> Swift if with let</em>
</div>

On the [listing 17](#listing-17), we consider usage of if with let to work with nullable variables
name and age. let statements try to unwrap the values of name and age. If both
variables contain non-null values, the block of code inside the if will execute. The
unwrapped variables name and age are only visible within the scope of the if block.

## Evaluation of research about control flow statements
Based on this evaluation, we will decide which of the control flow statements
should have compound expressions added to them.

### ```if```

As you can see from the examples ([3](#listing-3), [6](#listing-6), [7](#listing-7), [9](#listing-9)), compound expressions
in if statements are quite common among modern programming languages. We also
think that the case ([13](#listing-13)) when you need to check several nullable variables before passing
them to a function is quite important because functions and nullable variables are quite
common entities when writing code. We also think it is very important to note that if we
add compound expressions in a Swift-like manner, we will be able to create variables
directly inside the if and limit their scope to the scope of the if. This will help in solving
problems related to naming conflicts. Also, this feature will help prevent any null-related
problems related to variables that are declared inside if, outside of it, as they will not be
available outside of it.

In light of these benefits, we propose a new syntax for the if statement, which will add
the ability to declare local variables before the condition is checked in the if statement.

<div id="listing-18"></div>

```kotlin
if(val val1 = <expression1>; ... ; val valN = <expressionN>; <if_expression>){

}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-18">Listing 18:</d> Proposed syntax of <code>if</code> with compound expressions</em>
</div>

In [listing 18](#listing-18), we consider our proposed syntax for an if statement with compound expressions. We propose, similar to what is done in [C++](#listing-3) and [Swift](#listing-9), to allow variables to
be declared before the condition is checked.

Let’s also consider this example of using compound expressions inside an if statement.

<div id="listing-19"></div>

```kotlin
fun whoIsOldest(person1: Person?, person2: Person?) {
    if (val p1 = person1; val p2 = person2; val age1 = p1.age; age2 = p2.age;
        p1 != null && p2 != null && age1 != null && ag2 != null) {
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

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-19">Listing 19:</d> Direct Smart Casts for nullable types</em>
</div>

On the [listing 19](#listing-19), we consider a scenario where we determine which of two individuals
is older, and both are represented by nullable Person objects. The enhanced if syntax facilitates direct checks and smart casts, allowing for seamless access to properties like
age without additional null checks.
The benefit in general is that you can use earlier values in later expressions. In the [listing 19](#listing-19), p1 and p2 have already been null-checked, so we can access their age property
directly. And because the expressions can be anything that returns a nullable type they
can also be used with safe-casts.

