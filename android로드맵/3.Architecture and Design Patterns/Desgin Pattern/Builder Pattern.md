# Builder Pattern

- 복잡한 객체를 점진적으로 구성하는 데 사용되는 패턴

# 구조

- 빌더 클래스의 메서드호출을 연결하여 호출해서 자연스럽게 인스턴스를 구성하고
    - build() 메서드로 객체를 생성한다

```kt
class Product private constructor(
    val attribute1: String,
    val attribute2: Int,
    val attribute3: Boolean
) {
    // Builder 클래스
    class Builder {
        private var attribute1: String = ""
        private var attribute2: Int = 0
        private var attribute3: Boolean = false

        fun setAttribute1(value: String): Builder {
            this.attribute1 = value // Builder클래스 안의 변수들의 값을 변경한다 
            return this
        }

        fun setAttribute2(value: Int): Builder {
            this.attribute2 = value
            return this
        }

        fun setAttribute3(value: Boolean): Builder {
            this.attribute3 = value
            return this
        }

        fun build(): Product {
            return Product(attribute1, attribute2, attribute3) // 객체 생성 
        }
    }

    override fun toString(): String {
        return "Product(attribute1='$attribute1', attribute2=$attribute2, attribute3=$attribute3)"
    }
}

// 사용
fun main() {
    val product = Product.Builder()
        .setAttribute1("Attribute 1")
        .setAttribute2(42)
        .setAttribute3(true)
        .build()

    println(product)
}
```

- 여기서 main()의 product는 간단하게

```
val product = Product(attribute1 = "Attribute 1", attribute2 = 42, attribute3 = true)
```

- 으로 나타낼 수 있다
- 그럼 왜 더 복잡해지도록 Build Pattern을 사용 하는지가 궁금해질 수 있다

# 장점 

- 유효성 검사 보장: 
  - 빌더 패턴을 사용하면 객체 생성 과정에서 유효성 검사를 보장할 수 있다
    - 각 단계에서 필요한 매개변수를 설정하므로, 필수적인 값이 빠지거나 유효하지 않은 값이 전달되는 것을 방지할 수 있다
- 객체 생성과 초기화 과정의 복잡성 해결: 
  - 객체 생성 및 초기화 과정이 복잡할 때, 빌더 패턴은 이러한 복잡성을 해결할 수 있다
    - 각 단계별로 필요한 매개변수를 설정하므로, 생성자에서 처리해야 할 매개변수의 개수가 많을 때 더욱 좋다
- 원랜 더 많은 장점이 있었는데 kotlin을 사용하면 해결 되는 것이 많다
  - 기본값 지정, 매개변수를 명시적 으로 입력 등이 있다