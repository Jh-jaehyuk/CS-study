# 네트워크 통신 방식

## Unicast
- **정의**: 특정 대상과 1:1로 통신하는 방식. 각각의 컴퓨터끼리 통신하는 형태.
- **예시**: 우리가 현재 사용하는 클라이언트와 서버 간의 통신 방식.
<img src="https://github.com/user-attachments/assets/c50c5600-ba98-4139-822b-abf659511602" alt="unicast" width="500">

## Multicast
- **정의**: 1 : 다수의 형식으로 통신하는 방식. 하나의 컴퓨터가 여러 사람에게 데이터를 전송하는 형태.
- **예시**: 인터넷 방송, 스포츠 중계.
<img src="https://github.com/user-attachments/assets/6e983813-3048-433d-9230-a5a628926f65" alt="multicast" width="500">

## Broadcast
- **정의**: 네트워크 상의 모든 네트워크 장비와 통신하는 방식. 중앙 장비가 네트워크에 연결된 모든 장비에게 데이터를 전송.
- **특징**: 수신자가 데이터를 거부할 수 없음.
<img src="https://github.com/user-attachments/assets/49b9a78a-3f43-42c5-ae4c-58a9b602f7f0" alt="broadcast" width="500">

## Anycast
- **정의**: 네트워크에서 수신이 가능한 장비 중 가장 가까운 장비에게 데이터를 전송하는 방식. IPv6 기반으로 작동.
- **목적**: 
  - 클라이언트와 서버 간의 물리적 거리를 줄여 응답 시간을 최소화.
  - DDoS 공격 시 여러 서버에게 분산되므로 Unicast에 비해 피해가 줄어듦.
  - 다수의 서버가 존재하여 특정 서버가 장애를 겪더라도 다른 서버와 통신 가능.


<img src="https://github.com/user-attachments/assets/0b8d283d-be57-4e4a-9f74-a7a56037513c" alt="예시사진" width="500">

- **사용 예시**: Google의 DNS 서버 위치.

<img src="https://github.com/user-attachments/assets/30f27e64-5a2e-4ea7-8e04-85ba0cfa8e0c" alt="anycast" width="500">

[Google 클라우드 위치](https://cloud.google.com/about/locations/?hl=ko)

# 네트워크 프로토콜

## Protocol이란?
- **정의**: 네트워크 통신 시 데이터를 주고받는 형식과 규칙을 정한 것.
- **종류**:
  - **Ethernet Protocol**: MAC 주소 기반의 근거리 통신.
  - **ICMP (Internet Control Message Protocol)**: 오류 메시지 전송을 위한 프로토콜.
    - **DDoS 공격에 사용**: 서버에 계속 오류 메시지를 보내서 서버가 ICMP 응답에 집중하도록 만듦.
  - **ARP (Address Resolution Protocol)**: 네트워크 주소(IP)를 물리적 주소(MAC)로 대응시키는 프로토콜.

<img src="https://github.com/user-attachments/assets/c5642bce-02f3-4f18-90df-488ed6aa9113" alt="물리적 주소" width="500">

## HTTP (Hypertext Transfer Protocol)
- **정의**: 문서 전송을 위한 프로토콜. Request와 Response로 동작.

### Request 구성
1. **Request Line**: 요청 방식 (공백) URI (공백) HTTP Version
   - **요청 방식**: 대표적으로 GET, POST 등이 있음.
2. **Headers**: 요청 관련 메타데이터. Dictionary 구조.
   - **공통 항목**:
     - `Date`: HTTP 요청 생성 시간.
     - `Connection`: 연결 관리 방식 (예: `close`, `keep-alive`).
   - [자세한 Header 목록](https://gmlwjd9405.github.io/2019/01/28/http-header-types.html)


3. **Body**: 요청 데이터. 이미지, JavaScript 등 다양한 데이터가 들어갈 수 있음.

### URI와 URL의 차이점
- **URI (Uniform Resource Identifier)**: 인터넷에 있는 특정 자원을 나타내는 주소.
  - **특징**: 값은 유일하지만, 응답은 달라질 수 있음.
  - **예시**: `http://localhost:8080/account/login`에서 `/account/login` 부분.
- **URL (Uniform Resource Locator)**: URI를 포함하며, 네트워크 주소와 포트 번호 등을 포함한 모든 주소를 뜻함.

### Response 구성
1. **Status Line**: HTTP Version (공백) Status Code (공백) Reason Phrase
2. **Headers**: 응답 관련 메타데이터.
3. **Body**: 응답 데이터. 요청에 대한 결과가 포함됨.

## HTTP Status Code
- **100~199**: 단순 정보.
- **200~299**: 요청 성공.
- **300~399**: 요청이 수행되지 않아 다른 URL로 재지정.
- **400~499**: 요청이 불완전하거나 오류가 있음.
- **500~599**: 서버 문제로 메시지 처리가 불가능한 상황.

[자세한 Status Code 목록](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status#server_error_responses)
