# Naming
## Package Statement
- すべて小文字で連続する単語をそのまま繋げる。

```kotlin
// GOOD
package jp.eure.android.pairs.domain.usecase

// BAD
package jp.eure.android.pairs.domain.useCase
package jp.eure.android.pairs.domain.use_case
```

## Class, Object, Interface, Enum
- Upper camel caseで命名する。

```kotlin
// GOOD
class MyClass

// BAD
class myClass
```

### Enum Constants
- Upper snake caseで命名する。

```kotlin
// GOOD
enum class MyEnum {
    MY_VALUE,
    YOUR_VALUE
}

// BAD
enum class MyEnum {
    MyValue,
    YourValue
}
```

## Functions
- Lower camel caseで命名する。

```kotlin
// GOOD
fun doSomething()

// BAD
fun DoSomething()
```

## Properties and Variables
- Lower camel caseで命名する。

```kotlin
// GOOD
val myVal = 0

// BAD
val MyVal = 0
```
- companion object内の定数はUpper snake caseで命名する。

```kotlin
// GOOD
companion object {
    val MY_VALUE = 0
}

// BAD
companion object {
    val myValue = 0
}
```

- prefixをつけない。

```kotlin
// GOOD
class MyClass {
    companion object {
        var num = 0
    }
    val string = "foo"
}

// BAD
class MyClass {
    companion object {
        var sNum = 0
    }
    val mString = "foo"
}
```

## Resorces
- リソースのファイル名、idはLower snake caseで命名する。

# Format
`.idea/codeStyleSettings.xml`の設定に従う。以下に自動整形できないルールに関して記述する。

## Class, Data class, Object, Interface, Enum
- 1ファイルに複数のトップレベルclass等を宣言しない。

## Companion Object
- companion objectはclass宣言直下に記述する。
- companion objectのpropertyや関数をJavaからも利用する可能性がある場合には`@JvmStatic`をつける。可能であれば`const`キーワードでも良い。

## Functions
- overload functionは集約する。

### Higher-Order Functions
- lambda式を用いる場合、`()`を省略出来る場合には省略する。

```kotlin
// GOOD
list.filter { it % 2 == 0 }
Array(5) { it.toString() }

// BAD
list.filter({ it % 2 == 0 })
Array(5, { it.toString() })
```

- 複数の式から成り立つラムダ式では 単引数暗黙名`it`を使用しない

```kotlin
// GOOD
list.forEach { num ->
    foo(num)
    bar(num)
}

// BAD
list.forEach {
    foo(it)
    bar(it)
}
```

## Properties
- propertyの順序は何らかの合理的な順序で並べる。
- propertyは合理的なまとまりで集約し、まとまりごとに1行空ける。

```kotlin
// GOOD
lateinit var flagFoo: Boolean
lateinit var flagBar: Boolean

lateinit var viewFoo: View
lateinit var viewBar: View

// BAD
lateinit var flagFoo: Boolean
lateinit var viewFoo: View
lateinit var flagVar: Boolean
lateinit var viewBar: View

```

- propertyは可能であれば型推論を利用する。ただし、型を明示したい場合はこの限りではない。
- propertyはJavaからfieldとして利用する必要がある場合には`@JvmField`annotationをつける。

## Break
- 行の途中で改行を行う場合は演算子の直前で行う。
- constructor, function宣言で改行を行う場合は、引数の`,`の直後に行う。

## Braces
- 中括弧`{}`の前後にクラスや関数、関数呼び出し、キーワードがある場合にはスペースを1つ置く。
```kotlin
// GOOD
class MyClass {
	fun doSomething(list: List<Int>) {
		list.forEach { /*do something*/ }
	}
}

// BAD
class MyClass{
	fun doSomething(list: List<Int>){
		list.forEach{/*do something*/}
	}
}
```
- 開始中括弧`{`の前に改行を入れない。
- 開始中括弧`{`の後に改行を入れる。
- 終了中括弧`}`の前に改行を入れる。
- 終了中括弧`}`が文や式、関数の本体を終えるならばその中括弧の後に改行を入れる。終了中括弧の後に`else` 等が続く場合は改行をしない。

```kotlin
// GOOD
class MyClass {
    fun doSomething() {
        if (isFoo) {

        } else {

        }
    }
}

// BAD
class MyClass
{
    fun doSomething()
    {
        if (isFoo)
        {

        }
        else {

        }
    }
}
```

### If expressions
- 1行に収まるのであれば、中括弧`{}`を省略して1行で記述してもよい。

```kotlin
// GOOD
val thing = if (isFoo) doSomething() else doAnotherThing()

// BAD
val thing = if(longBooleanValue) somethingLongLongFunction() else somethingLongLongLongFunction()
```

### Lambda expressions
- 1行に収まるのであれば、中括弧`{}`前後の改行はしなくてもよい。

```kotlin
// GOOD
list.forEach { doSomething(it) }

// NOT GOOD
list.forEach {
    doSomething(it)
}
```
