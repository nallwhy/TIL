### 2017-03-16

#### Implements **Composition over Inheritance** by `delegates by`

http://kiranrao.in/blog/2017/03/05/kotlin-coi/

```kotlin
open class ForwardingMutableSet<E>(s: MutableSet<E>): MutableSet<E> by s
```
