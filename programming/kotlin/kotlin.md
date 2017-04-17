### 2017-04-17

#### Kotlin all your tests

https://speakerdeck.com/dpreussler/kotlin-all-your-tests-codefest-dot-ru-2017


### 2017-04-13

#### kotlin-unwrap

https://github.com/importre/kotlin-unwrap

```kotlin
val _a = foo("Hello")
val _b = foo("World")
val _c = foo(null)

// example: error handing
unwrap(_a, _b, _c) { a, b, c ->
    println("$a, $b$c") // not invoked
} otherwise {
    println("Nah!")     // invoked because `_c` is null
}
```


### 2017-04-12

#### Kodein

https://github.com/SalomonBrys/Kodein

Kodein is a very simple and yet very useful dependency retrieval container.


### 2017-03-29

#### Your first Node.js app with Kotlin

https://medium.com/@Miqubel/your-first-node-js-app-with-kotlin-30e07baa0bf7

You can use Kotlin to build Node.js application.


### 2017-03-16

#### Implements **Composition over Inheritance** by `delegates by`

http://kiranrao.in/blog/2017/03/05/kotlin-coi/

```kotlin
open class ForwardingMutableSet<E>(s: MutableSet<E>): MutableSet<E> by s
```
