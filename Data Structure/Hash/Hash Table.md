# Hash Table

**해시 테이블**(해시 맵 또는 딕셔너리)은 키(key)와 값(value)으로 구성된 자료구조이다.  
키와 값으로 이루어져 있는데 왜 해시 테이블이라고 부를까?  
  
키를 해시 함수에 통과시켜 나온 해시 값을 인덱스로 사용하여  
테이블에 값을 저장하거나 탐색하기 때문!  
  
Hash Function에서 말한대로 서로 다른 수가 같은 해시 값을 가지게 되면 이를 "**충돌**"이라 한다.

---
## Hash Table의 장단점
**장 점**  
* 자료의 검색, 읽기, 저장 속도가 빠름
* 자료가 중복되는지 확인하기 쉬움
  
**단 점**  
* 일반적으로 더 많은 저장 공간을 필요로 함
* 충돌을 해결할 방법이 필요함
  
그렇다면 어떻게 **충돌**문제를 해결할 수 있을까?

---
## 충돌을 해결하는 방법
1. **Separate Chaining(개별 체이닝)**
> **개별 체이닝**은 충돌한 키의 자료를 연결 리스트로 저장하는 방법이다.
  
![separate-chaining](https://github.com/user-attachments/assets/b1cb9cf5-7383-484a-9a2c-071319265d56)
  
2. **Open Addressing(오픈 어드레싱)**
> **오픈 어드레싱**은 충돌한 키 다음에 위치한 인덱스들 중 비어있는 곳에 저장하는 방식이다.
  
![open-addressing](https://github.com/user-attachments/assets/3f8023dc-ad15-44eb-af92-23b422290e64)
  
---
## 충돌 해결 방식들의 특징
**Separate Chaining**
* 모든 원소가 자신의 해시값과 일치하는 주소에 저장됨
* 전체 저장 공간보다 많은 개수를 저장할 수 있음
* 해시 값 충돌이 빈번하게 발생한다면 작동 속도가 빠르지 않음
  
**Open Addressing**
* 해시 값 충돌이 자주 일어나더라도 작동 속도에 큰 차이가 없음
* 모든 원소가 자신의 해시값과 일치하는 주소에 저장된다는 보장이 없음
* 전체 저장 공간보다 많은 개수를 저장할 수 없음
  
---
## 파이썬으로 해시 테이블 구현하기

```python
class HashTable:
    def __init__(self, max_len=1000):
        self.max_len = max_len
        self.table = [[] for _ in range(self.max_len)]

    def _hash(self, key):
        res = sum([ord(s) for s in key])
        return res % self.max_len
    
    def set(self, key, value):
        idx = self._hash(key)
        self.table[idx].append((key, value))

    def get(self, key):
        idx = self._hash(key)
        value = self.table[idx]
        if not value:
            return None
        for v in value:
            if v[0] == key:
                return v[1]
        return None
```