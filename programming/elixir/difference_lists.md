## Difference Lists of Elixir

이해한대로 정리해보자면

linked list 의 뒤에 계속해서 append 해나가다 보면 앞에서부터 계속해서 순차 검색을 해야하기 때문에 O(n)의 복잡도를 가진다.

그래서 elixir 에서는 (따져보면 prolog 부터) list 의 앞쪽에 추가하는 것을 권장한다.

하지만 그것만으로는 원하는 동작을 다 할 수 없는 경우가 많다.

```elixir
iex) list = [1, 2]
[1, 2]

iex) new_list = [3 | list]
[3, 1, 2]
```

그래서 만들어진 개념이 Difference Lists!

다른 언어에서의 구현이 어떻게 되어있는지는 모르겠지만 개념을 따지고 보자면 이런 것이다

```elixir
[a, b, c]
.(a, .(b, .(c, [])))
```

즉, 연산을 끝마치지 않고 뒤쪽에 뭔가 들어올 수 있는 공간을 만들어 두고서 계속해서 붙여나간 후 마지막에 뒤에서부터 prepend 를 쭉 해오는 방식.

당연히 연산 단위로 다 저장해놓고 나중에 연산을 때리기 때문에 기존 list 의 prepend 연산에 비해서는 밀리지만, list 가 커졌을 때 append 연산은 훨씬 빠르다.

아래는 difflist 의 benchmark.
[1..10000] 까지 누적해서 append 실행.

```
benchmark name           iterations   average time
regular list prepend          10000   115.79 µs/op
difflist append                1000   2304.42 µs/op
reverse list append              10   169003.40 µs/op
regular list append              10   184620.70 µs/op
```

Reference:  
https://github.com/sotojuan/difflist  
https://en.wikibooks.org/wiki/Prolog/Difference_Lists  
http://stackoverflow.com/questions/26966055/understanding-difference-lists
