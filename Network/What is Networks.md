## Network

### 네트워크란 무엇인가?

**네트워크란?**

노드들이 데이터를 공유할 수 있게 하는 디지털 전기통신망의 하나이다.

즉, 분산되어 있는 컴퓨터를 통신망으로 연결한 것을 말한다.

네트워크에서 여러 장치들은 노드 간 연결을 사용하여 서로에게 데이터를 교환한다.

*노드 : 네트워크에 속한 컴퓨터 또는 통신 장비

**인터넷이란?**

문서, 그림 영상과 같은 여러가지 데이터를 공유하도록 구성된 세상에서 가장 큰 전세계를 연결하는 네트워크

흔히 **www**를 인터넷으로 착각하는데, www는 인터넷을 통해 웹과 관련된 데이터를 공유하는 것

### 네트워크의 분류

**크기에 따른 분류**

- LAN(Local Area Network)
    
    <aside>
    💡 근거리 통신망
    → PC방에서 친구와 스타크래프트를 LAN으로
    
    </aside>
    
- WAN(Wide Area Network)
    
    <aside>
    💡 멀리 있는 지역을 하나로 묶은 네트워크
    → 가까운 지역끼리 묶인 LAN과 LAN을 다시 하나로 묶은 것
    
    </aside>
    
    ![wan1](https://github.com/user-attachments/assets/bfaf7fb9-45d9-446b-b2fa-1791c3fc8248)
    
- MAN(Metropolitan Area Network)
- Etc.(VLAN, CAN, PAN, …)

**연결 형태에 따른 분류**

- Star
    
    <aside>
    💡 중앙 장비에 모든 노드가 연결된 형태
    → LAN 대역을 만들 때 이용됨
    
    </aside>
    
    ![star1](https://github.com/user-attachments/assets/1a91f673-b2a7-464b-841e-0d24c1cb0d59)
    
    ![star2](https://github.com/user-attachments/assets/77a0e0cb-c0f7-4c41-ad12-c3e3c0be167f)
    
    중앙 장비가 고장난다면 문제가 생김
    
    - 일반적으로 가정집에서는 공유기를 통해서 핸드폰, 컴퓨터, TV 등이 연결됨
    - 공유기가 고장나면 전부 다 인터넷 불가
    
- Mesh
    
    <aside>
    💡 여러 노드들이 서로 그물처럼 연결된 형태
    
    </aside>
    
    ![별모양으로 구성되어 있지만 Star형이 아님에 주의하자.](https://github.com/user-attachments/assets/88080db9-ddda-4a93-b9ac-74445902577b)
    
    별모양으로 구성되어 있지만 Star형이 아님에 주의하자.
    
    ![mesh2](https://github.com/user-attachments/assets/db1c0990-44b1-49eb-8f86-67251c0138bd)
    
- 혼합형
    
    <aside>
    💡 실제 인터넷은 여러 형태로 구성된 혼합형
    
    </aside>
    
    ![star mesh](https://github.com/user-attachments/assets/ef66e046-389e-42bf-9d08-671182413a3c)
    

### 네트워크의 통신방식

**네트워크에서 데이터는 어떻게 주고 받는가?**

- 유니 캐스트
    
    <aside>
    💡 특정 대상이랑만 1:1로 통신
    
    </aside>
    

- 멀티 캐스트
    
    <aside>
    💡 특정 다수와 1:N으로 통신
    
    </aside>
    

- 브로드 캐스트
    
    <aside>
    💡 네트워크에 있는 모든 대상과 통신
    
    </aside>
    

어떤 교실을 예로 들어보자.

교실 안에 있는 한 명의 학생만 선택하여 통신하면 **유니 캐스트**

교실 안에 있는 한 분단을 선택하여 통신하면 **멀티 캐스트**

교실 안에 있는 학생 전체와 통신하면 **브로드 캐스트**

**생각해볼 문제**

→ 그렇다면 특정한 사용자를 어떻게 찾을 수 있을까?

### 네트워크 프로토콜

**프로토콜이란?**

프로토콜은 일종의 약속, 양식

네트워크에서 노드와 노드가 통신할 때 어떤 노드가 어느 노드에게 어떤 데이터를 어떻게 보내는지 작성하기 위한 양식

택배는 택배만의 양식이 있듯, 각 프로토콜들도 해당 프로토콜만의 양식이 존재함

**여러가지 프로토콜**

![protocols](https://github.com/user-attachments/assets/1eae3392-9bf8-4ced-bb29-3f8cc48ba88e)

- 가까운 곳 ⇒ MAC 주소
    - Ethernet 프로토콜
- 멀리 있는 곳 ⇒ IP 주소
    - ICMP
    - IPv4
    - ARP
- 여러가지 프로그램을 이용할 때 ⇒ 포트 번호
    - TCP, UDP

실제로는 가까운 곳과 연락한다고 해서 Ethernet만 사용하는 것은 아님

어떤 데이터를 보낸다고 해보자.

그 데이터를 보낼 때 어떤 프로그램을 사용할지(TCP),

얼마나 멀리 떨어져있는 지역인지(IPv4),

그 지역에서 어떤 컴퓨터인지 특정(Ethernet)하는 과정을 거쳐서 통신이 발생함

$$
Data → TCP → IPv4 → Ethernet
$$

위와 같이 프로토콜들이 하나로 합치는 것을 **캡슐화(Capsulation)** 한다라고 함