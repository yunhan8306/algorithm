# 문법 정리

## Collection
### groupBy
- Array, collection을 Map 으로 매핑함
- 리턴타입 : Map<T, K>
  
```kotlin
public inline fun <T, K> Iterable<T>.groupBy(keySelector: (T) -> K): Map<K, List<T>> {
    return groupByTo(LinkedHashMap<K, MutableList<T>>(), keySelector)
}
val list = listOf<T>()
val group: Map<T, List<T> > = list.groupBy { it }
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
