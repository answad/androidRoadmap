# Dependency Injection

- 의존성 주입 
- 객체 인스턴스 의 생성을 사용 하는곳 에서 직접 하지 않고 (다른 곳에서 만들어 져서) 필요한 곳에 전달 되도록 코드를 조직화 하는 기법
    - 객체 인스턴스 를 사용 하는 곳을 클라이언트 라고 부름
    - 여기서 의존성(dependency): 사용 되는 객체의 인스턴스
    - 클라이언트가 아닌 잘 조직화 된 곳에서 일관성 있는 형태로 객체 생성 방법을 정의함

# 왜 의존성 주입을 사용해야 하는가

### 코드를 재사용 가능하게 한다

- 클라이언트의 코드 변경 없이도 쉽게 다른 결과를 만들 수 있다
- 객체의 생성 과정이 바뀌더라도 클라이언트 코드에 영향을 주지 않음

```kt
val prodNewsRemoteDataSource = NewsRemoteDataSource(ProdNewsApi())
val devNewsRemoteDataSource = NewsRemoteDataSource(DevNewsApi())
```

### 클라이언트는 interface 로만 객체를 알고 있으면 되니까 좀더 추상적 으로 코드를 설계 할수 있음

### 코드를 테스트 가능 하게 한다 객체의 생성 방법을 설정에 따라 다르게 할 수 있음

- 코드를 테스트 용으로 간단 하게 전환 가능
- 테스트 용 DataSource 만들기

```kt
 val fakeDataSource = NewsRemoteDataSource(TestApi())
```

# Injector 클래스

- Injector 클래스 는 주입 되는 모든 타입들 을 위한 생성 방법을 정의함
- 의존성 을 주입 할수 있는 방법을 정의 한다

```kt
class ProdInjector {
    fun getNewsApi(): NewsApi = ProdNewsApi()
    fun getNewsRemoteDataSource(): NewsRemoteDataSource = NewsRemoteDataSource(getNewsApi())
}
```
