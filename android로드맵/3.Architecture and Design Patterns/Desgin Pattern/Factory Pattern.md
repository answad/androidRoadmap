# Factory Pattern

- 객체 생성을 캡슐화하여 클라이언트 코드로부터 분리하는 디자인 패턴
    - 이 패턴은 객체를 생성하기 위한 인터페이스를 제공하고
        - 어떤 객체를 가져오는지 불러오는 클래스에서 정할수 있게 한다
- 다른말로
    - 슈퍼클래스에서 객체를 생성하는 인터페이스를 제공하면서
    - 서브클래스가 생성될 객체의 유형을 변경할 수 있도록 한다
- 팩토리 패턴은 객체를 만들어내는 공장(Factory 객체)을 만드는 패턴
- 이 패턴은 클라이언트 코드와 구체적인 객체 사이에 추상화 계층을 도입한다
- 팩토리 메서드는 하나의 공통 슈퍼 클래스를 공유하는 여러 가능한 클래스 중 하나에서 클래스의 인스턴스를 생성하고자 할 때 사용한다

# 특징

- 객체를 생성하는 로직을 분리시켜서
    - 단일책임원칙을 지킬수 있다
- 새로운 객체를 만들어야할때 변경이 줄어든다
- 테스트하기 쉽다

```kt
// 도형을 나타내는 추상 클래스
abstract class Shape {
    abstract fun draw()
}

// 원 클래스
class Circle : Shape() {
    override fun draw() {
        println("Circle.draw() 호출")
    }
}

// 사각형 클래스
class Rectangle : Shape() {
    override fun draw() {
        println("Rectangle.draw() 호출")
    }
}
```

```kt
// 도형을 생성하는 팩토리 클래스
class ShapeFactory {
    // 도형을 생성하는 팩토리 메서드
    fun createShape(type: String): Shape {
        return when (type.toLowerCase()) {
            "circle" -> Circle()
            "rectangle" -> Rectangle()
            else -> throw IllegalArgumentException("지원되지 않는 도형 타입: $type")
        }
    }
}
```

```kt
fun main() {
    val factory = ShapeFactory()

    // 원 객체 생성
    val circle = factory.createShape("circle")
    circle.draw()

    // 사각형 객체 생성
    val rectangle = factory.createShape("rectangle")
    rectangle.draw()
}
```