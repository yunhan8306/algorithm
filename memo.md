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

### sortedWith
- Array, collection을 Comparator 로 정렬 후 새로운 리스트 반환함
- 인스턴스는 Comparator
```kotlin
fun <T> Iterable<T>.sortedWith(comparator: Comparator<in T>): List<T>
```

### Comparator
- 두 객체를 비교하는 로직을 정의하는 인터페이스
- 음수 : 오름차순 / 양수 : 내림차순
```kotlin
interface Comparator<in T> { fun compare(o1: T, o2: T): Int }
// sortedWith와 사용할 때
array.sortedWith(
    Comparator { num1, num2 -> num1 - num2 }
)
```

### compareTo
- 두 객체를 비교하여 정렬 순서를 나타내는 정수값(Int)을 반환하는 함수
- 음수 : 오름차순 / 양수 : 내림차순
```kotlin
interface Comparable<in T> {
    operator fun compareTo(other: T): Int
}
```

### sumOf
- Array, collection을 숫자로 매핑한 뒤 합을 반환
- 리턴 타입 : Int
```kotlin
public inline fun <T : Any> Iterable<T>.sumOf(selector: (T) -> Int): Int
```

### slice
- Array, collection을 인덱스 범위 원소만 추출하여 새로운 List 반환
- 인덱스 범위는 모두 포함
- 원본과 독립적
- 리턴 타입 : 
```kotlin
public fun <T> List<T>.slice(indices: IntRange): List<T>

public fun <T> Array<out T>.slice(indices: IntRange): List<T> {
```

### joinToString
- Array, collection의 요소들을 구분자(separator)로 이어붙여서 단일 문자열로 만듬
- 일반적인 경우 separator만 지정해서 사용
- 리턴타입 : String
```kotlin
fun <T> Iterable<T>.joinToString(
    separator: CharSequence = ", ",
    prefix: CharSequence = "",
    postfix: CharSequence = "",
    limit: Int = -1,
    truncated: CharSequence = "...",
    transform: ((T) -> CharSequence)? = null
): String
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

### flatten
- 2중 Array, Collection을 단일 리스트로 평탄화 ( 2중 구조가 같은 자료구조여야함 )
- 리턴타입 : List<R>
```kotlin
public fun <T> Iterable<Iterable<T>>.flatten(): List<T>

public fun <T> Array<out Array<out T>>.flatten(): List<T>
```

### ifEmpty
- Array, collection이 empty 인 경우 대체 값 반환

```kotlin
fun <C : Collection<T>, T> C.ifEmpty(defaultValue: () -> C): C
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

### entires
- Map의 key-value 쌍을 Map.Entry 형태로 set으로 매핑함
- Map.Entry<K, V> 은 한 쌍의 key-value만 포함
- 리턴타입 : Set<Map.Entry<K, V>>

```kotlin
val hash = hashMapOf<K, V>()
val entries: MutableSet<Map.Entry<K, V>> = hash.entries
```


## String
### trimStart
- 앞부분 문자열 제거
- 인스턴스 없으면 공백 제거

```kotlin
fun String.trimStart(vararg chars: Char): String

fun String.trimStart(): String
```

### ifEmpty
- 문자열이 empty 인 경우 대체 값 반환

```kotlin
fun String.ifEmpty(defaultValue: () -> String): String
```

## Number
### Math.ceil
- 소수점 올림
- 리턴 타입 : Double

```kotlin
fun ceil(x: Double): Double
// 사용 시
Math.ceil(5.5) = 6.0
```

### Math.floor
- 소수점 내림
- 리턴 타입 : Double
  
```kotlin
fun floor(x: Double): Double
// 사용 시
Math.floor(5.5) = 5.0
```

### Math.sqrt
- 제곱근
- 리턴 타입 : Double
  
```kotlin
fun sqrt(x: Double): Double
// 사용 시
Math.sqrt(9.0) = 3.0
```

### Math.pow
- 거듭제곱 반환
- 리턴 타입: Double

```kotlin
fun pow(base: Double, exponent: Double): Double
// 사용 시
Math.pow(5.0, 2.0) = 25.0
```

### Math.abs
- 절댓값 반환
- 리턴 타입: Int, Long, Float, Double

```kotlin
fun abs(x: T): T
// 사용 시
Math.abs(-5) = 5
Math.abs(-5.5) = 5.5
```
