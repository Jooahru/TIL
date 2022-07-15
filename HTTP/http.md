# Http

## IP 인터넷 프로토콜
 * 지정한 IP 주소에 데이터 전달
 * 패킷이라는 통신 단위로 데이터 전달

## IP 프로토콜의 한계
* 비연결성 - 패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송
* 비신뢰성 - 패킷이 순서대로 안오는경우, 중간에 손실나는 경우
* 프로그램 구분 - 같은 IP를 사용하는 서버에서 통신하는 애플리케이션이 여러개이면?

## 인터넷 프로토콜 스택의 4계층
* 애플리케이션 계층 - HTTP,FTP
* 전송계층 - TCP, UDP
  * TCP 특징
    * 연결지향 - TCP 3way handshake (syn => syn+ack => ack)
    * 데이터 전달 보증
    * 순서보장
    * 현재 대부분 TCP 사용
  * UDP 특징(사용자 데이터그램 프로토콜)
    * 연결지향 X 데이터전달 보증 X 순서보장 X
    * 단순하고 빠름
    * IP와 거의 같지만 port ,체크섬 정도 추가 어플리케이션에서 추가 작업 필요
* 인터넷계층 - IP
* 네트워크 인터페이스 계층

## PORT
* 0~65535 할당 가능
* 0~1023: 잘 알려진 포트, 사용하지 않는 것이 좋음
* FTP - 20,21 TELNET -23 HTTP -80 HTTPS -443

## DNS (도메인 네임 시스템)
* 예) google.com

## HTTP
 * 클라이언트 서버 구조
   * Request,Response 구조
 * Stateless (무상태 프로토콜)
   * 서버가 클라이언트의 상태를 보존X
   * 장점 서버 확장성 높음
   * 단점 클라이언트가 추가 데이터 전송해줘야함
 * 비연결성
   * HTTP는 기본이 연결을 유지하지 않는 모델
   * 서버 자원을 효율적으로 사용 가능
   * TCP/IP 연결을 계속 새로 맺어야하는 단점이 있음
   * HTTP 지속연결(Persisten Connections)로 문제 해결
 * HTTP메시지

## HTTP 메서드
* API URI는 리소스를 URI에 매핑 (/member)로해서 get,post,put,delete...
* GET:리소스 조회
* POST:요청 데이터 처리, 주로 등록
* PUT:리소스를 대체, 해당 리소스가 없으면 생성
  * POST와 차이점은 PUT은 리소스 위치를 알고 URI 지정
  * ex) PUT /member/{id}
* PATCH: 리소스 부분 변경
  * PUT과 차이점은 PUT은 하나만 바꿔도 전체가 다 바뀐다.
  * EX)PUT : name,age를 가진 객체에 age만 바꾸면 name초기화된다
  *    patch: name,age를 가진 객체에 age만 바꾸면 age만 바뀐다
* DELETE: 리소스 삭제

## HTTP 메서드 속성
* 안전(Safe Methods)
  *  호출해도 리소스를 변경하지 않는다
* 멱등(Idempotent Methods)
  * 한번 호출하든 두번 호출하든 100번 호출하든 결과가 똑같다.
  * GET,PUT,DELETE /// POST(결제)는 아님
  * 자동 복구 메커니즘에 활용
* 캐시가능(Cacheable Methods)
  * 주로 GET,정도만 캐시로 사용