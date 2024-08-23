# 왜 하냐?

우리는 현재 AWS를 통해 웹 서버를 배포하고 있는 상태

즉, AWS에서 공인 ip를(인스턴스) 돈 주고 하나 사서 배포하고 있다.

우리의 프로젝트는 웹 서버에 딥러닝 추론을 위한 서비스를 제공하는데, 
딥러닝 연산 기능마저도 AWS에서 지원을 해 준다. 
하지만 이것을 사용할 시 요금 폭탄의 이슈 발생… 😱

요금 폭탄도 있지만, 제한된 자원 내에서 해결해야 하므로 AWS의 딥러닝 서버가 아닌

우리가 가지고 있는 딥러닝 서버 즉, DLLS(DeepLearning Local Server)를 활용한다.

**굳이 소켓 서버를 만들지 않고도 웹 서버에서 바로 DLLS로 요청을 보낼 수는 있지만**

**(포트를 따로 뚫는다던가, 프록시 우회? 등으로..) 이렇게 할 시 보안의 이슈에 매우 취약해짐**

**⇒ 그런고로, 우리는 한정된 자원 안에서 보안을 지키며 서비스를 구현하기 위해
소켓 서버, 소켓 클라이언트 통신을 한다.**

# 그래서 어떻게 구현하냐?

 

socket server의 역할을 수행하는 것은 aws_server의 fastapi 폴더가 담당

socket client의 역할은 local client가 담당 (linux 기반으로 통신하기 위해 WSL에서 실행)

<details>
<summary> aws server = socket server </summary>
일단 aws server에 접속하면 최상단은 현재 이런 구성을 가짐



- att : 내가 실제로 구동 중인 프로젝트 파일들이 들어있음 (front, back, fastapi)
- ssl : 보안을 지키며, 소켓 통신을 지원하기 위한 것들 
pem키 certificate 등의 파일에서 허락된 socket client만 통신을 하기 위함
- sw : aws 서버 초기 세팅에는 파이썬 관련 기능들을 지원하지 않기 때문에
이를 위해 파이썬 기능들을 지원하도록 따로 깔아 둠

    <details>
    <summary>aws_server/project_name/validation</summary>
    project_name 폴더로 가면 우리가 CI/CD 때 구성했던 환경들이 있음

    소켓 서버 통신이 제대로 돌아가는지 검증하기 위한 validation 폴더를 생성

    **(** validation에서 구성한 것들은 소켓 통신이 되는지 확인용이지 우리가 최종적으로 
    사용할 폴더는 아님! 다만 validation에서 했던 빌드업이 최종에 그대로 적용 됨**)**

    ![aws_root](https://github.com/user-attachments/assets/90ae4ecb-2d0c-4d5f-ad6a-9c8fba553655)  

    validation 디렉토리에 가보면 3가지 디렉토리가 존재

    socket_boiler_plate : 소켓 서버 역할을 수행

    socket_control_with_fastapi : 딥러닝 요청 서빙을 위한 fast api 기능을 수행 

    test-dlls : 딥 러닝 연산 요청에 관한 처리를 수행 (실제 연산까지)

    위의 3개는 분리돼서 진행 되는게 아니고 포함 관계임

    test-dlls( fastapi ( socket-server ) ) ) 의 포함 관계

    **공인 ip를 가지는 socket -server는 내부 망의 socket-client가 어딨는지 모르기 때문에**

    **직접적으로 바로 연결할 수 없음 그렇기 때문에 간접적으로 접근하기 위해서**

    **그리고 fastapi는 비동기 처리를 지원하기 때문에 요청은 fastapi를 거친다.**

    **fasapi는 공인,사설 ip를 엮는 중간 다리를 할 뿐만 아니라 실제 딥러닝 연산 요청을 비동기 방식으로 서빙하는 역할도 수행** 
    → 그 중 우리가 서비스할 custom protocol은 test-dlls에서 구현

    # socket_boiler_plate

    1. **AWS 환경에서 FastAPI에서 구동 될 Socket Server 구동하기**

    얘는 소켓 서버의 역할을 수행하며 소켓 클라이언트와 소켓 통신을 지원한다.

    소켓 클라이언트와 통신하기 위해 소켓 서버의 .env 세팅은 다음과 같이 작성한다.

    ```python
    # socket_boiler_plate .env
    HOST=0.0.0.0
    PORT=37373
    ```

    HOST는 소켓 서버 입장에서 내부망이 뭔지 모르니까 어떤 ip든 받아야 해서 0.0.0.0 설정

    PORT는 소켓 통신을 위한 포트를 37373 번으로 뚫어 놓음

    ⇒ 일단 소켓 서버와 소켓 클라이언트는 37373을 통해 공인과 사설 IP를 연결 시키고

    소켓서버와 aws 내부의 다른 api (fastapi, vue ..)랑 연결 통신하려면 해당 PORT를 뚫으면 됨

    1. **AWS 환경에서 Socket Server 구동 검증하기**

    1번 과정에서 .env에 37373 PORT를 뚫어 소켓통신을 지원하므로 통신할 외부 
    클라이언트를 작성한다.

    **우리는 이 과정을 aws 서버에서 구현했기 때문에 실제 aws 인바운드 규칙에서도**

    **37373 PORT를 추가시켜야 함! (추가 안하면 37373 통신이 막힘)**

    향후 이 부분의 ip는 우리가 사용할 DLLS IP주소가 적혀야 함
    <img src = "https://github.com/user-attachments/assets/83130497-c90b-4786-adc1-b6851a9ffba1">  
    </details>

</details>

<details>
<summary> local client = socket client = 실제 딥러닝 연산 수행하는 곳 </summary>
socket_client_boiler_plate .env 세팅

```python
TARGET_HOST=AWS IP # AWS와 소통해야 하므로 AWS IP만 받음
TARGET_PORT=37373 # 소켓 서버와 소켓 통신을 위한 37373번 포트 사용
```

이렇게 소켓 클라이언트 세팅 후 소켓 서버, 소켓 클라이언트 둘 다 실행

```python
# 소켓 서버
python3 -m main.server

# 소켓 클라이언트
python3 -m main.client
```

둘 다 실행하면 아래와 같이 소켓 통신으로 송수신이 가능해진다.

<img src="https://github.com/user-attachments/assets/0ef4ba71-c768-41af-86f8-a392cfd1fafc">  

사실 굳이 fastapi를 거치지 않더라도 소켓 서버 ↔ 소켓 클라이언트 간 통신은 가능함

**fastapi는 오로지 비동기 처리를 지원하기 위해서 거쳐가는 느낌인가?**
</details>