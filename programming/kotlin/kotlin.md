### 2017-05-09

#### Unit tests on Android with Kotlin

https://antonioleiva.com/unit-tests-android-kotlin/


### 2017-05-08

#### Kapsule

https://github.com/traversals/kapsule  
https://blog.gouline.net/kapsule-minimalist-dependency-injection-for-kotlin-ed3e344d60ed

Minimalist dependency injection library for Kotlin

#### How to remove all !! from your Kotlin code

https://medium.com/@david.vavra/how-to-remove-all-from-your-kotlin-code-87dc2c9767fb

Use build-in functions requireNotNull or checkNotNull with accompanied exception message for easy debugging.

```kotlin
uploadPhoto(requireNotNull(intent.getStringExtra("PHOTO_URL"), { "Activity parameter 'PHOTO_URL' is missing" }))
```

#### KUnidirectional

https://speakerdeck.com/cesarvaliente/unidirectional-data-flow-on-android-using-kotlin

https://github.com/CesarValiente/KUnidirectional

Unidirectional data flow architecture on Android using Kotlin.

#### How to mock final classes on Kotlin using Mockito 2

https://antonioleiva.com/mockito-2-kotlin/

`test/resources/mockito-extensions/org.mockito.plugins.MockMaker`
```
mock-maker-inline
```

#### Tail recursion and how to use it in Kotlin

https://medium.com/@JorgeCastilloPr/tail-recursion-and-how-to-use-it-in-kotlin-97353993e17f


### 2017-05-02

#### Kotlin Dependency Injection with the Reader Monad

https://medium.com/@JorgeCastilloPr/kotlin-dependency-injection-with-the-reader-monad-7d52f94a482e

https://github.com/JorgeCastilloPrz/KotlinAndroidArchitecture

#### Kodein

https://github.com/SalomonBrys/Kodein


### 2017-04-28

#### Kotlin 1.1 is also for Android Developers

https://blog.jetbrains.com/kotlin/2017/04/kotlin-1-1-is-also-for-android-developers/

* Type aliases
* Inheritance of data classes
* Destructuring inside lambdas
* Local delegated properties
* Using underscore to ignore unused vriables on lambdas
* Coroutines
* @JvmOverloads


### 2017-04-18

#### JUnit 5: Kotlin

https://blog.stylingandroid.com/junit-5-kotlin


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
