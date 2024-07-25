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

In C++, compound expressions are quite powerful, especially within control flow structures. They often leverage the comma operator, which allows the execution of multiple
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

On the [listing 2](#listing-2), we consider the C++ ```for``` loop, where the comma operator is used to
manage two variables simultaneously in the loop’s initialization and progression expressions. ```i``` is incremented, and ```j``` is decremented with each iteration of the loop. This kind
of compound expression is very helpful in situations when we need to update multiple
counters or indices synchronously. C++ also supports complex conditions inside the ```if```
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

On the [listing 3](#listing-3), we consider the C++ ```if``` statement, where the comma operator is used
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

On the [listing 4](#listing-4), we consider the C++ ```switch``` statement, where the initialization of the
variable ```x``` is before the condition that is checked in the ```switch``` construction. The initialization of the variable ```x``` and the condition to be checked are separated by a semicolon.
This use of initialization statements in ```switch``` conditions is a feature introduced in [C++17](https://en.cppreference.com/w/cpp/language/switch), enhancing the language’s ability to handle compound expressions cleanly.


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

On this [listing 5](#listing-5), we are considering a classic ```for``` loop from Java, it has three different
sections, just like ```for``` loop from C++ ([2](#listing-2)).

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

On the [listing 7](#listing-7), we consider JavaScript ```if``` statement with compound expression, on line
2 we can see that before checking ```x+y>5``` we increment ```x``` and ```y```. We use the comma
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

On the [listing 8](#listing-8), we consider JavaScript ```for``` statement with compound expression, on
line 1 we can see that define ```a``` and ```b``` and then increment ```a``` and decrement ```b``` inside the
```for``` loop. We use the comma operator to define two variables inside one definition block
and change their values inside one iteration block of the ```for``` statement.

### Swift

Swift’s approach to compound expressions in control flow statements, especially in ```if```
statements includes optional binding mixed with boolean conditions. This mechanism
helps to make ```if``` statements more safe and clear, because helps to avoid ```null``` pointer
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

On the [listing 9](#listing-9), we consider Swift ```if``` statement with compound expression, on line 1 we
can see that we use ```let``` statements inside ```if``` statement to safely unwrap optional values
returned by ```getX()``` and ```getY()```. If both values are non-```null``` and ```x``` is greater than ```y```, the
body of the ```if``` statements executes.

Each of these examples shows that in different languages we have different approaches
and syntactic features for handling compound expressions in control flow statements.
They also reflect each language’s overall design goals and philosophies. These things
can be different in different languages. Therefore, we cannot blindly transfer constructs
from these languages to Kotlin.


## Existing solutions for compound expressions in control flow statements in Kotlin

Some people love the classic ```for``` loop so much that they resort to writing their own ```for```
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
expressions such as ```when``` there is a limited use of compound expressions.

We can declare a variable and also assign a value to it within ```when``` declaration. Also, the ability to declare a variable inside ```when``` statement brackets make it possible to create
something similar in essence to ```if``` from C++ with one nested variable creation inside ```if```
parentheses. Because ```if``` is syntactic sugar over ```when``` in Kotlin.

<div id="listing-11"></div>

```kotlin
if(int x = y(); x){
    std::cout << "x is not null":
}else{
    std::cout << "x is null";
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-11">Listing 11:</d> C++ <code>if</code> with compound assignment</em>
</div>

On the [listing 11](#listing-11), we consider C++ if statement with the compound declaration of variable ```x``` in line 1. After that, this variable is checked for equality to ```null```, and then a
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

On the [listing 12](#listing-12), we consider Kotlin ```when``` statement with the compound declaration of
variable ```x``` in line 1. After, this variable is checked for equality to ```null``` in line 2, and if it is
equal to ```null```, the expression from line 2 is printed, otherwise from line 3.

## Problems with working with several nullable variables 

Kotlin prides itself on ```null``` safety, but the current mechanisms for dealing with multiple
nullable variables can sometimes lead to less clean code and an increase in boilerplate.
For instance, when calling a function only if certain parameters are not null, developers
might resort to nested ```let``` blocks:

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

On the [listing 13](#listing-13), we consider an example where the user needs to use two nested ```let```
blocks to check and use two variables in one function call. Such solutions add unnecessary complexity and verbosity as the number of parameters increases.

After checking with BigCode it turned out that 286818 of 81170612 files (0.33%) contain two nested ```let```.

11371 out of 81170612 files (0.01%) contain three or more nested ```let```.

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
extension function on ```Pair```. Paired objects in combination with ```let``` are used to simultaneously check two parameters that can be null. This approach, as discussed
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

On the [listing 15](#listing-15), we consider a solution to the problem described earlier by using
the generic function ifNotNull. This function executes only if all parameters are
non-```null```. Using a generic function reduces some boilerplate but requires overloading the function for different numbers of arguments, adding to the codebase’s
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

On the [listing 16](#listing-16), we consider an extension ```callIfNotNull``` on function references
to call only if all parameters are non-```null```. This method simplifies calling functions
with nullable parameters but necessitates a separate function definition for each
variable count, which is not ideal for code maintenance and readability.

## Solutions to similar problems in other languages

Swift has a similar problem with null-checking multiple variables and solves
this by making it easy to declare local values within ```if``` statements:

<div id="listing-17"></div>

```swift
if let name = name, let age = age {
    doSth(name, age)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-17">Listing 17:</d> Swift if with let</em>
</div>

On the [listing 17](#listing-17), we consider usage of ```if``` with ```let``` to work with nullable variables
```name``` and ```age```. ```let``` statements try to unwrap the values of ```name``` and ```age```. If both
variables contain non-```null``` values, the block of code inside the ```if``` will execute. The
unwrapped variables ```name``` and ```age``` are only visible within the scope of the ```if``` block.

## Evaluation of research about control flow statements
Based on this evaluation, we will decide which of the control flow statements
should have compound expressions added to them.

### ```if```

As you can see from the examples ([3](#listing-3), [6](#listing-6), [7](#listing-7), [9](#listing-9)), compound expressions
in ```if``` statements are quite common among modern programming languages. We also
think that the case ([13](#listing-13)) when you need to check several nullable variables before passing
them to a function is quite important because functions and nullable variables are quite
common entities when writing code. We also think it is very important to note that if we
add compound expressions in a Swift-like manner, we will be able to create variables
directly inside the ```if``` and limit their scope to the scope of the ```if```. This will help in solving
problems related to naming conflicts. Also, this feature will help prevent any ```null```-related
problems related to variables that are declared inside ```if```, outside of it, as they will not be
available outside of it.

In light of these benefits, we propose a new syntax for the ```if``` statement, which will add
the ability to declare local variables before the condition is checked in the ```if``` statement.

<div id="listing-18"></div>

```kotlin
if(val val1 = <expression1>; ... ; val valN = <expressionN>; <if_expression>){

}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-18">Listing 18:</d> Proposed syntax of <code>if</code> with compound expressions</em>
</div>

In [listing 18](#listing-18), we consider our proposed syntax for an ```if``` statement with compound expressions. We propose, similar to what is done in [C++](#listing-3) and [Swift](#listing-9), to allow variables to
be declared before the condition is checked.

Let’s also consider this example of using compound expressions inside an ```if``` statement.

<div id="listing-19"></div>

```kotlin
fun whoIsOldest(person1: Person?, person2: Person?) {
    if (val p1 = person1; val p2 = person2; val age1 = p1.age; val age2 = p2.age;
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
is older, and both are represented by nullable ```Person``` objects. The enhanced if syntax facilitates direct checks and smart casts, allowing for seamless access to properties like
age without additional ```null``` checks.
The benefit in general is that you can use earlier values in later expressions. In the [listing 19](#listing-19), ```p1``` and ```p2``` have already been ```null```-checked, so we can access their ```age``` property
directly. And because the expressions can be anything that returns a nullable type they
can also be used with safe-casts.

<div id="listing-20"></div>

```kotlin
if (val child = person as? Child; val car = child.favouriteToy as? Car;
    child != null && car != null) {
    car.race()
    print("$child is racing their toy $car")
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-20">Listing 20:</d> Safe casts example with <code>if</code> with compound expressions</em>
</div>

On the [listing 20](#listing-20), we consider the example of using safe-casts with compound expressions in the ```if``` statement. In the example, the variables are checked for conformity to the
required type, and if the type is correct and non-```null```, the body of ```if``` is executed. This is
a fairly common use case to check if something is non-```null``` and then perform an additional
check to see if it is appropriate to use it.

So we can see that adding compound expressions to an ```if``` statement will have an impact
on safe casts. Safe casts following a compound assignment offer improved type safety.
Since the variables are only accessible within the ```if``` body after passing the ```null``` checks,
the compiler can guarantee their types, avoiding the potential for type-related errors.

We would also like to point out that adding compound expressions to an ```if``` statement will
reduce the amount of boilerplate code in cases like this [on listing 13](#listing-13) since it eliminates the
need to use nested ```let``` blocks or separate individual variable checks.

In light of the previously listed benefits of adding compound expressions to the ```if``` statement, we think it is appropriate to add compound expressions to [the ```if``` statement in the form we have proposed](#listing-18).

### ```when```

Now let’s turn our attention to the ```when``` statement. After studying the Kotlin compiler, we learned that ```if``` is syntactic sugar over ```when```.

Compared to ```if```, ```when``` does not have as many counterparts with compound expressions.
But there is still an [example](#listing-4) (```switch``` is the analog of when in C++). We also managed
to find a [request on youtrack](https://youtrack.jetbrains.com/issue/KT-25698) that suggests adding the ability to declare variables
inside ```when``` parentheses, similar to what [we suggested for ```if```](#listing-18).

<div id="listing-21"></div>

```kotlin
when (val x = a.foo(); bar(a, x)) {
    is Case1 -> doStuff1(a, x)
    is Case2 -> doStuff2(a, x)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-21">Listing 21:</d> <code>when</code> with compound variable initialization</em>
</div>

<div id="listing-22"></div>

```kotlin
when (val x = a.foo() as? buz; val y = b.foo() as? buz; x != null && y != null) {
    true -> doStuff1(y, x)
    else -> doStuff2(y, x)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-22">Listing 22:</d> <code>when</code> with compound variable initialization and null</em>
</div>

On the [listing 21](#lising-21), we’re looking at an example of a compound expression in a ```when``` statement. Here, like in C++, a variable is initialized first, followed by an expression that will
influence the choice of one or another branch within ```when```.

We think this is a good example of where compound expressions can be used because
it has the same advantages as adding compound expressions to ```if```.

On the [listing 22](#listing-22), we consider the example of using safe casts with compound expressions in the ```when``` statement. In the example, the variables are checked for conformity to
the required type, and after that, if the type is correct and non-```null```, the ```true``` branch is
executed, otherwise ```false```.

Thus, incorporating compound expressions into the ```when``` statement can enhance type
safety by ensuring that variables are accessible within the ```when``` body only after successful
```null``` checks. Also, adding compound expressions to ```when``` will make working with nullable
variables better because if they are declared inside ```when``` statements, their parentheses
will be restricted to those parentheses.

In light of all these benefits, we propose our prototype ```when``` with compound expressions.


<div id="listing-23"></div>


```kotlin
when (val val1 = <expression1>; ... ;val valN = <expressionN>;<when_expression>) {

}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-23">Listing 23:</d> Proposed syntax of <code>when</code> statement</em>
</div>

On the [listing 23](#listing-23), we consider our prototype syntax. Now it will be possible to declare
variables before declaring a condition that is checked in ```when```. Declarations of different
variables are separated by semicolons. At the end of the expression in brackets must be
a condition, according to which the ```when``` branches will be selected.

There is also an idea to add the ability to only declare variables in the init block and leave when without a condition, so that only to enter some variables in the when scope and then use them there, but a prototype of this kind has not been implemented.


<div id="listing-24"></div>

```kotlin
when(x; y; ){
    x != 5 && y != 10 -> println("5 and 10")
    else -> println("no")
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-24">Listing 24:</d> <code>when</code> without expression</em>
</div>

### Addtitional notes about null checks in ```when``` and ```if``` prototype
There was also the idea of making null handling something similar to the existing mechanism with ```!``` and ```?```.

The idea is to add to ```val``` ```!``` sign in case the variable is definitely not ```null``` and if ```null``` is passed to it further execution is interrupted and ```?``` in case the variable is ```null``` execution is not interrupted.

Example of that syntax:

<div id="listing-25"></div>

```kotlin
// in this case if fun will return null execution will be interupted
if(val! x = fun(); x > 10){

}

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-25">Listing 25:</d> example with val!</em>
</div>

<div id="listing-26"></div>

```kotlin
// in this case if fun will return null execution will not be interupted
if(val? x = fun(); x > 10){

}

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-26">Listing 26:</d> example with val?</em>
</div>

### Compound expressions in ```when``` branches

Introducing compound expressions in the conditions of ```when``` branches can further enhance code readability and maintainability in Kotlin. This feature would allow developers to declare and initialize variables directly within the condition of each ```when``` branch, leading to more concise and expressive code.

#### Proposed syntax

<div id="listing-27"></div>

```kotlin
when {
    (val a = expr1; a > 10) -> { /* code block */ }
    (val b = expr2; b < 5) -> { /* code block */ }
    else -> { /* code block */ }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-27">Listing 27:</d> possible syntax of when branches with compound expressions</em>
</div>

#### Benefits

1. **Enhanced Readability:** Keeps the initialization and the condition in a single place, improving the readability of complex conditions.
2. **Reduced Boilerplate:** Eliminates the need for variable declarations outside the when statement, reducing boilerplate code.
3. **Scoped Variables:** Ensures that variables declared within the condition are scoped to the corresponding branch, preventing misuse outside their intended context.

#### Potential Uses

1. **Complex Condition Evaluation:** Useful when multiple variables are needed to evaluate conditions, reducing the need for nested or sequential checks.
2. **Smart Casting:** Facilitates smart casting within the ```when``` branches, ensuring variables are properly typed.
3. **Streamlined Logic:** Combines initialization and logic in one place, which is particularly beneficial for handling nullable types or performing preliminary calculations.


### Additional notes about alternative syntax for compound expressions in ```if```
Another potential syntax looks like this. 

<div id="listing-27"></div>

```kotlin
if (a > b && val x = someCalculation() && x > 10 && val y = anotherCalculation(x) && y < 20) {
    // Block to execute
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-27">Listing 27:</d> Potential syntax for <code>if</code> with compound variables declaration</em>
</div>

In this syntax we make it possible to declare variables in any part of the expression that is used inside ```if```.
Such syntax has several primes in comparison with [syntax that was proposed initially](#listing-18):


1. ***Scoped Variable Declarations:***
    * ***Proposed Syntax:*** Variables declared within the ```if``` condition are scoped to that block, ensuring they are only accessible within the block. This helps prevent unintended side effects and keeps the code clean and safe.
    * [***Init Block Syntax:***](#listing-14) Similarly, variables declared in the init block are also scoped to the ```x``` statement, but combining declarations and checks in one line enhances readability.
  
2. ***Enhanced Perfomance:***
    * ***Proposed Syntax:*** Allows variables to be checked for various conditions as soon as they are declared. And if the variables do not satisfy them, interrupt execution of subsequent expressions.


    ```kotlin
    if (a > b && val x = someCalculation() && x != null && x > 10 && val y = anotherCalculation(x) && y < 20) {
        // Block to execute
    }
    ```


    * [***Init Block Syntax:***](#listing-14)  Requires you to first check to declare all variables and then check all of them in a separate part of the ```if```-statement condition.

    ```kotlin
    if (val x = someCalculation(); val y = anotherCalculation(x); a > b && x != null && x > 10 && y < 20) {
    // Block to execute
    }
    ```


But this syntax also has some disatvantages. 

1. ***Reduced Readability:***

    * ***Proposed Syntax:*** Using && to combine variable declarations and conditions in a single line can make the code less readable, especially when multiple variables and conditions are involved. The combined expressions can become cluttered and harder to parse quickly.
    
    ```kotlin
    if (a > b && val x = someCalculation() && x > 10 && val y = anotherCalculation(x) && y < 20) {
    // Block to execute
    }
    ```

    * [***Init Block Syntax:***](#listing-14) Having a separate initialization block keeps the code cleaner and more readable by clearly separating variable declarations from the conditions.

    ```kotlin
    if (val x = someCalculation(); val y = anotherCalculation(x); a > b && x > 10 && y < 20) {
    // Block to execute
    }
    ```

2. ***Difficulty in Debugging:***
    * ***Proposed Syntax:*** Debugging becomes more challenging with the proposed syntax because all the declarations and conditions are combined. It can be difficult to identify which part of the expression caused an issue or which variable failed the condition.

    * [***Init Block Syntax:***](#listing-14) The init block approach makes it easier to isolate and debug each variable initialization and condition, as each declaration and condition is explicitly separated.

3. ***Inconsistent Flow Control:***
    * ***Proposed Syntax:*** Combining multiple declarations and conditions with && can lead to inconsistent flow control, especially if side effects are present in the expressions. The order of evaluation and potential side effects can become less predictable.

    * [***Init Block Syntax:***](#listing-14) The init block syntax provides more consistent and predictable flow control, as each declaration and condition is evaluated in a clear, sequential manner.

### ```for```

A ```for```-loop is a type of loop specifically designed to iterate over collections or any iter-
able sequence of elements. It includes an iteration variable, a container expression that
provides the elements, and a loop body that executes each element in [the iterable](https://kotlinlang.org/spec/statements.html#loop-statements).

The ```for```-loop is a syntactic construct that can be overloaded, expanding as follows:

<div id="listing-28"></div>

```kotlin
when(val $iterator = C.iterator()) {
    else -> while ($iterator.hasNext()) {
            val VarDecl = __iterator.next()
            <... all the statements from Body>
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-28">Listing 28:</d> <code>for</code>-loop expanding</em>
</div>

On the [listing 28](#listing-28), we consider expansion of ```for(VarDecl in C)``` Body. It is the same as
[24](#listing-24) where ```iterator```, ```hasNext```, ```next``` are all suitable operator functions available in the
current scope. ```VarDecl``` here may be a variable name or set of variables.

As you can see from the examples ([2](#listing-2), [8](#listing-8), [5](#listing-5)), classic ```for``` loop is quite
common among modern programming languages. Also, the fact that people are inventing
their own implementations using the existing [syntax](#listing-10) and creating various discussions
related to adding the classic ```for``` loop to Kotlin shows that this idea is quite popular in the
Kotlin community ([Discuss.kotlinlang.org. for loop with dynamic condition](https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57), [Discuss.kotlinlang.org. For-loop dynamic step](https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429), [youtrack. KT-1447. Please add support for traditional for](https://youtrack.jetbrains.com/issue/KT-1447/Please-add-support-for-traditional-fori10-i32-i-32-loops), [Discuss.kotlinlang.org: Community’s Realization of Classic For in Kotlin with Exist-
ing Code Features](https://discuss.kotlinlang.org/t/any-reason-to-not-keep-the-good-old-for-loop-format/25287/20)).

The traditional ```for``` loop, which can be found in such languages as [Java](#listing-5), [C++](#listing-2),
and C, offers syntax that is familiar to many programmers. It provides clean and concise
iteration across a range of values, with the ability to easily change the loop’s index variable
and conditionally control loop execution. Familiarity and ease of use make it an attractive
feature for many developers switching to Kotlin from other languages.

Let’s look at an example of what a classic ```for``` loop might look like in Kotlin.


<div id="listing-29"></div>

```kotlin
for (val i = 0; i < numIterations; i++) {
// loop-body
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-29">Listing 29:</d> Proposed syntax of classic <code>for</code> loop in Kotlin</em>
</div>

On the [listing 29](#listing-29), we are looking at what a classic ```for``` loop in Kotlin might look like. The
variable that is created for iteration, in this case, ```i```, cannot be changed inside the loop
body, but it is changed according to the rule described at the end of the expression written
in brackets in ```for``` (in this example, ```i++```). Also in the center, it records the condition when
the loop exits (in this example, ```i < numIterations```).

Let’s consider potential use cases for this syntax.

<div id="listing-30"></div>

```kotlin
for (val i = 0; i < numIterations; i++) {
    print(text.charAt(i))
    if (someCondition()) {
        numIterations=numIterations-1
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-30">Listing 30:</d> Changing iteration boundaries while traversing a loop example</em>
</div>

On the [listing 30](#listing-30), we consider an example of using the classic for proposed on [the
discuss.kotlinlang.org](https://discuss.kotlinlang.org/t/for-loop-with-dynamic-condition/57). In this example, the right border of the segment along which the variable is iterated is changed. This is not possible at the moment because the boundaries along which the iteration is performed are created when creating for
and are not changed further [24](#listing-27). Although this example looks quite convincing, we don’t
think it is a good practice to write such code because, even with such a simple example,
it is quite difficult to predict the program’s behavior because it is not always obvious at
which step the loop will be exited. Writing such constructs also complicates finding errors
in the program. It is also important to note that this example can be rewritten using ```while```
in the current Kotlin syntax.

<div id="listing-31"></div>

```kotlin
var i = 0
while(i < numIterations){
    print(text.charAt(i))
    if (someCondition()) {
        numIterations=numIterations-1
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-31">Listing 31:</d> changing iteration boundaries while traversing a loop example</em>
</div>

On the [listing 31](#listing-31), we consider a workaround of the previously discussed example of the
usage of classic ```for```. The disadvantages of this workaround are that the ```i``` variable is
visible outside ```while```, and it can also be changed inside the ```while``` body (all this adds
unnecessary uncertainty in program execution). Also, separating the declaration and the
rules by which the variable we are iterating on changes makes the code less readable.

Let’s look at another example.

<div id="listing-32"></div>

```kotlin
for(val i = 0; i < 500; i+= (if (i < 40) 10 else 20)) {
    println("Now at $i")
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-32">Listing 32:</d> Dynamically changing the step while iterating through a loop</em>
</div>

On the [listing 32](#listing-32), we consider an example of using the classic ```for``` proposed on the
[discuss.kotlinlang.org](https://discuss.kotlinlang.org/t/for-loop-dynamic-step/6429). In this example, the variable being iterated over can
be changed by 10 or 20, depending on its value. This example shows how much more
flexible the classic ```for``` loop can be. Despite this, we believe that writing such constructs
negatively affects code readability and complicates it. It is also important to note that this
example can be rewritten quite easily using ```while``` in the current Kotlin syntax.

<div id="listing-33"></div>

```kotlin
var i = 0
while( i < 500 ){
    println("Now at $i")
    i += if( i < 40 ) 10 else 20
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-33">Listing 33:</d> Dynamically changing the step while iterating through a loop</em>
</div>

On the [listing 33](#listing-33), we consider a workaround of the previously discussed example of the
usage of classic ```for```. The disadvantages of this workaround are that the ```i``` variable is
visible outside ```while```, and it can also be changed inside the ```while``` body (all this adds unnecessary uncertainty in program execution). Also, separating the declaration and the
rules by which the variable we are iterating on changes makes the code less readable. 

Thus, it turns out that adding the classical ```for``` can improve code readability since its use
reduces the need for external initialization and update operators, encapsulating all logic
related to the loop in the ```for``` statement. Also, declaring a variable inside ```for``` allows you
to restrict its scope, which is also useful because it helps you avoid naming conflicts.

Despite all the benefits of adding classic ```for``` in Kotlin described earlier, the important fact
remains that the ```for``` loop in Kotlin was originally consciously [designed only as ```forEach```](https://kotlinlang.org/spec/statements.html#loop-statements), so we think that adding compound expressions to the ```for``` loop, as proposed, makes
no sense because it violates language design.

### ```while```

Now let’s look at the ```while``` loop. The ```while``` loop is a basic loop that is used in Kotlin. It
is assumed to be used whenever we need a loop, except for iterations, since ```for``` exists
for them. Therefore, we think that adding compound expressions to ```while``` does not
contradict Kotlin’s language design, which is already a big plus compared to ```for```.

Let’s take a look at an example we managed to find during our research.

<div id="listing-34"></div>

```kotlin
val buffer = ByteArray(8192)
val bytesRead : Int
val byteArrayOutputStream = ByteArrayOutputStream()
val inputStream = FileInputStream(file)
while(val byteRead = inputStream.read(buffer); byteRead != -1){

}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-34">Listing 34:</d> streaming data processing with <code>while</code> loop example</em>
</div>

On the [listing 34](#listing-34), we consider an example of a ```while``` loop with compound variable initialization. This variable cannot be changed inside the ```while``` body. But it can be changed
between its iterations. The first question that arises in the case of adding such a feature.
The variable that is initialized in parentheses ```while``` loop is created once or must be created anew every iteration of the loop. This is a rather complicated question for which we
do not have any arguments, either for one side or the other. 
But the variant when a variable inside while changes only between iterations, but cannot be changed inside a block seems more promising.

## Prototypes implemenation

After studying the K2 compiler code, we came to the conclusion that the previously described prototypes for ```when``` and ```if``` can be implemented in two different ways: as syntactic sugar that will be resolved during ```RAW_FIR``` tree construction or by adding variables from the init block to the corresponding scope during ```IR``` tree construction.

Both the ```when``` and ```if``` prototypes have no built-in check for ```null```. 

### Implementation as syntactic sugar
The work on this prototype mainly affects the desugaring stage along
with changes in the parser. The implemented prototype can be found in the corresponding
[branch of the GitHub repository](https://github.com/nekitivlev/kotlin/tree/syntax_sugar_prototype).

#### ```if``` prototype

We decided that a good option would be to make a prototype ```if``` with a compound expression syntactic sugar on ```run``` function and an ordinary ```if```.
This means that the ```if``` with compound expressions will be desugared into a ```run```, which
will first declare all the variables we write in the parentheses of our ```if``` with compound
expressions, and then will be followed by an ordinary ```if``` with condition check from our ```if```
with compound expressions.


<div id="listing-35"></div>

```kotlin
run{
    val val1 = <expression1>
    ...
    val valN = <expressionN>
    if(<if expressions>){

    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-35">Listing 35:</d> desugared <code>if</code> prototype</em>
</div>

On the [listing 35](#listing-35), we can see what will be the desugared [prototype we talked about](#listing-18)
earlier. We decided to do it this way because in this case, the scoping of variables declared inside ```if``` with compound expressions will really correspond to the scope of the ```if```.

##### Changes in parser

For the parser part, the needed changes was to modify ```kotlin.compiler.psi.main.KotlinExpressionParsing.parseIf()``` function, which parse ```if``` statement. A necessary change is to add the ability to declare variables inside an ```if``` statement, and turn it into ```COMPOUND_EXPRESSION``` in case variables are declared. 

##### Changes in the ```RAF_FIR``` tree building

Since in the case of compiling ```if``` with compound expressions, we want to get a ```run```
scope function inside which variables and classic ```if``` will be declared. So the construction of ```RAW_FIR``` tree containing ```if``` with compound expressions will start with the call of
```convertCallExpression``` function inside ```LightTreeRawFirExpressionBuilder```. Here we
have made the necessary code modifications to build a tree corresponding to the run
scope function.

We also wrote our own function inside ```LightTreeRawFirExpressionBuilder``` responsible for constructing the anonymous function, which contains a block containing all the
variables declared with compound expression and our control flow statement.

Thus, the resulting prototype is an emulation of a ```run``` function containing variables and a
control flow statement declared with compound expressions.

#### ```when``` prototype

We decided that a good option would be to make a prototype when with a compound expression syntactic sugar on run function and an ordinary when.
This means that the ```when``` with compound expressions will be desugared into a ```run```, which
will first declare all the variables we write in the parentheses of our ```when``` with compound expressions, and then will be followed by an ordinary ```when``` with a condition check from
our ```when``` with compound expressions.


<div id="listing-36"></div>

```kotlin
run{
    val val1 = <expression1>
    ...
    val valN = <expressionN>
    when(<if expressions>){

    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-36">Listing 36:</d> desugared <code>when</code> prototype</em>
</div>

On the [listing 36](#listing-36), we can see what will be the desugared [prototype we talked about](#listing-23)
earlier. We decided to do it this way because, in this case, the scoping of variables
declared inside ```when``` with compound expressions will really correspond to the scope of
the ```when```.

##### Changes in parser

We modified this function in a similar way as we did for ```if``` statement. Thus, we do
not change the PSI tree that is built if the parser receives an ordinary when statement as
input, but if the parser receives a ```when``` statement with compound expressions as input,
then in addition to the variables declared inside the ```when``` statement with compound expressions, the following nodes will be added: ```CALL_EXPRESSION```, ```COMPOUND_EXPRESSION```,
```COMPOUND_EXPRESSION```, ```BLOCK```. As in the case of the ```if``` statement with compound expressions.

##### Changes in the ```RAF_FIR``` tree building

Since in the case of parsing when with compound expressions our tree contains nodes
```CALL_EXPRESSION```, ```COMPOUND_EXPRESSION```, ```COMPOUND_EXPRESSION```, ```BLOCK```, all the same actions will take place before entering the ```convertCompoundExpression``` function as they
did when building the tree by if with compound expressions. In order to add support
for when with compound expressions, we simply added a check inside the ```convertCompoundExpression``` function to see which node was passed to us as the control flow
statement node, depending on this, either when or if will be added to our anonymous
function. Thus we added support for compound expressions in the ```when``` statement.

### implemenatinon by adding variables from the init block to the corresponding scope during  ```IR``` tree construction

The work on this prototype mainly affects the parser, desugaring stage, IR tree building stage. The implemented prototype can be found in [the corresponding
branch of the GitHub repository](https://github.com/nekitivlev/kotlin/tree/when_with_multiple_arguments_resolution).

#### Changes in parser 

##### ```if```

For the parser part, the needed changes was to modify ```kotlin.compiler.psi.main.KotlinExpressionParsing.parseIf()``` function, which parse ```if``` statement. A necessary change is to add the ability to declare variables inside an ```if``` statement, in the case when there are no variables in the init block, the ```psi tree``` obtained during parsing remains unchanged.

##### ```when```

For the parser part, the needed changes was to modify ```kotlin.compiler.psi.main.KotlinExpressionParsing.parseWhen()``` function, which parse ```when``` statement. A necessary change is to add the ability to declare variables inside an ```when``` statement, in the case when there are no variables in the init block, the ```psi tree``` obtained during parsing remains unchanged.


#### Changes in desugaring stage

We added a parameter to ```FirWhenExpression``` that is responsible for variables in the init block. 

We also made necessary changes to the construction of ```RAW_FIR tree``` from both ```lightTree``` and ```PSI``` ```when``` and ```if```.

#### Changes in IR construction stage

Changes have been made here that add variables to the scope of the statements in which they were declared. 

## Diagnostics

Because of the fact that in the case of [implementaion through syntax sugar](#implementation-as-syntactic-sugar) compound ```when/if``` statement become a ```CALL_EXPRESSION``` with variables and ```when```/```if``` statement inside existing diagnostics do not work on them properly.

But if we are talking about [implemenatinon by adding variables from the init block to the corresponding](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction) scope during  ```IR``` tree construction diagnostics work properly with this prototype. 

We also written our own analysis tests to become confident in this fact. 

## Tests

Both implementations have been tested on existing tests and since they do not change the operation of the compiler if the existing syntax is used, they all pass.

Also the our own tests were written. Both implementations pass tests related to parsing. 

But as we already said diagnostics don't work properly with [first prototype](#implementation-as-syntactic-sugar). Because of this, most codegen tests run only with certain compiler settings that will turn off diagnostics.

But if we are talking about [second](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction) prototype all our tests passed in the case of running them on K2 compiler. 

## Benchmarks 

We also wrote our benchmarks.
As benchmarks we used the same examples containing different number of variables written with and without using init block in ```when``` and ```if``` statements.

We ran our benchmarks on these cases:
[first prototype](#implementation-as-syntactic-sugar), [second prototype](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction), on case when we declare variables and then use standart ```if```/```when```, on case when we declare variables and then use standart ```if```/```when``` inside ```run``` scope function.
Each test file was run 100 times with 10 warmups beforehand.
There is results. 

| case                  | Average compilation time | Average run time |
|-----------------------|------------------|----------|
| [first prototype](#implementation-as-syntactic-sugar) (```when```) | 2.69311 s| 0.04805 s| 
| [first prototype](#implementation-as-syntactic-sugar) (```if```)   | 2.53378 s| 0.04714 s|
| [second prototype](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction) (```when```) | 2.35559 s | 0.03988 s |
| [second prototype](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction) (```if```) | 2.36185 s | 0.04128 s |
| existing syntax (```if```) | 2.55353 s | 0.04535 s | 
| existing syntax (```when```) | 2.52543 s | 0.04278  s |
| existing syntax with run (```if```) | 2.72552 s | 0.04718 s|
| existing syntax with run (```when```) | 2.73926 s | 0.04447 s |

All benchmarks were run on ```Dell Precision 5570 with i9-12900H and 32 GB of RAM```.
The ```hyperfine``` utility was used for time measurement.

As you can see [first prototype](#implementation-as-syntactic-sugar) is relatively slow. 
But [the second](#implemenatinon-by-adding-variables-from-the-init-block-to-the-corresponding-scope-during--ir-tree-construction) shows good speed.

Tests cases: [existing syntax ```if```](https://github.com/nekitivlev/kotlin/tree/when_with_multiple_arguments_resolution/existingSyntaxExamplesIf), [existing syntax ```when```](https://github.com/nekitivlev/kotlin/tree/when_with_multiple_arguments_resolution/existingSyntaxExamplesWhen), [new syntax ```if```](https://github.com/nekitivlev/kotlin/tree/when_with_multiple_arguments_resolution/compoundSyntaxExamplesIf), [new syntax ```when```](https://github.com/nekitivlev/kotlin/tree/when_with_multiple_arguments_resolution/compoundSyntaxExamplesWhen).



# Scopes

As you can see earlier we have not a few arguments for adding compound expressions were built on the fact that it will be useful for working with scopes. But let's look at this area a bit more closely and also consider suggestions for improving scopes in Kotlin.


## Ways of working with scopes 

There are different approaches to work with scopes in various programming languages. 
But most popular languages use roughly the same approach for dealing with scopes.

### Kotlin 

In Kotlin, the scope of variables is determined by their placement in the code:
- **Local scope:** Variables declared inside a function are only accessible within that function.
- **Class scope:** Variables declared within a class (e.g., properties) are accessible within that class. Access can be controlled using visibility modifiers (private, protected, internal, public).
- **Package scope:** Functions and variables declared at the package level are accessible to all files within that package. The internal modifier makes them accessible only within the module.

### JavaScript

In JavaScript, scope is managed through different methods:
- **Function scope:** Variables declared with var inside a function are accessible throughout that function.
- **Block scope:** Variables declared with let and const are accessible only within the block in which they are declared (e.g., within a loop or conditional statement).

<div id="listing-37"></div>

```javascript
function example() {
  if (true) {
    var x = 10; 
    let y = 20; 
  }
  console.log(x); 
  console.log(y); 
}

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-37">Listing 37:</d> example of working with scopes in JavaScript </em>
</div>

### Python 

Python uses the LEGB rule (Local, Enclosing, Global, Built-in) to determine variable scope:

- **Local:** Variables declared inside a function.
- **Enclosing:** Variables declared in the enclosing functions (closures).
- **Global:** Variables declared at the module level.
- **Built-in:** Built-in names, such as print.

### C++

In C++, variable scope is defined as follows:

- **Local scope:** Variables declared inside functions or code blocks.
- **Global scope:** Variables declared outside all functions.
- **Class scope:** Variables declared within a class are accessible within that class.

### Swift 

Swift also employs multiple levels of scope:

- **Local scope:** Variables declared inside a function are only accessible within that function.

- **Class or struct scope:** Properties are accessible within their classes or structs. Access is controlled by modifiers (private, fileprivate, internal, public, open).

### Rust 

In Rust, scope is determined by modifiers and variable placement:

- **Modules and packages:** Variables and functions can be declared in modules using mod. Visibility is controlled by the pub modifier.

<div id="listing-38"></div>

```rust
mod example {
    pub fn public_function() {
        println!("This is a public function.");
    }

    fn private_function() {
        println!("This is a private function.");
    }
}

fn main() {
    example::public_function(); // accessible
    // example::private_function(); // error
}

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-38">Listing 38:</d> example of working with scopes in Rust </em>
</div>

But there are also other approaches for dealing with scopes. 

Some programming languages have the ability to delete to make a variable invisible in some scope, but this is often done through the use of macros and is not a feature built into the language.

### Julia

Julia has macros that allow for flexible code management. We can use a macro to remove a variable from an internal scope.

<div id="listing-39"></div>

```Julia
macro remove_var(x)
    return quote
        local $x
        nothing
    end
end

x = 5

if true
    @remove_var x
    # x not available here
end

println(x)  # x available here, output: 5
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-39">Listing 39:</d> example of deleting variable from scope in Julia </em>
</div>

### Nim

Nim also supports macros and code manipulation at compile time. Example of a macro to remove a variable from a scope:

<div id="listing-40"></div>

```Nim
import macros

macro removeVar(name: expr): stmt =
  result = quote do:
    var `name` {.discardable.}
    `name` = default(typeof(`name`))

var x = 5

block:
  removeVar(x)
  # x not available here

echo x  # x available here, output: 5

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-40">Listing 40:</d> example of deleting variable from scope in Nim </em>
</div>

### Scala

Scala supports metaprogramming using macros and annotations, allowing you to create your own compiler annotations.

<div id="listing-41"></div>

```Scala
import scala.annotation.StaticAnnotation
import scala.language.experimental.macros
import scala.reflect.macros.blackbox

class removeVar extends StaticAnnotation {
  def macroTransform(annottees: Any*): Any = macro RemoveVarMacro.impl
}

object RemoveVarMacro {
  def impl(c: blackbox.Context)(annottees: c.Expr[Any]*): c.Expr[Any] = {
    import c.universe._
    val result = annottees.map(_.tree).toList match {
      case q"var $name: $tpe = $expr" :: body =>
        val updatedBody = body.map {
          case q"if (true) $expr2" =>
            q"""
              if (true) {
                var $name: $tpe = null.asInstanceOf[$tpe]
                $expr2
              }
            """
          case other => other
        }
        q"var $name: $tpe = $expr; ..$updatedBody"
    }
    c.Expr[Any](q"..$result")
  }
}

@removeVar
var x: Int = 5

if (true) {
  // x is not available here
}

println(x)  // x available here, output: 5

```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-41">Listing 41:</d> example of deleting variable from scope in Scala </em>
</div>

## Possible extensions
There are several ideas related to expanding existing ways of working with scopes.

### ability to delete variables from scope
We didn't find any requests to add this feature to kotlin, but some specific languages have this feature (you can find examples above).

### ```let``` scope function with multiple arguments

There is also exist an idea to add ```let``` with the ability to declare multiple variables. This looks like a good solution for the problems described [here](#listing-13).


1. Code Cleanliness: Reduces nesting and improves code readability by reducing the number of nested ```let``` blocks.
2. Template Code Reduction: Reduces repetitive code checks to ```null```.
3. Improved Reliability: Reduces the likelihood of errors due to misuse of nullable variables.

#### Possible syntax

<div id="listing-42"></div>

```kotlin
multilet (a, b, c) { nonNullA, nonNullB, nonNullC ->
// Code executed if a, b and c are not null
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-42">Listing 42:</d> possible syntax for multilet in Kotlin </em>
</div>

#### Possible usage 

1. Checking Multiple Input Sources

<div id="listing-43"></div>

```kotlin
multilet (nameField.text, emailField.text, passwordField.text) { name, email, password ->
    validateAndSubmit(name, email, password)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-43">Listing 43:</d> possible usage of multilet in Kotlin </em>
</div>

### ```with``` scope function with multiple arguments

There are [requests](https://discuss.kotlinlang.org/t/using-with-function-with-multiple-receivers/2062) to add the ability to use multiple variables in a scope function. 

<div id="listing-44"></div>

```kotlin
with(args, activity) {
    putString(stringKey, “String”)
    putInt(intKey, 12345)
    putChar(charKey, ‘c’)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-44">Listing 44:</d> possible syntax of <code>with</code> with multiple variables in Kotlin </em>
</div>


<div id="listing-45"></div>

```kotlin
with(args) {
    with(activity) {
        putString(stringKey, “String”)
        putInt(intKey, 12345)
        putChar(charKey, ‘c’)
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-45">Listing 45:</d> equiavalent of <code>with</code> with multiple variables in Kotlin </em>
</div>

After checking with BigCode it turned out that 252622 of 81170612 files (0.31%) contain two nested ```with```.

2277 out of 81170612 files (~0.00%) contain three or more nested ```with```.

Also we were able to find a [custom implementation of this feature](https://discuss.kotlinlang.org/t/multiple-scope-with-function/27429).

In the end it looks like a good idea to add this feature to kotlin, but on the other hand I can't say that adding this feature will improve the existing code much.

### Nullability and scopes smartcasts

We also considered the idea of adding the ability to pass information that a variable is definitely not ```null``` to the body of the function where the variable will be called.  So that using this information the compiler could avoid compiling parts of the function code related to checking this variable for ```null```.

<div id="listing-46"></div>

```kotlin
if(val x = fun(); x!=null){
    fun1(x)
}

fun1(value : Int?){

    if(value == null){
        println("no")
    }else{
        //only println("yes") will be compiled
        println("yes")
    }
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-46">Listing 46:</d> example of a case where the previously described feature would be useful </em>
</div>

But considering the available tools, adding such a feature would slow down the compiler very much, so we don't think it is expedient.

### Local scopes

While talking about scopes, the idea of being able to import modules locally like in ```OCaml``` and ```Haskell``` also came up.
This has some uscases, let's look at them.

**1. Avoiding Name Conflicts:** 
When working with libraries that contain classes or functions with the same names, local imports can help avoid name conflicts. 

<div id="listing-47"></div>

```kotlin
fun process() 
    run {
        import com.example.package1.Helper
        val helper1 = Helper()
        helper1.doSomething()
    }

    run {
        import com.example.package2.Helper
        val helper2 = Helper()
        helper2.doSomethingElse()
    }

```


<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-47">Listing 47:</d> example of avoiding name conflict using local imports</em>
</div>

**2. Restricting Import Scope:** 
Local imports can restrict the visibility of imported modules to a specific block of code, helping to prevent the accidental use of imported elements outside of that block.

<div id="listing-48"></div>

```kotlin
fun performAction() {
    run {
        import com.example.utils.ActionUtil
        ActionUtil.performSpecificAction()
    }
    // ActionUtil is not accessible here
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-48">Listing 48:</d> example of restricting import scope using local imports</em>
</div>

**3. Managing Dependencies:**
You can locally import dependencies needed only for a specific test method.
This makes it easier to understand the dependencies of each test and prevents accidental use of unnecessary dependencies.

<div id="listing-49"></div>

```kotlin
@Test
fun testMathOperations() {
    // Local import for testing
    import org.junit.jupiter.api.Assertions.assertEquals
    assertEquals(4, 2 + 2)
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-49">Listing 49:</d> example of managing dependencies using local imports</em>
</div>

As you can see this has some usecases, despite this we could not find any queries regarding this feature on the kotlin forums. 

### Scopes with controlflow statements

We propose a ```scope``` block where variables can be declared, followed by controlflow statement that utilize these variables within its condition. This approach aims to provide a clear separation of variable initialization and condition evaluation, enhancing code readability and maintainability.

#### Proposed syntax

<div id="listing-50"></div>

```kotlin
scope {
    val x = someCalculation()
    val y = anotherCalculation(x)
} if (x > 10 && y < 20) {
    // Block to execute
}
```


<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-50">Listing 50:</d> example of proposed syntax</em>
</div>


#### Advantages of ```scope``` block
1. **Enhanced Readability and Structure:**

- Clear Separation: By separating variable declarations from the condition, the code becomes easier to read and understand. The scope block clearly indicates where variables are initialized, and the if statement focuses solely on the conditional logic.

- Organized Code: This structure promotes organized and modular code, making it easier to follow the flow of logic.

2. **Improved Maintainability:**

- Easier Modifications: Changes to variable initialization or the condition can be made independently, reducing the risk of introducing errors. This modular approach makes the codebase easier to maintain and update.
- Scalability: As the complexity of variable initialization grows, the scope block can accommodate these changes without cluttering the control flow statement.
3. **Error Handling:**

- Isolated Initialization: Any exceptions or errors that occur during variable initialization can be handled within the scope block, keeping the 
if statement clean and focused on its primary purpose.

4. **Consistent Flow Control:**

- Scoped Variables: Variables declared within the scope block are only accessible within the subsequent if statement, preventing unintended side effects and ensuring that the variables are not used outside their intended context.

#### Disadvatages of ```scope``` block

1. **Increased Verbosity:**

- **Additional Syntax:** Introducing a scope block adds extra syntax, which might be seen as verbose for simple cases. This could potentially make the code look more complicated than necessary for straightforward conditions.

2. **Overhead for Simple Conditions:**

- **Simple Use Cases:** For simple conditions where only one or two variables need to be checked, this syntax might add unnecessary complexity. In such cases, the traditional method might be more appropriate.

### Using ```where``` Clauses for Variable Initialization in Kotlin

We also considered an idea to add ```where``` block similar to ```where``` block in Haskell. 

<div id="listing-51"></div>

```kotlin
if (x > 10 && y < 20) where {
    val x = someCalculation()
    val y = anotherCalculation(x)
} {
    // Block to execute
}
```

<div style="text-align: center; margin-top: 5px;">
    <em><d name="listing-51">Listing 51:</d> example of proposed syntax</em>
</div>

#### Advantages of ```where``` block

1. **Improved Readability:** Clearly delineates where variables are initialized and how they are used, enhancing code readability.
2. **Scoped Initialization:** Keeps variable scope tightly controlled, minimizing the risk of variable misuse outside the intended context.
3. **Reduced Boilerplate:** Combines variable initialization and conditional logic, reducing the need for separate initialization blocks.

#### Disadvantages of ```where``` block
1. **Syntax Complexity:** Introducing a new keyword and syntax structure could increase the complexity of the language, making it harder for beginners to learn.

