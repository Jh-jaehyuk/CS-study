# 프로세스와 스레드

- 프로세스: 실행중인 프로그램
- 스레드: 프로세스 안 실행 단위
- 노트북으로 유튜브를 볼 때
  - 프로세스 : 유튜브에서 동영상이 재생됨
  - 스레드: 동영상이 재생되고 있는 중(프로그램이 실행되고 있음)에 동시에 좋아요를 누름
  - 동영상이 실행되는 단위 하나, 좋아요를 누르는 실행 단위 하나
  - 프로그램에 여러개를 실행 할 수 있는 단위가 있음
  - 이 각각을 스레드라고 함

![프로세스](https://github.com/user-attachments/assets/79f06ef7-c85b-46ce-8a6b-7b2a1ca4acfa)

- 운영체제에는 여러개의 프로세스가 실행 될 수 있다.
  - 유튜브를 키고, 카톡을 키고, 파이참을 키고, 디코를 킨다.
  - 각각의 프로세스는 독립한 메모리를 할당 받는다.
  - 당연한건데, 유튜브와 카톡을 동시에 켜놨는데 유튜브에서 카톡에 있는 내 정보를 마음대로 쓰면 말이 안된다.

![프로세스와 스레드](https://github.com/user-attachments/assets/31809800-3afc-4a94-a608-19b8786fac3f)

- 하나의 프로세스 안에 여러개의 스레드(아까 유튜브 볼 때 좋아요 처럼)
- 이때 코드, 데이터, 힙은 공유가 되지만 스레드는 공유를 안한다.
  - 동영상 재생의 스레드와 좋아요의 스레드가 있을 때
  - 이 ‘실행’이라는 것은 결국 어떤 함수, 메서드가 호출되어 실행이 된다.
  - 메서드의 호출 정보들은 스택에 저장된다. 그리고 서로 아무 연관이 없다. → 독립적인 공간
  - 데이터에는 전역변수가 저장되는데 전역변수는 공통으로 쓴다.
  ### 정리하자면
  - 프로세스는 여러개의 스레드를 가지고 있는데 스레드끼리는 데이터를 공유 할 수 있다.
  - 그러나 스택 영역은 공유하지 않고 독립적으로 사용한다.

### 프로세스와 스레드에 대해 설명해주세요

- 프로세스는 실행중인 프로그램이고 스레드는 프로세스 안에서 실행되는 흐름 단위입니다.
- 프로세스는 메모리와 CPU를 프로세스마다 할당받아서 사용하는데
- 스레드는 프로세스 안에서 다른 스레드와 메모리와 CPU를 공유해서 사용합니다.
