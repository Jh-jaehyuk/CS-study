## 패킷

```text
네트워크 상에서 전달되는 데이터를 통칭한다.
그 중에서 사용자 데이터는 페이로드라고도 함.
```

![packet1](https://github.com/user-attachments/assets/9c669177-1e0c-4f76-aefd-ab90e702331b)  

- 여러 프로토콜들로 캡슐화되어 있음
    
    $$
    Header\ +Payload\ +Footer
    $$
    
    - 대부분 Footer는 잘 사용되지 않는다. 아래 예시를 통해 확인해보자.
        
        $$
        Ethernet\ +IPv4\ +TCP\ +HTTP
        $$
        
        1. HTTP 라는 프로토콜을 Payload로 해서 TCP를 Header로 붙임  
        2. HTTP + TCP를 Payload로 해서 IPv4를 Header로 붙임  
        3. HTTP + TCP + IPv4를 Payload로 해서 Ethernet을 Header로 붙임
        
        위와 같이 Payload에 Header를 붙이는 과정을 **캡슐화**라고 한다!
        
        ***캡슐화**: 여러 프로토콜을 이용해서 최종적으로 보낼 때 패킷을 만드는 과정

    - 캡슐화할 때 하위 계층이 붙고 상위 계층이 붙을 순 없다.


- 패킷을 받았을 때 프로토콜을 하나씩 확인하면서 데이터를 확인하는 과정을 **디캡슐화**라고 함
    
    ![packet2](https://github.com/user-attachments/assets/3cf20747-c8ac-46bc-a70b-e19afdcc9810)
    위 사진엔 보낼 때라고 되어있지만 받을 때라고 해야 맞다.
    
    - 디캡슐화할 때도 상위 계층을 먼저 확인하고 하위 계층을 확인해야 하는 순서가 있다.


- 계층별 패킷의 이름을 **PDU**(Protocol Data Unit)라고 한다.
    - 2계층의 PDU = 프레임 Ex) Ethernet + IPv4 + TCP + Data
    - 3계층의 PDU = 패킷 Ex) IPv4 + TCP + Data
        - 3계층 PDU 이름이 패킷이지만 일반적으로 패킷이라고 하면 네트워크 상에서 전달되는 데이터를 통칭한다.
    - 4계층의 PDU = 세그먼트 Ex) TCP + Data