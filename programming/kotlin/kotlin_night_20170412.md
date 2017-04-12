## Kotlin STD

### kotlin

#### let

```kotlin
user?.let {
  println("${it.id}: ${it.name}")
}
```
어디에 쓸까? 굳이 null check 하는데 쓰기는..


github.com/importre/kotlin-unwrap

if 쓰지 않고 여러 변수 null check

#### apply

```kotlin
Observable.blabla
  .subscribe { }
  .apply { disposables.add(this) }

arguments = Bundle().appy {
  putInt("part", part)
}
```

#### also

apply 와는 달리 scope 변경 없음.

#### with

scope 변경

#### run

apply + with

block scope 느낌으로도 씀.

run {
  var a;
}

run {
  var a;
}

#### takeif / takeUnless

조건에 따라 null or value

#### Array - contentDeepEquals

deep value compare

Retrofit 반환으로 List 를 쓰는 이유.
(list 는 항상 value compare vs array 는 reference compare)


### kotlin.system

#### measureNanoTime/ measureTimeMillis

measureNanoTime {
  
}


### kotlin.collections(eager) / sequences(lazy)

### associate

val m1 = users.associate { it.id to it } # pair 로 만들어줌
var m2 = users.associateBy(User::id) # 동일


### kotlin.jvm

@file:JvmName("Utils")
@file:JvmMultifileClass

extention 등이 어떤 package 로 들어가게 할지 정할 수 있다.

@JvmOverloads

java 에는 parameter 에 default value 가 없기 때문에.
