# 메모리 구조
- 우리가 사용하는 메모리, 즉 RAM
- 프로그램을 실행했을 때 이 메모리를 어떻게 사용할까에 대한 내용
- 메모리 공간 종류 4가지: Code, Data, Heap, Stack

![ram구조](https://github.com/user-attachments/assets/17634435-87f1-4916-b472-8516e34b8140)

- 사용자가 프로그램을 실행하면 운영체제는 그 프로그램이 있는 하드디스크로 간다.
- 가서 그걸 메모리로 불러온다.
- CPU는 메모리로 불러온 것들을 실행한다.
- 각각의 역할을 알아보자

![ram구조2](https://github.com/user-attachments/assets/c2a63b12-fcf1-4f5b-a343-f0f5df1ae010)

- 코드 영역: 소스코드가 들어가는 부분
- 데이터 영역: 전역변수, 정적변수
- 힙 영역: 사용자가 동적으로 할당함
    - 크롬을 사용하다가 어떤 버튼을 눌렀을 때 그 버튼 정보가 어디에 저장이 됨
    - 저장되는 공간이 힙
- 컴파일 타임과 런 타임
    - 컴파일 타임 :프로그램을 배포할 때를 뜻함, 이미 메모리를 얼마나 차지할 지가 결정되어 있음
    - 런 타임: 사용자가 동적으로 할당, 즉 사용하면서 결정이 됨 → 사용중에 크기가 결정되는 것을 런타임이라 한다.
- 스택 영역: 후입선출
    - 함수 정보를 저장함, 지역 변수와 매개 변수가 저장됨
    - a 함수, b 함수, c 함수를 순서대로 호출했다면 (a → b → c 순으로 쌓임)
    - (스택 구조니까) c 함수가 실행되고 b 함수가 실행, a 함수가 실행 됨
- 힙과 스택 사이 화살표의 의미
    - 그 두 사이 공간은 빈 공간이다.
    - 힙이 길어지면 공간을 더 쓸 수도 있고 스택이 길어지면 공간을 더 쓸 수가 있다.

### 메모리 구조에 대해서 설명해주세요.

- 메모리에는 크게 네가지 종류가 있습니다. 코드, 데이터, 힙, 스택입니다.
- 코드는 소스코드가 들어가는 부분이고
- 데이터는 전역변수, 정적변수가 할당되는 부분입니다.
- 힙은 사용자가 직접 관리하는 영역으로 데이터가 동적으로 할당 되는 공간입니다.
- 스택을 함수의 호출정보, 지역변수, 매개변수들이 저장되게 됩니다.