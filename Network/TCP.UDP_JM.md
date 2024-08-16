## TCP:신뢰성 높은 프로토콜

- 신뢰성이 높다 → 상대방이 받았는지 못 받았는지 확인
- 대신 느리다

![tcp](https://github.com/user-attachments/assets/809a1f7c-91c9-4b66-a24a-a7adc01e0740)

- **SYN:**Connection을 생성할 때 사용하는 flag
- **FIN:**Connection을 끊을 때 사용하는 flag
- **ACK:**data를 전송하면 수신자가 받았음을 알려주기 위해 쓰는 Flag

### connection 생성(3way handshake)

![3way](https://github.com/user-attachments/assets/f03e7eb3-90c8-443e-b5f2-289e637a89c2)

### Data 전송

![3wayy](https://github.com/user-attachments/assets/13b4a0c4-0a86-4cae-a0e3-a567c67581f7)

### **Connection 해제(4way handshake)**

![4way](https://github.com/user-attachments/assets/3cb50763-1cad-4a00-ba8d-baa9604171b3)

- 데이터 흐름제어(수신자 버퍼 오버플로우 방지)
- 혼잡 제어
    - 하나씩만 연결되어 있는 것이 아니라 거미줄처럼 여러군데가 연결되어 있는데 그중 하나에서 문제가 생기면 여기저기 문제가 됨
    - 네트워크가 마비됨
    - 이것을 방지하기 위해 이 네트워크 안에서는 몇개의 메세지만 돌아다니도록 설정함
- 1:1만 가능하다

## UDP: 빠르다 대신 신뢰성이 낮다

- 신뢰성은 연결을 통해 알 수 있다.
- UDP는 연결이 이루어지지 않는다. 그냥 보내고 끝 대신에 빠르다.
- 유튜브 라이브, 트위치 아프리카 같은 스트리밍 서비스에 사용
- 한 프레임이 깨져도 다음 프레임이 바로 와서 제대로 된 화면을 보여준다.
- 1:1, 1:N, N:M이 가능하다.

### TCP와 UDP에 대해 설명해주세요

- TCP는 신뢰성 있는 통신을 위해 사용하는 프로토콜로 높은 신뢰성을 보장하지만 UDP보다는 속도가 느립니다. 3way, 4way handshake로 서버와 클라이언트가 1:1로 통신을 하고요 흐름제어와 혼잡제어가 이루어지게 됩니다.
- UDP는 비연결형 프로토콜로, 손상된 데이터에 대해서 재전송하지 않습니다. 신뢰성이 낮지만 속도가 빨라서 스트리밍 같은 서비스에 사용됩니다. 마지막으로 1:1, 1:N, N:M으로 연결이 가능합니다.