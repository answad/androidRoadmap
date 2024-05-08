# Intent란

- 안드로이드의 4대컴포넌트끼리의 통신을 맡은것
- 다른 애플리케이션과 통신할때도 사용한다

# 사용 예시

- 화면(Activity)시작: 화면 간 이동이나 액티비티의 시작
    - 예시로 다른 액티비티를 시작하거나 다른 앱의 액티비티를 시작할 때 Intent를 사용할 수 있다
- 서비스 시작: 백그라운드 작업을 처리하기 위해 서비스를 시작하는 데 사용됨
    - 예시로 애플리케이션의 서비스를 시작하거나 시스템 서비스를 시작할 때 Intent를 사용할수 있다
- 브로드캐스트 전송: 다른 애플리케이션 또는 시스템에 브로드캐스트 메시지를 보내는 데 사용됨

# 각 예시가 작동하는 과정

### Activity 시작

- Intent를 startActivity()에
    - startActivity(Intent)형식으로 전달하여
- 새로운 Activity 인스턴스를 생성한다
    - Intent는 기본적으로 시작할 Activity를 설명하는 데이터를 가지고 다른 필요한 데이터를 가지고 있다
- startActivityForResult()으로 Activity를 시작하면 액티비티의 startActivityForResult콜백으로 인해서
    - Intent객체로 결과를 전달한다

### Service 시작

```md
Service는 사용자 인터페이스 없이 백그라운드에서 작업을 실행하는 구성요소입니다. Android 5.0 (API 수준 21) 이상에서는 JobScheduler로 서비스를 시작할
수 있습니다.
JobScheduler에 관한 자세한 내용은 API-reference documentation를 참조하세요.
Android 5.0 (API 수준 21) 이전 버전의 경우 Service 클래스의 메서드를 사용하여 서비스를 시작할 수 있습니다.
Intent를 startService()에 전달하여 일회성 작업(예: 파일 다운로드)을 실행하기 위해 서비스를 시작할 수 있습니다.
Intent는 시작할 서비스를 설명하고 필요한 데이터를 전달합니다.
서비스가 클라이언트-서버 인터페이스로 설계된 경우 Intent를 bindService()에 전달하여 다른 구성요소의 서비스에 바인딩할 수 있습니다.
```

### 브로드캐스트 전송

- sendBroadcast() 또는 sendOrderedBroadcast()에 Intent를 전달해서 다른 앱에 브로드캐스트를 전달할 수 있다

# Intent의 종류

- Intent는 명시적(Intent를 받을 대상이 명확한 경우)
    - 명시적 Intent는 대상 컴포넌트의 이름이나 액션을 지정하여 특정 구성 요소에 직접 전달된다
        - 인텐트에 클래스 객체나 **ComponentName** 을 지정하여 호출할 대상을 확실히 알 수 있는 경우에 사용한다
            - 주로 애플리케이션 내부에서 사용한다
- 암시적(Intent를 받을 대상이 여러 개일 때)이 있다
    - 암시적 Intent는 액션, 데이터 유형 및 기타 속성을 지정하여 시스템에서 해당 Intent를 처리할 수 있는 구성 요소를 찾도록 요청합니다
        - 호출할 대상이 달라질 수 있는 경우에는 암시적 인텐트를 사용한다
            - 인텐트는 실행할 작업에대한 정보만 가진다
                - 주로 안드로이드 시스템에 특정 작업을 처리해달라고 요청할때 사용
- 암시적 인텐트를 사용하면
    - 시스템이 모든앱의 Intent Filter를 검색하는데
        - 인텐트 필터(Intent filter)는 안드로이드 애플리케이션에서 컴포넌트가 특정한 인텐트를 처리할 수 있는지 여부를 지정하는 데 사용되는 요소이고
          Manifest파일에 정의된다

### 예시

![스크린샷 2024-05-07 오후 8.47.26.png](..%2F..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2F38%2Fkvylqg593kzbfrl92wb5532w0000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_aYqCvf%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-05-07%20%EC%98%A4%ED%9B%84%208.47.26.png)

# Intent에 포함된 정보

1. 구성요소 이름(Component name)
2. 작업(Action)
3. 데이터(Data)
4. Category
5. 추가 항목
6. Flags

### 구성요소 이름

- 필수는 아니지만 명시적인 Intent를 사용하기위해 꼭 필요하다
    - 없으면 암시적인 Intent이다
- setComponent(), setClass(), setClassName() 또는 Intent 생성자를 사용하여 구성요소 이름을 설정할 수 있다

### 작업

- 실행할 작업을 지정하는 문자열이다
    - 보통 Intent 클래스나 다른 프레임워크 클래스에서 정의한 작업 상수를 사용한다
- 예시

```
ACTION_VIEW: 주어진 데이터를 보여주기 위한 액션입니다. 주로 웹 페이지, 이미지, 텍스트, 비디오 등을 보여주는 데 사용됩니다.
ACTION_EDIT: 주어진 데이터를 편집하기 위한 액션입니다. 주로 텍스트 편집기, 이미지 편집기 등과 함께 사용됩니다.
ACTION_SEND: 데이터를 다른 앱에 보내기 위한 액션입니다. 주로 공유 기능에 사용됩니다.
ACTION_CALL: 전화를 걸기 위한 액션입니다. 이 액션은 전화 번호를 지정하는 데 사용됩니다.
ACTION_DIAL: 전화 다이얼러를 열기 위한 액션입니다. 전화 번호를 입력하는 창이 나타납니다.
ACTION_PICK: 데이터를 선택하기 위한 액션입니다. 예를 들어, 연락처에서 연락처를 선택하거나 이미지 갤러리에서 이미지를 선택하는 데 사용됩니다.
ACTION_SENDTO: 특정한 수신자에게 데이터를 보내기 위한 액션입니다. 예를 들어, 이메일 앱에서 특정 이메일 주소로 이메일을 보내는 데 사용됩니다.
```

