## Kotlin Functors, Applicatives, And Monads in Pictures

https://hackernoon.com/kotlin-functors-applicatives-and-monads-in-pictures-part-1-3-c47a1b1ce251


Get different result depending on the `context`. This is the idea that Functors, Applicatives, Monads, Arrows etc are all based on.

```kotlin
sealed class Option<out A> {
  object None : Option<Nothing>()
  data class Some<out A>(val value: A) : Option<A>()
}
```

### Functors

When a value is wrapped in a context, you can’t apply a normal function to it. This is where `map` comes in. `map` knows how to apply functions to values that are wrapped in a context.

```kotlin
fun sumThree(n: Int) = n + 3

Option.Some(2).map(::sumThree)
// => Some(5)
```
But how does map know how to apply the function?

```kotlin
seled class Option<out A> {
  ...

  inline fun <B> map(f: (A) -> B): Option<B> = when (this) {
      is None -> this
      is Some -> Some(f(value))
  }
}
```

```kotlin
val option: Option<Int> = someCallThatMightReturnNone()
option.map { it + 3 }
// => None
```

Here’s how you work with a database record in a language without `Option`.

```kotlin
let post = Post.findByID(1)
if post != nil {
  return post.title
} else {
  return nil
}
```

But in Kotlin using the `Option` functor:

```kotlin
findPost(1).map(::getPostTitle)
```

Arrays are functors too!

*Basically Kotlin provides an extension function to all iterables in the form:

```kotlin
inline fun <T, R> Iterable<T>.map(transform: (T) -> R): List<R> {..}
```

What happens when you apply a function to another function?

```kotlin
{ a: Int -> a + 2 } map { a: Int -> a + 3 }
// => ???
```

The result is just another function!

```kotlin
typealias IntFunction = (Int) -> Int

infix fun IntFunction.map(g: IntFunction): IntFunction {
    return { x -> this(g(x)) }
}

val foo = { a: Int -> a + 2 } map { a: Int -> a + 3 }
foo(10)
// => 15
```

### Applicatives

Applicatives take it to the next level. With an applicative, our values are wrapped in a context, just like Functors, but our functions are wrapped in a context too!

Yeah. Let that sink in. Applicatives don’t kid around. Unlike Haskell, Kotlin doesn’t have yet a built-in way to deal with Applicatives. But it is very easy to add one! We can define an apply function for every type supporting Applicative, which knows how to apply a function wrapped in the context of the type to a value wrapped in the same context:

```kotlin
infix fun <A, B> Option<(A) -> B>.apply(f: Option<A>): Option<B> =
        when (this) {
            is Option.None -> Option.None
            is Option.Some -> f.map(this.value)
        }
infix inline fun <A, reified B> Array<(A) -> B>.apply(a: Array<A>) =
        Array(this.size * a.size) {
            this[it / a.size](a[it % a.size])
        }
```

If both `this` and the function are `Some`, then the function is applied to the unwrapped option, otherwise `None` is returned.

For the `Array` I'm using its constructor parameters to generate the array, although note that this wouldn't be the most performant choice for bigger arrays.

```kotlin
Some({ a: Int -> a + 3 }) apply Some(2)
// => Some(5)
```

So, following our previous explanation, using apply can lead to some interesting situations. For example:

```kotlin
arrayOf<(Int) -> Int>({ it + 3 }, { it * 2 }) apply arrayOf(1, 2, 3)
// => [ 4, 5, 6, 2, 4, 6 ]
```

### Monads

Functors apply a function to a wrapped value.

Applicatives apply a wrapped function to a wrapped value.

Monads apply a function that returns a wrapped value to a wrapped value. Monads have a function `flatMap` to do this.

```kotlin
inline fun <B> flatMap(f: (A) -> Option<B>): Option<B> = 
when (this) {
    is None -> this
    is Some -> f(value)
}
```

Suppose half is a function that only works on even numbers:

```kotlin
fun half(a: Int) = when {
    a % 2 == 0 -> Some(a / 2)
    else -> None
}
```

What if we feed it a wrapped value?

We need to use `flatMap` to shove our wrapped value into the function.

```kotlin
Some(3).flatMap(::half)
// None
Some(4).flatMap(::half)
// Some(2)
Some(2).flatMap(::half)
// None
```

### Conclusion

1. A functor is a type that implements `map`.
2. An applicative is a type that implements `apply`.
3. A monad is a type that implements `flatMap`.
4. `Option` implements `map` and `flatMap`, plus we can extend it to implement `apply`, so it is a functor, an applicative, and a monad.

Playground: https://github.com/aballano/FAM-Playground

Original version of Haskel: http://adit.io/posts/2013-04-17-functors,_applicatives,_and_monads_in_pictures.html
