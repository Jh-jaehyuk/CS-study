# Cryptography using Hash
  
```text
해시는 역변환이 불가능하다(또는 너무 어렵다)는 특징 때문에 암호화에 자주 사용됩니다.
```
  
## 해시를 이용한 암호화
로그인 기능을 구현한다고 할 때, 아이디와 패스워드를 그냥 데이터베이스에 저장하면
어떤 일이 발생할까요?  
데이터베이스가 해킹당하면 모든 계정이 그대로 털린다는 문제점이 있습니다!  
  
문제를 해결하기 위해 패스워드를 SHA-256과 같은 해시 알고리즘을 통해 
암호화하는 방법을 사용할 수 있습니다.  
![sha-256-image](https://losskatsu.github.io/assets/images/blockchain/sha256/sha256-02.png)  
일반적으로 SHA-256을 직접 구현하는 경우는 거의 없으니 구현 방법은 생략합니다.  
  
패스워드를 SHA-256을 이용해 암호화하게되면 64자리의 16진수로 반환되고 
그 값을 데이터베이스에 저장해서 사용하도록 할 수 있습니다.  
하지만, 이 또한 문제가 될 수 있는데 다른 모든 곳에서 똑같이 SHA-256을 사용한다고하면
동일한 패스워드는 동일한 해시값을 갖기 때문에 마찬가지로 계정이 털린다는 것입니다!  
그럼 이 문제를 어떻게 해결해야할까요?  
    
---
## Salt
위의 문제는 Salt라는 것을 추가하여 해결할 수 있습니다.  
Salt는 각 계정별로 다른 값을 갖는 임의의 문자열이라고 할 수 있습니다.  
이걸 사용하면 어떻게 같은 패스워드에 같은 해시값이 나오는 문제를 해결할 수 있을까요?  
아래의 예시를 통해 확인해봅시다.  

**without a salt**  
| Username | Password | Hashed value(SHA-256) |  
|---|---|---|  
| user1 | password123 | EF92B778BAFE771E89245B89ECBC08A44A4E166C06659911881F383D4473E94F |  
| user2 | password123 | EF92B778BAFE771E89245B89ECBC08A44A4E166C06659911881F383D4473E94F |  
  
같은 비밀번호라면 같은 해시값을 가집니다.  
그렇다는 것은 해시값을 통해 비밀번호를 특정하기 쉬워진다는 것입니다.  
만약 **Salt**를 추가한다면 어떨까요?  
  
**with a salt**  
| Username | Salt | Password + Salt | Hashed value(SHA-256) |  
|---|---|---|---|  
| user1 | D;%yL9TS:5PalS/d | **password123**D;%yL9TS:5PalS/d | 9C9B913EB1B6254F4737CE947EFD16F16E916F9D6EE5C1102A2002E48D4C88BD |  
| user2 | )<,-<U(jLezy4j>* | **password123**)<,-<U(jLezy4j>* | 6058B4EB46BD6487298B59440EC8E70EAE482239FF2B4E7CA69950DFBD5532F2 |  
  
**비밀번호는 같지만 Salt가 달라서 해시값이 크게 달라지는 것을 볼 수 있습니다.**  
이렇게 되면 특정한 값이 어떤 해시값을 갖는지 유추하기 어려워져서
해시값을 통해 비밀번호를 특정하는 것이 거의 불가능해집니다.
