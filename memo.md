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

### fold
- Array, collection을 순차적으로 연산함
- 초기값을 설정 할 수 있고, 람다 반환은 이전값, 현재값
- 리턴타입 : 람다 마지막
```kotlin
public inline fun <T, R> Iterable<T>.fold(initial: R, operation: (acc: R, T) -> R): R {
    var accumulator = initial
    for (element in this) accumulator = operation(accumulator, element)
    return accumulator
}
```

### reduce
- Array, collection을 순차적으로 연산함
- 초기값을 설정할 수 없고, 타입 제한적, 람다 반환은 이전값, 현재값
- 리턴타입 : T
```kotlin
public inline fun <T> Iterable<T>.reduce(operation: (acc: T, T) -> T): T
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
