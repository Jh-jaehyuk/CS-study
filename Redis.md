# Redis

## 📍 Redis란 무엇인가?
#### ✔️ Redis는 Remote(원격)에 위치하고 프로세스로 존재하는 In-Memory기반의 Dictionary(key-value)구조 데이터 관리 server 시스템이다.
<br>

## 📍  Dictionary(key-value)구조 데이터란 무엇인가?
#### ✔️ Dictionary(key-value)구조 데이터란, MySQL 같은 관계형 데이터가 아닌 비관계형 구조로서 데이터를 그저 ‘키-값’형태로 단순하게 저장하는 구조를 말한다. 그래서 일종의 NoSQL로 분류되기도 한다. (MongoDB와 같은 형태)
![key-value](https://github.com/user-attachments/assets/fba52372-ba31-4a50-8a4b-5f08fb2b5731)
<br>

## 📍 Redis의 주요 특징
#### ✔️ 메모리 기반 데이터 저장소라 모든 데이터들을 메모리에 저장하고 조회한다. 때문에 속도가 매우 빠르다.

##### &emsp; ↳메모리에 데이터를 저장하기 때문에 저장 공간에 제약이 있어, 주로 보조 데이터 저장소로 사용한다.

#### ✔️ 메모리에 상주하면서 서비스의 상황에 따라 DB로 사용될 수 있으며, Cache로도 사용될 수 있다.(Redis의 특징 이해 - 1 참고)

#### ✔️ 영속성 - 메모리의 데이터는 휘발성이지만 Redis는 메모리 기반이지만 영속적인 데이터 보존(Persistence)이 가능하다.  (Redis의 특징 이해 - 2 참고)

#### ✔️ 원자성 - 여러 프로세스에서 동시에 같은 key에 대한 갱신을 요청하는 경우, 데이터 부정합 방지 Atomic처리 함수를 제공한다. (Redis의 특징 이해 - 3 참고)
<br>

## 📍 Redis의 특징 이해 - 1
#### ✔️ Cache란 한 번 조회된 데이터를 미리 특정 공간에 저장해놓고, 똑같은 요청이 발생하게 되면 서버에게 다시 요청하지 않고 저장해놓은 데이터를 제공하여 빠르게 서비스를 제공하는 것을 의미한다.

#### ✔️ Redis Cache의 구조 패턴은 Look aside Cache패턴과 Write Back패턴이 존재한다.

#### ✔️ Look aside Cache패턴 - 위에서 언급한 일반적인 캐시 정의를 그대로 구현한 구조이다. 캐시에 한 번 접근하여 데이터가 있는지 판단한 후, 있다면 캐시의 데이터를 사용하고 없다면 실제 DB에 있는 데이터를 사용한다.

##### &emsp; -Look aside Cache패턴의 진행 순서-
![LookasideCache패턴순서](https://github.com/user-attachments/assets/a4c5f8f3-0282-4c77-9362-e7fba112cecc)
![LookasideCache패턴그림](https://github.com/user-attachments/assets/feb89f38-17d9-401d-b8e9-0baceec72b3a)
![LookasideCache패턴그림2](https://github.com/user-attachments/assets/e052015f-29cd-4036-b75c-335d40e51608)
<br>

## 📍 Redis의 특징 이해 - 2
#### ✔️ Redis에서 대표적인 영속적 데이터 보존 방식에는 RDB와 AOF가 있다.

#### ✔️ RDB - 특정 시점의 Redis data를 나타내는 여러 개의 데이터 파일(스냅샷)을 생성하는 방식이다.
![RDB그림](https://github.com/user-attachments/assets/98299328-ff76-448c-8ec2-5c78fa543ac8)

##### &emsp; ↳ 스냅샷이란 데이터의 영구 저장을 위해 메모리에 저장된 모든 데이터를 디스크 저장하는 기능 기능으로 메모리 내용을 *.rdb파일로 저장하여 해당 시점으로 복구할 수 있다.
![RDB그림2](https://github.com/user-attachments/assets/9f1b396a-5b10-4b18-9068-efe268d8707d)
##### &emsp; ↳  쉽게 생각하여 특정 시점의 Redis백업 기능이라고 생각하면 된다.
##### &emsp; ↳ 리눅스의 fork()함수에 의해 동작한다.

#### ✔️ AOF -입력, 수정 삭제의 명령을 실행할 때마다 log 파일에 저장한다. 해당 로그 파일은 append-only모드로 쓰여진다. Redis가 다시 시작되면 AOF 로그에 저장된 명령을 재실행하여 기존 데이터를 복구한다.
![AOF](https://github.com/user-attachments/assets/a63232eb-c049-434e-b0af-02b0934f2cc0)
<br>

## 📍 Redis의 특징 이해 - 3
#### ✔️ 서로 다른 Redis 클라이언트에서 기능을 수행하기 위해 한번에 여러 명령을 보낸다면 각 클라이언트의 여러 명령이 뒤섞여 실행되며, 이로 인해 경합이 발생하고, 예상치 못한 문제가 발생할 수 있다. 이를 방지하기 위해 크게 Transaction과 Lua Script 기능을 사용할  수 있다.
##### &emsp; ↳ Transaction와 Lua Script(https://hudi.blog/redis-atomicity/)
<br>

## 📍 Redis의 장점
#### ✔️ Redis는 관계형 데이터베이스가 아니기 때문에 쿼리 연산을 지원하지 않지만, 대신 데이터의 고속 읽기와 쓰기에 최적화 되어 있다. 

#### ✔️ NoSQL 형식의 데이터베이스는 단순 검색 및 추가 작업에 있어서 매우 최적화된 키-값 저장 기법을 사용하여 응답 속도나 처리 효율 등에 있어서 매우 뛰어난 성능을 보여준다.

#### ✔️ Redis는 In-Memory 솔루션으로 분류되기도 하는데, 다양한 데이터 구조체를 지원함으로써 DB, Cache, Message Queue, Shared Memory 등의 용도로 사용할 수 있다.
##### &emsp; ↳일반 데이터베이스 같이 디스크(ssd)에 데이터를 쓰는 구조가 아니라 메모리(dram)에서 데이터를 처리하기 때문에 작업 속도가 상당히 빠르다.
![In-memory](https://github.com/user-attachments/assets/322ae033-199c-4ebe-b486-c9f4a2d3d02f)
#### ✔️ Redis는 Java, Python, PHP, C, C++, C#, Ruby등을 비롯한 많은 프로그래밍 언어 프레임워크에 대한 API를 폭넓게 지원한다는 장점도 있다.
<br>

## 📍 Redis의 단점
#### ✔️ Redis는 Java script와 같이 싱글 스레드 기반으로 동작한다. 그래서 한 번에 하나의 명령만 실행하기 때문에 긴 처리 시간이 필요한 명령에는 불리하다.
#### ✔️ 메모리 파편화 - Redis는 메모리를 할당 받고 해제하는 과정에서 부분부분 빈 공간이 생기게 되는데 그로 인해 메모리에 낭비가 발생하게 된다.
![Memory](https://github.com/user-attachments/assets/61e60e0c-10e3-4cae-ad87-490d7db5d5f7)
<br>

## 📍 Redis 탄생 비화
#### ✔️ 이탈리아의 Salvatore Sanfilippo라는 해커가 MySQL로 어플을 개발하다가 너무 느려서 화딱지가 나서 직접 빠른 서버를 만들어봐야겠다고 생각했고, 그 결과 개발된 것이 Redis라는 비하인드 스토리가 있다.