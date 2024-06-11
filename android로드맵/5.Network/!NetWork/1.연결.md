# 연결

- 우선 android 에서 인터넷을 사용 하려면 manifest 에

```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

- 인터넷 사용 권한을 추가 해야 한다
- 이 권한들은 일반 권한이고 설치시 허가된다

# 통신

- 안드로이드는 보통 http 프로토콜을 이용하여 통신한다
- 기본적으로 통신에는 Http(s)URLConnection 를 사용하고
- 실재로 클라이언트가 보는 라이브러리는 Retrofit이다
- Retrofit은
    - OkHttp를 포함하고 OkHttp는
        - 를 포함한다 HttpURLConnection
- Retrofit -> OkHttp -> HttpsURLConnection 순으로 호출이 이루어진다
- 이 구조덕분에 클라이언트가 좀더 간단한 코드로 통신을 구현 할 수 있다

### 동작 방식

- Retrofit은 API 인터페이스와 호출 방법을 정의하고, 네트워크 요청을 OkHttp으로 실행한다
- OkHttp는 Retrofit의 요청을 받아 네트워크 연결을 설정하고, HttpsURLConnection으로 데이터를 주고받는다
- HttpsURLConnection은 OkHttp에 의해 사용되어 실제 네트워크 연결과 데이터 전송을 수행한다

# 안드로이드에서 사용하는 통신 라이브러리(?)

### Retrofit:

- 고수준의 REST API 클라이언트 라이브러리로, 네트워크 요청을 쉽게 관리하고 데이터 변환을 처리한다
- OkHttp를 기본 HTTP 클라이언트로 사용한다

### OkHttp:

- 저수준의 HTTP 클라이언트 라이브러리로, 네트워크 연결, 요청 및 응답을 효율적으로 관리한다
- HttpURLConnection 또는 HttpsURLConnection을 사용하여 실제 HTTP 통신을 수행한다

### HttpsURLConnection:

- 자바 표준 라이브러리로 제공되는 HTTP(S) 통신 클래스이다
- 네트워크 연결을 관리하고, HTTP(S) 요청 및 응답을 처리한다

