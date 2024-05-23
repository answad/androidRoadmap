# Shared Preferences

- 데이터를 키-값 쌍으로 저장하는 안드로이드 API

# 특징

- 안드로이드의 Shared Preferences는 데이터를 키-값 쌍으로 저장하는 데 사용된다
    - 이는 작은 key-value 형태의 데이터베이스(Ex - Redis)와 유사하게 작동하고
- 보통 설정이나 애플리케이션 상태를 저장한다
- Android의 파일 시스템에 XML 파일 형식으로 저장된다
    - 위치 -> /data/data/[패키지 이름]/shared_prefs/[파일 이름].xml
- 데이터는 일반적으로 대량의 데이터를 저장하는 데 사용되지 않는다
    - 이유
        - 성능 저하: xml 파일 전체를 메모리에 로드 하기 때문에 메모리적인 성능 저하가 발생한다
        - 동시 접근 불가 : 여러 스레드나 프로세스에서 동시에 액세스하거나 수정하는 경우에 데이터 일관성을 유지하기 어려울 수 있다
        - 읽기/쓰기 성능이 뛰어나지 않으며, 특히 데이터 양이 많을 경우 성능 저하가 발생한다

# 사용 예시

```kotlin
// SharedPreferences의 이름 상수
private const val PREFS_NAME = "MyPrefs"

// SharedPreferences 키 상수
private const val KEY_USERNAME = "username"
```

```kotlin
val prefs: SharedPreferences = context.getSharedPreferences(PREFS_NAME, Context.MODE_PRIVATE)
```

- 위 코드는 SharedPreferences 객체를 생성하고, PREFS_NAME("MyPrefs") 라는 이름의 SharedPreferences 파일을 가져온다
- 이 파일은 해당 애플리케이션 내에서만 접근할 수 있도록 "MODE_PRIVATE" 모드로 열립니다.

```kotlin
val editor: SharedPreferences.Editor = prefs.edit()
```

- SharedPreferences 파일을 수정하기 위해 SharedPreferences.Editor 객체를 생성한다
- SharedPreferences.Editor 는 SharedPreferences에 key-value 쌍을 삽입하고 수정한다

```kotlin
editor.putString(KEY_USERNAME, "JohnDoe")
editor.apply() // 또는 editor.commit()
```

- apply,commit 을 이용해서
    - 실제로 입력하고 적용할 수 있다
- 둘의 차이점은 
  - apply는 비동기적으로 디스크(xml파일) 에 쓰고
  - commitdms 동기적으로 쓴다

```kotlin
// SharedPreferences에서 사용자 이름을 가져오는 코드
val savedUsername = prefs.getString(KEY_USERNAME, "")
```
- ""는 key에 해당하는 key-value쌍이 없을때 받아올 기본값을 지정하는 것이다