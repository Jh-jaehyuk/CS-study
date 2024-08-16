- 도메인 주소를 IP주소로 변환해주는 시스템
    - [naver.com](http://naver.com)을 검색할 때 172.168.어쩌구로 변환해준다.
    - 이렇게 변환해주는 것을 DNS라고 한다.
    - 내가 네이버를 검색하면 ISP(내가 사용하는 통신사)에서 DNS를 해주는 해석기를 가지고 있다.
    - DNS를 통해 naver에 가서 IP주소를 가지고 돌아오고 나는 이 주소로 연결을 하게 됨
- 도메인 체계

![domain](https://github.com/user-attachments/assets/3e6ea47c-605e-4e79-96d7-c55a7ec8affa)

- naver.com을 검색하면 맨 뒤에서 시작
    - 루트에서 com을 검색해서 naver를 찾음
- abc.co.kr을 검색하면
    - 루트에서 kr을 검색해서 co를 검색해서 abc를 찾음

### DNS가 뭐에요?

- DNS는 도메인 주소를 IP주소로 변환해주는 시스템입니다.
- DNS는 다음과 같은 순서로 작동하게 되는데요
- 첫번째로 URL을 입력하면, ISP가 관리하는 DNS해석기에 요청을 라우팅시킵니다.
- 그 다음에 DNS해석기가 루트 서버에 top-level의 서버 주소를 요청하고
- top-level에서 second-level, second-level에서 서버에서 sub DNS server
- 이렇게 해서 최종적으로 IP주소를 얻게 됩니다.