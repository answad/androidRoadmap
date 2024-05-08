# BroadCast Receiver

- BroadCast Receiver는 publish-subscribe디자인 페턴을 따른다
    - 이 디자인 페턴은
        - Publisher과 Subscriber로 나눠서 Publisher는 메시지를 발행하고
        - Subscriber는 Publisher의 관심 있는 이벤트 또는 메시지 유형에 대해 구독해서 메시지를 받는다
- 안드로이드 OS로부터 발생하는 각종 이벤트와 정보를 받아와 핸들링한다
- 안드로이드 시스템이나 다른 앱으로부터 전송되는 브로드캐스트 메시지를 수신하는 구성 요소
    - 예시로 배터리 부족 경고, 시간 변경, 화면 켜짐/꺼짐 등의 이벤트가 있다