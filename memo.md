# 문법 정리

## Collection
### groupBy
- Array, collection을 Map 으로 매핑함
- 리턴타입 : Map<T, K>
  
```kotlin
public inline fun <T, K> Iterable<T>.groupBy(keySelector: (T) -> K): Map<K, List<T>> {
    return groupByTo(LinkedHashMap<K, MutableList<T>>(), keySelector)
}
```

### sortedBy, sortedByDescending
- Array, collection을 정렬함
- 람다 반환은 Int
```kotlin
public inline fun <T, R : Comparable<R>> Iterable<T>.sortedBy(crossinline selector: (T) -> R?): List<T>

public inline fun <T, R : Comparable<R>> Iterable<T>.sortedByDescending(crossinline selector: (T) -> R?): List<T>
```

### sumOf
- Array, collection을 숫자로 매핑한 뒤 합을 반환
- 리턴 타입 : Int
```kotlin
public inline fun <T : Any> Iterable<T>.sumOf(selector: (T) -> Int): Int
```

### fold
- Array, collection을 순차적으로 연산함
- 초기값을 설정 할 수 있고, 타입 유동적, 람다 반환은 이전값, 현재값
- 리턴타입 : 람다 마지막
```kotlin
public inline fun <T, R> Iterable<T>.fold(initial: R, operation: (acc: R, T) -> R): R
```

### foldIndexed
- Array, collection을 순차적으로 연산함
- 초기값을 설정 할 수 있고, 타입 유동적, 인덱스 제공, 람다 반환은 인덱스, 이전값, 현재값
- 리턴타입 : 람다 마지막
```kotlin
public inline fun <T, R> Iterable<T>.foldIndexed(initial: R, operation: (index: Int, acc: R, T) -> R): R
```

### reduce
- Array, collection을 순차적으로 연산함
- 초기값을 설정할 수 없고, 타입 제한적, 람다 반환은 이전값, 현재값
- 리턴타입 : T
```kotlin
public inline fun <T> Iterable<T>.reduce(operation: (acc: T, T) -> T): T
```

### maxBy, maxByOrNull
- Array, collection 중 최대 값 반환
- 리턴타입 : T?
```kotlin
@Deprecated
public inline fun <T, R : Comparable<R>> Iterable<T>.maxBy(selector: (T) -> R): T

public inline fun <T, R : Comparable<R>> Iterable<T>.maxByOrNull(selector: (T) -> R): T?

```

### flatMap
- 2중 Array, Collection을 단일 리스트로 평탄화 ( 내부는 Iterable<R> -> 람다 내부는 Iterable<R> )
- 리턴타입 : List<R>
```kotlin
public inline fun <T, R> Iterable<T>.flatMap(transform: (T) -> Iterable<R>): List<R>
```


## Map
### keys
- Map의 key를 Set 으로 매핑함
- 리턴타입 : MutableSet<K>
  
```kotlin
val hash = hashMapOf<K, V>()
val keys: MutableSet<K> = hash.keys
```


### values
- Map의 value를 MutableCollection 으로 매핑함
- 리턴타입 : MutableCollection<V>
  
```kotlin
val hash = hashMapOf<K, V>()
val values: MutableCollection<V> = hash.values
```
