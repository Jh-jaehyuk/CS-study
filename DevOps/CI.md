# CI/CD 왜 하냐?

한 번 이렇게 세팅해 놓으면 **Github Actions**가 Github의 **main branch의 변화를 감지**함

그래서 코드가 변화할 때 마다 변화된 상태로 빌드하여 자동 배포를 해줌

(수동 배포를 할 때는 코드가 바뀔 때 마다 우리가 그 상태를 빌드하여 배포하는 귀찮음이 있음)

→ **이 과정을 Github actions가 코드만 main branch에 올리면 알아서 해준다! (빌드 & 배포)**

![pipeline](https://github.com/user-attachments/assets/5917b0a0-4ac8-474e-af1b-4a2aca30a983)


- GitHub Actions란 ?
    
    Github Action은 Github 저장소를 기반으로 소프트웨어 개발 Workflow를 자동화 할 수 있는 도구로, **Github에서 직접 제공하는 CI/CD 도구이다.**
    
    github action은 Workflow를 기반으로 동작하며, Github 저장소에서 발생하는 build, test, package, release, deploy 등 다양한 이벤트를 기반으로 사용자는 직접 원하는 Workflow를 
    만들 수 있다.
    
    즉 우리는 **GitHub Actions로** **Workflow를 만들고, 이를 통해 빌드 및 배포 프로세스를 자동화 할 수 있다!**😎
    
    더 많은 이벤트를 보고 싶다면 https://github.com/features/actions 여기서 확인할 수 있다.

https://cafe.naver.com/eddicorp/1451

**Github Actions가 터진 상태에서 Frontend 수동 배포 글 참고**

Github Actions가 터져 자동 배포가 안되기 때문에 수동으로 빌드 & 배포 진행

- local frontend file build 하기

local frontend 저장소에 가서 npm run build 명령어 실행!

물론 npm 명령어를 하기 위해선 npm을 깔아야 함

- npm install —leagcy-peer-deps
- npm run build

build 명령어를 마치면 frontend workdir에 /dist 폴더가 생성된다.  

![dist](https://github.com/user-attachments/assets/23fd969b-3ca4-47ca-a108-c6612b69f4fe)


/dist 폴더에는 html을 구성하기 위한 애들이 있음 (css, fonts, js 등..)

이 내용들을 aws상의 frontend html 폴더로 scp 방식을 통해 전송한다.

```yaml
scp -i "pem키(상대경로 혹은 절대경로)" -r * ec2-user@AWS_IP:/home/ec2-user/프로젝트팀/vue-frontend/html/
```

![scp_result](https://github.com/user-attachments/assets/64744bbe-5935-47e9-84d0-c50d72638e67)  

scp를 통해 dist의 내용들이 aws의 html 폴더 내에도 복사된 것을 확인할 수 있다.

잘 복사 됐다면, 다시 html의 상위 폴더로 돌아와서 docker-compose.yml 파일을 구성한다.

docker-compose.yml 파일에는 docker-compose 명령어들과 변수들의 포맷으로 이루어짐

(뭘 쓰는지 궁금하다면 docker-compose 명령어 “keyword” 치면 될 듯)

내용은 local 상에서 만들었던 docker-compose.yml 파일과 동일

- aws 상 docker-compose.yml 파일
    
    
    ```yaml
    version: "3.7"
    services: # front에서 활용할 서비스
      nginx:  # nginx란 서비스를 쓸거다.
        image: "nginx:latest" # nginx 최신버전을 쓸 것임
        container_name: frontend-deploy-nginx # 사용할 container 이름
        restart: unless-stopped # container를 stop 시키기 전까지 항상 재시작
        volumes: # networks 처럼 아래 정의가 안되어 있다면 새로 볼륨을 생성
          - /home/ec2-user/att/vue-frontend/conf:/etc/nginx/conf.d # 새 볼륨을 생성해서 연결
          - /home/ec2-user/att/vue-frontend/html:/usr/share/nginx/html # 새 볼륨을 생성해서 연결
        ports: 
          - "80:80"
        networks: # 해당 services와 연결할 network 추가
          - app
    
    networks:
      app:
        driver: bridge
    ```
    
# services 컨테이너

  - services
    
  Services는 Docker Compose에서 실행할 컨테이너를 정의합니다. 
  각각의 서비스는 이미지 이름, 컨테이너 이름, 사용할 포트, 환경 변수 등의 
  정보를 포함합니다.
    
  - services/volumes
    
  volumes는 컨테이너와 호스트 간의 데이터 공유를 위한 볼륨을 정의합니다.
    
  볼륨의 역할은 다음과 같다.
    
  Host 의 volume 을 사용하게 되면, 사용자가 서버에 저장한 DATA 가 다른 서버에는 저장되지 않는다. 
    
  이로 인해, 사용자가 같은 서버에 접속하는 보장이 없으므로, 만약 다른 서버에 접속한다면, 전에 저장한 DATA를 조회 못 하는 문제가 생긴다. 
    
  이를 해결하기 위해 외부 스토리지의 volume 에 연결해서 어느 서버에 접속해도 DATA가 유지되게 해야 한다
    
  **즉, 외부에서 데이터에 접근할 때, 각 컨테이너에 저장하는게 아니고**
    
  **docker-compose 에서 제공하는 volume을 참조하도록 해서 누구나 동일한 상태의 데이터를 조회할 수 있도록 돕는 역할이다.**
    
  이를 시각화하면 다음과 같다.
    
  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a6b22cb1-0923-4019-95a9-9a67b1a2bbea/377090be-0ce9-4f3f-9dd4-7656393abac0/Untitled.png)
    
  외부의 컨테이너들이 docker-compose에서 제공한 volume의 데이터를 참조하는 모습
    
  (어떤 컨테이너든 동일한 데이터를  참조할 수 있다.) 
    
  - services/ports
    
  ports는 컨테이너가 사용할 포트와 호스트에서 사용할 포트를 지정합니다.
    
  지정해주고 docker ps 해보면 내가 이미지화 했던 docker-compose 에서
    
  80 (컨테이너 내부 포트)→ 80 (호스트에서 사용(=공개)할 포트)로 
  tcp 방식으로 통신하는 것을 확인할 수 있다.
    
  ![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/a6b22cb1-0923-4019-95a9-9a67b1a2bbea/55eeeb2c-5ff7-4136-be39-1abe9ace85c3/Untitled.png)
    
  컨테이너 내부에서 모두에게 공개로 보낸다 ??
    
  local상에서 돌아갔던 내용을 이제 local이 아닌 모두에게 공개(배포)하겠다는 건가?
    
  **→ 모두에게 공개는 우리가 aws에서 인바운드 설정으로 ipv4 모두에게 공개한 포트만 
  가능하다. (우리 플젝의 경우는 80과 33333을 공개했으니 이것만 공개)**
    
  8000에 대해서는 공개는 안 했지만, local상에서만 db를 돌게하는게 아니라 호스트가 
  사용하도록 만들어 외부 요청에 대해 db 데이터를 이용하게 만듦
    
  - services/networks
    
  해당 services 컨테이너가 어떤 networks를 사용할지 지정한다.
  services 의 컨테이너에 networks 를 지정하면, 밑에 networks 에 작성된 network를 
  참조하게 된다. 만약, networks 에 network 를 정의하지 않으면, 새 network 가 생성된다
    
  **services 컨테이너 networks에 app이라 썼으므로 아래 networks에 app에 대해 정의하기** 
    
  # networks 컨테이너
    
  services 컨테이너에서 사용하기로 한 networks에 대해 정의하는 부분
    
  driver: bridge는 bridge 방식으로 통신하겠다는 의미
    

docker-compose.yml 파일 까지 구성했다면,

docker-compose up 명령어를 실행한다!

실행하면 docker-compose.yml 파일에 구성된 내용대로 docker-compose가 생성됨

docker-compose.yml 파일에서 지정한 port방식과 container_name을 따르는 것을 확인!

![frontend_ci](https://github.com/user-attachments/assets/eee661ee-1a1a-4ace-8250-4d527005b425)
