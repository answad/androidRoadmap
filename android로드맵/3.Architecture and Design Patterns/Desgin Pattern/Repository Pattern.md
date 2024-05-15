# Repository Pattern

- 소프트웨어 디자인 패턴 중 하나
  - 데이터에 접근하는코드를 코드를 묶어서 추상화하여 애플리케이션의 비즈니스 로직과 데이터 소스 간의 결합을 줄인다
    - 예시로 백엔드와 통신하는코드, room에 접근하는코드등이 있다
- 한마디로 데이터에 접근하는부분을 인터페이스로 추상화해서 사용하는것이다

# 특징

- 비지니스로직과 데이터 접근, 변환 로직을 분리할수 있다

# 예시코드

```kt
data class User(val id: Int, val name: String, val email: String)

// 데이터소스 인터페이스
interface UserDataSource {
    fun getUserById(userId: Int): User?
    fun getUserByEmail(email: String): User?
    fun saveUser(user: User)
}

// 데이터소스 구현
class UserDataSourceImpl : UserDataSource {
    private val users = mutableListOf<User>()

    override fun getUserById(userId: Int): User? {
        return users.find { it.id == userId }
    }

    override fun getUserByEmail(email: String): User? {
        return users.find { it.email == email }
    }

    override fun saveUser(user: User) {
        users.add(user)
    }
}

// 레포지토리
class UserRepository(private val userDataSource: UserDataSource) {
    fun getUserById(userId: Int): User? {
        return userDataSource.getUserById(userId)
    }

    fun getUserByEmail(email: String): User? {
        return userDataSource.getUserByEmail(email)
    }

    fun saveUser(user: User) {
        userDataSource.saveUser(user)
    }
}

// 테스트 코드
fun main() {
    // UserDataSource 인스턴스 생성
    val userDataSource = UserDataSourceImpl()

    // UserRepository 인스턴스 생성
    val userRepository = UserRepository(userDataSource)

    // 새로운 사용자 추가
    val newUser = User(1, "John Doe", "john@example.com")
    userRepository.saveUser(newUser)

    // 이메일을 기반으로 사용자 검색
    val userByEmail = userRepository.getUserByEmail("john@example.com")
    println("User found by email: $userByEmail")

    // 사용자 ID를 기반으로 사용자 검색
    val userById = userRepository.getUserById(1)
    println("User found by ID: $userById")
}
```

- 이런식으로 데이터에 접근하는 코드를 분리해서 사용할수 있다