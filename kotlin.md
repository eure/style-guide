# Naming
## Case defined
1. 言葉を素のASCIIに変換し、アポストロフィを除く。 (e.g. `Müller’s algorithm` -> `Muellers algorithm`)
1. スペースや残っている句読点で分離し、単語に分割する。
1. すべての単語を小文字にする。
1. すべての単語をcaseに合わせて連結する。

### Lower camel case
最初の単語を除いて全ての単語の頭文字を大文字にして連結する。

| Prose form | Correct | Incorrect |
|:-:|:-:|:-:|
| XML HTTP request | xmlHttpRequest | XMLHTTPRequest |
| new customer ID | newCustomerId | newCustomerID |
| supports IPv6 on iOS| supportsIpv6OnIos | supportsIPv6OnIOS |

### Upper camel Case
全ての単語の頭文字を大文字にして連結する。

| Prose form | Correct | Incorrect |
|:-:|:-:|:-:|
| XML HTTP request | XmlHttpRequest | XMLHTTPRequest |
| new customer ID | NewCustomerId | NewCustomerID |
| supports IPv6 on iOS| SupportsIpv6OnIos | SupportsIPv6OnIOS |

### Lower snake Case
全ての単語を`_`で連結する。

| Prose form | Correct | Incorrect |
|:-:|:-:|:-:|
| XML HTTP request | xml_http_request | XML_HTTP_request  |
| new customer ID | new_customer_id | new_customer_ID |
| supports IPv6 on iOS| supports_ipv6_on_ios | supports_IPv6_on_iOS |

### Upper snake Case
全ての単語の頭文字を大文字にして`_`で連結する。

| Prose form | Correct | Incorrect |
|:-:|:-:|:-:|
| XML HTTP request | XML_HTTP_REQUEST |  |
| new customer ID | NEW_CUSTOMER_ID |  |
| supports IPv6 on iOS| SUPPORTS_IPV6_ON_IOS | SUPPORTS_IPv6_ON_iOS |

## File
- ktファイル名はclass名と同一にする。

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
## Package Statement
- package文は改行しない。

## Import Statements
- import文は改行しない。
- ワイルドカードimportは使わない。

## Class, Data class, Object, Interface, Enum
- 1ファイルに複数のトップレベルclass等を宣言しない。

### Class, Data class
- primary constructorの直前は改行しない。

```kotlin
// GOOD
class MyClass constructor(...)

// BAD
class MyClass
constructor(...)
```

## Companion Object
- companion objectはclass宣言直下に記述する。
- companion objectのpropertyや関数をJavaからも利用する可能性がある場合には`@JvmStatic`をつける。可能であれば`const`キーワードでも良い。

## Annotations
- primary constructorへのannotationは直前につける。

```kotlin
// GOOD
class MyClass @Annotation constructor(...)

// BAD
class MyClass
@Annotation
constructor(...)
```

- secondary constructorへのannotationは直上につける。
- propertyへのannotationは直上につける。
- 関数へのannotationは直上につける。

```kotlin
// GOOD
class MyClass {

    @Annotation
    val property = "property"

    @Annotation
    constructor(...) {

    }

    @Annotation
    fun function() = "function"
}

// BAD
class MyClass {

    @Annotation val property = "property"

    @Annotation constructor(...) {

    }

    @Annotation fun function = "function"
}
```

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

- propertyは可能なであれば型推論を利用する。ただし、型を明示したい場合はこの限りではない。
- propertyはJavaからfieldとして利用する必要がある場合には`@JvmField`annotationをつける。

## Block Indentation
- ブロックのインデントにはスペース4つを使う。
- 演算子直前の改行はスペース8つでインデントする。

```kotlin
// GOOD
val result
        = someLongExpression(foo, bar, fizz, buzz)

// BAD
val result
    = someLongExpression(foo, bar, fizz, buzz)
```

- constructor, functionの引数宣言で改行を行う場合、第一引数の後に改行し第二引数以降はIntelliJ(Android Studio)に従って第一引数にアラインする。

```kotlin
// GOOD
class MyClass constructor(foo: Foo,
                          bar: Bar,
                          fizz: Fizz,
                          buzz: Buzz)

// BAD
class MyClass constructor(foo: Foo,
        bar: Bar,
        fizz: Fizz,
        buzz: Buzz)
```

## Spaces
- `,`, `:`,`?:`の直後にはスペースを置く。
- `+`, `-`, `*`, `/`, `%`の前後にはスペースを置く。
- `{}`の前後になにか他の記述がある場合にはスペースを置く。

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
- 単式で構成され、カラムリミットを超えないのであれば、中括弧`{}`を省略して1行で記述してもよい。

```kotlin
// GOOD
val thing = if (isFoo) doSomething() else doAnotherThing()

// BAD
val thing = if(longBooleanValue) somethingLongLongFunction() else somethingLongLongLongFunction()
```

### Lambda expressions
- 単式で構成され、カラムリミットを超えないのであれば、中括弧`{}`前後の改行はしなくてもよい。

```kotlin
// GOOD
list.forEach { doSomething(it) }

// NOT GOOD
list.forEach {
    doSomething(it)
}
```