- setAction() 또는 Intent 생성자를 사용하여 인텐트의 작업을 지정할 수 있다

### 데이터

- 작업할 데이터의 MIME을 참조하는 URL(Uri)객체
    - MIME유형과 URL(Uri)를 둘다 지정해야한다
        - MIME(Multipurpose Internet Mail Extensions)는 인터넷에서 여러 종류의 데이터를 표현하고 전송하기 위한 방법을 정의하는 인터넷
          표준
- 데이터 URI를 설정하려면 setData()를 사용한다
- MIME 유형을 설정하려면 setType()을 사용한다 필요한 경우 setDataAndType()를 사용하여 두 가지를 모두 명시적으로 설정할 수 있다

```markdown
**주의**: URI와 MIME 유형을 모두 설정하려면 setData()와 setType()를 호출하면 안 된다
이 두 메서드는 서로의 값을 무효화하기 때문이다
URI와 MIME 유형을 모두 설정하려면 항상 setDataAndType()을 사용해라
```

### 카테고리

- 구성요소의 종류에 관한 추가 정보가 포함된 문자열
    - 하나의 인텐트에 여러개의 카테고리를 넣을수 있지만 대부분의 인텐트에서 필요로 하지 않는다
- 예시

```markdown
DEFAULT: 일반적인 동작을 나타내는 기본 카테고리
BROWSABLE: 브라우저 앱과 관련된 카테고리
LAUNCHER: 런처 액티비티를 나타내는 카테고리
EDIT: 편집 액티비티와 관련된 카테고리
```

### 추가 항목

- 요청된 작업을 처리하는데 필요한 정보가 포함된 key-value쌍

### 플래그

- Intent의 동작을 변경하거나 제어하는 데 사용

# 명시적 인텐트 예시

```kotlin
// 이 코드는 Activity 안에 있어서, 그래서 'this' 는 Context 이다
// The fileUrl is a string URL, such as "http://www.example.com/image.png"
val downloadIntent = Intent(this, DownloadService::class.java).apply {
    data = Uri.parse(fileUrl)
}
startService(downloadIntent)
```

# 암시적 인텐트 예시

```kotlin
val sendIntent = Intent().apply {
    action = Intent.ACTION_SEND
    putExtra(Intent.EXTRA_TEXT, textMessage)
    type = "text/plain"
}

// Intent 사용 시도
try {
    startActivity(sendIntent)
} catch (e: ActivityNotFoundException) {
    //  Exception 처리 코드
}
```

- 암시적인 인텐트를 startActivity에 주입하면
    - 시스템은 모든 앱의 인텐트 필터를 검사 하여 Intent를 처리할 수 있는 애플리케이션을 실행한다
        - 가능한 애플리케이션이 하나인경우 바로 실행하지만
        - 여러개면
![스크린샷 2024-05-07 오후 8.47.26.png](..%2F..%2F..%2F..%2F..%2F..%2F..%2Fvar%2Ffolders%2F38%2Fkvylqg593kzbfrl92wb5532w0000gn%2FT%2FTemporaryItems%2FNSIRD_screencaptureui_aYqCvf%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202024-05-07%20%EC%98%A4%ED%9B%84%208.47.26.png)
- 이런창이 떠서 애플리케이션을 선택하도록 한다 

# 인텐트 필터 예시

```xml
<activity android:name="MainActivity" android:exported="true">
    <!-- 이 액티비티는 메인 진입점으로 설정된다 -->
    <intent-filter>
        <!-- 이 액티비티는 메인 진입점으로 설정된다 -->
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
    </intent-filter>
</activity>

<activity android:name="ShareActivity" android:exported="false">
    <!-- 이 액티비티는 "SEND" 작업과 텍스트 데이터를 처리합니다 -->
    <intent-filter>
        <action android:name="android.intent.action.SEND"/>
        <category android:name="android.intent.category.DEFAULT"/>
        <!-- 이 액티비티가 text/plain MIME 타입 데이터를 처리할 수 있도록 지정합니다 -->
        <data android:mimeType="text/plain"/>
    </intent-filter>
    <!-- 이 액티비티는 미디어 데이터와 함께 "SEND"와 "SEND_MULTIPLE" 작업도 처리합니다 -->
    <intent-filter>
        <!-- 이 액티비티가 "SEND"와 "SEND_MULTIPLE" 작업을 처리할 수 있도록 지정합니다 -->
        <action android:name="android.intent.action.SEND"/>
        <action android:name="android.intent.action.SEND_MULTIPLE"/>
        <!-- 이 액티비티가 임의의 데이터를 처리할 수 있도록 지정합니다 -->
        <category android:name="android.intent.category.DEFAULT"/>
        <!-- 이 액티비티가 특정 MIME 타입의 미디어 데이터를 처리할 수 있도록 지정합니다 -->
        <data android:mimeType="application/vnd.google.panorama360+jpg"/>
        <data android:mimeType="image/*"/>
        <data android:mimeType="video/*"/>
    </intent-filter>
</activity>

```