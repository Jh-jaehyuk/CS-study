# CAPTCHA

![chaptcha_image1](https://github.com/user-attachments/assets/f40f2508-5303-4bfd-97d5-db5a3aa63f9b)  

# CAPTCHA

#### 사이트에 접속 시도중인 봇들이 많다 우리가 모르는 수많은 사이트에 접속을 시도하는데

#### 유명한 사이트 같은 경우에는 스팸 게시물이나 접속은 지속적으로 시도 하거나 데이터를 마음대로

#### 수집하는 봇들이 많은데 특히 AI가 발전함에 따라 AI 봇들 같은게 많은데 사실 데이터를 수집하는 봇을

#### 막는게 큰 의미가 없는게 개들은 IP를 바꾸거나 우회해서 오기 때문이다

#### 그렇다고 봇을 막자고 엄격하게 막아버리면 빈대 잡으려다 초가삼간 태운다는 말이 있듯이

#### 일반 사용자들도 봇으로 걸러버리고 접근성이 나빠지는 결과를 초래한다

#### 그래서 보통 캡챠를 도입한다

### 1. 문자형 CAPTCHA

![chaptcha_image2](https://github.com/user-attachments/assets/ec73a095-b0e3-4bd1-b0df-00ed06efeccb)  

##### 이미지로 표시된 글자로 구성되어 있고 요구하는 내용을 입력하는 형태

##### CHPTCHA 초기에는 우리가 흔히 보는 방식의 문자 해독식을 도입을 했는데

##### 요즘에는 정말 쉽게 봇에 뚫리는게 간단한 CNN 모델로 99.99%의 확률로 뚫는데 성공을 했다는 연구 결과 논문이 있을 정도다.

##### 심지어 이런 CAPTCHA를 자동으로 풀어누는 서비스를 제공하는 곳도 있을 정도

##### 그리고 이런 문자를 활용한 CAPTCHA는 사용자에게 욕을 선사 하기도 한다.

![chaptcha_image3](https://github.com/user-attachments/assets/b4b14cf3-59e9-446a-beda-e7355b4b81b8)  
![chaptcha_image4](https://github.com/user-attachments/assets/9dc5bc64-a343-433d-9ece-764c1ed343d6)

### 2. 지능형 CAPTCHA

##### 그래서 이런 문자형 CAPTCHA들이 많이 뚫리면서 사람의 지능을 조금 사용하게 하는 방법이 나오면서

##### 특정 이미지를 찾아내거나 아니면 물체를 회전 시킨다던지 틀린 그림을 찾게 한다던지

##### 이 역시도 앞서 말한 고령자 분들이나 시력이 안 좋거나 등등

##### 실제로 이런 CAPTCHA를 도입하면 가입률이나 구매율이 떨어진다는 논문이 나올정도다

![chaptcha_image5](https://github.com/user-attachments/assets/baeb3474-4c7f-4a12-a316-37e878a657f7)  
![chaptcha_image6](https://github.com/user-attachments/assets/11c90890-569a-4f9e-9904-dcce159312ee)

### 3. 체크형 CAPTCHA

![chaptcha_image7](https://github.com/user-attachments/assets/308a4cc1-2adf-49d9-9ab4-fbabefa13394)  

##### 또 이런 문제를 다시 보안해서 만든게 이런 체크형 CAPTCHA라고 볼 수 있다

##### 체크만 하면 통과시켜주는 CAPTCHA들인데 흔히 보는 형태로

##### 실제로는 클릭을 하는건 별 상관이 없고 저걸 누르면 사용자는 보지 못하지만

##### 뒤에서는 실제로 브라우저 종류, OS, User agent, Cookie, ... 등을 검사해서

##### 애가 봇인지 아닌지 검사를 하고 그래서 뭔가 의심스러운걸 발견하면

##### 우리를 화나게 하는 이런걸 풀어서 통과해야 되는거구요

##### 악명높은 리캡챠2라게 오답률이 상당히 높죠

![chaptcha_image8](https://github.com/user-attachments/assets/9f656e9e-94ff-483f-bf62-d8711193d2b9)

##### 그리고 이미지에서 어디가 버스고 어디가 오토바이고 어디가 사람인지 애매한 경우도 많죠

![chaptcha_image9](https://github.com/user-attachments/assets/aa0c9e4f-3862-4eb6-b0e8-a2ef9e1a0a0f)

##### 사실 저런 캡챠의 맹점이 시각 장애인들이나 시력이 좋지 못한분들을 위해 음성을 제공하는데

##### 그걸 듣고 음성을 듣고 그대로 라이브러리도 있고 아니면 간단한 딥러닝 모델로 이런 이미지

##### 캡챠를 풀어서 체크해주는 모델을 개발해서 90% 이상 풀었다는 연구 결과 논문도 있습니다.

### 4. honeypot

##### 애초에 사람하고 봇을 구별 하자는 방법으로 나온 방식인데

##### 기본적으로 봇들은 뭔가 input값이 비어있으면 그걸 채우려고 하는데 의도적으로 비워놓거나

##### 아니면 엄청 작게 만들어서 사용자가 눈치채지 못하게 하거나 아니면 아예 화면 밖으로 폼을

##### 빼놓는 방식을 쓰는데 이것도 display{none} 이런걸 쓰서 가려놓거나 하면 봇이 캡챠라고 인식해서

##### 안채워서 통과하는 방법으로 뚫리기도 합니다

![chaptcha_image10](https://github.com/user-attachments/assets/4504ec5b-00ff-4405-806e-70e6fb6a28aa)

### 5. Proof of work

![chaptcha_image11](https://github.com/user-attachments/assets/bd86f1e2-46f7-4ca7-bb66-60b2608efc19)

##### 간단하게 말하자면 제출 할때 파워 그러니까 CPU 해시 연산을 시키는건데 비트코인이라고 생각하면 됩니다.

##### 그래서 답이 맞으면 서버에서 검사하고 통과 시키는 방식이고 봇들의 CPU 파워를 낭비시켜서 공격을 포기하게

##### 만드는 방법이라고 생각하시면 됩니다.

### 6. Google ReCAPTCHA V3

![chaptcha_image12](https://github.com/user-attachments/assets/b458a583-f0e3-4e9a-a455-725c71b10550)

##### 요즘 최신 캡챠라고 볼 수 있는데 자동으로 자기가 알아서 체크하고 심지어 아예 아이콘만 띄우고

##### 가려놓는 식으로 캡챠를 놓는데 이런 경우에 유저가 뭘 할게 없어서 접근성이 매우 좋죠

##### 이런 방식은 어떻게 동작 하냐면

##### 간단하게 말해서 유저 정보를 구글이나 클라우드플레어로 보내서 분석한다고 볼 수 있죠

##### 브라우저, OS, Cookie, IP, ... 등등 의 점수를 자기들의 기준점 이상을 통과하면

##### 그때서 유저한테 토큰을 발행해주고 이제 그거를 다시 유저가 서버로 보내면 OK 통과 해주는 방식이죠

##### 의심스러우면 브라우저 API 검증 같은거를 추가로 돌려서 진짜 유저와 봇의 비율 같은걸 계산해서 보여주기도 합니다

##### 결론은 내 정보를 기업에 팔아서 편하게 쓴다는 소리입니다

##### 그게 싫으신 분들은 시크릿 모드로 사용 하시면 됩니다
