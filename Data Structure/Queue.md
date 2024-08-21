# Queue
```text
큐는 먼저 들어온 값이 먼저 나가는 선입선출(First-In First-Out, FIFO) 형태의 자료구조
일상 생활에 비유하면 줄 서는 것에 비유할 수 있다.
먼저 줄 서기 시작한 사람이 먼저 입장하기 때문이다.
```
![Queue-1](https://github.com/user-attachments/assets/bcb3832b-cc01-4166-99d3-05dc5eb49fea)

## Methods
![Queue-2](https://github.com/user-attachments/assets/b0645bc6-cd72-4e85-b9ed-360692cfea4d)  

필요에 의해 더 추가될 수 있지만, 일반적으로 아래의 **6개 Methods**를 갖는다.  
1. **enqueue**  
    큐의 맨 뒤에 원소를 _추가_
2. **dequeue**  
    큐의 맨 앞 원소를 _제거_
3. **front**  
    큐의 맨 앞 원소를 제거하지 않고 그 값을 반환
4. **back**  
    큐의 맨 뒤 원소를 제거하지 않고 그 값을 반환
5. **empty**  
    큐에 원소가 하나라도 있으면 1, 하나도 없으면 0을 반환
6. **size**
    큐의 원소 개수를 반환

## Implementation
파이썬에서 큐를 구현하는 방식은 두 가지가 있다.  
첫번째는 스택과 마찬가지로 list를 이용하는 방법이고,  
두번째는 collections 모듈에 있는 deque를 이용하는 방법이다.  
  
**첫번째 방법**
```python
class Queue:
    def __init__(self):
        self.items = []

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        self.items.pop(0)

    def front(self):
        try:
            return self.items[0]
        except Exception as e:
            raise IndexError("Queue has no element.")

    def back(self):
        try:
            return self.items[-1]
        except Exception as e:
            raise IndexError("Queue has no element.")

    def empty(self):
        return 1 if not self.items else 0

    def size(self):
        return len(self.items)
```
  
**두번째 방법**
```python
from collections import deque

class Queue:
    def __init__(self):
        self.items = deque()

    def enqueue(self, item):
        self.items.append(item)

    def dequeue(self):
        self.items.popleft()

    def front(self):
        try:
            return self.items[0]
        except Exception as e:
            raise IndexError("Queue has no element.")

    def back(self):
        try:
            return self.items[-1]
        except Exception as e:
            raise IndexError("Queue has no element.")

    def empty(self):
        return 1 if not self.items else 0

    def size(self):
        return len(self.items)
```
  
### 두가지 방법의 차이점
🤔두 방법은 dequeue 구현 방식만 다른 것 같은데, 어떤 차이가 있을까?    
💡**dequeue 구현 방식에 따라서 큐의 작동 시간이 달라진다!**  

`list.pop()`은 pop 내부에 인덱스를 적어서 해당 인덱스의 값을 제거한다.  
하지만 list는 메모리가 연속적이어야 하기 때문에, 해당 인덱스의 값을 제거하고 
그 인덱스 뒤에 있는 값들을 앞으로 가져오게 된다.  
메모리를 이동하는 것 또한 시간을 소요하게 되는 것이므로 list로 작성한 것은 큐 내부에 원소가 많다면
`dequeue`가 동작할 때마다 많은 시간을 소요하게 된다.  
list와 달리 deque로 구현하게 되면, deque는 *Linked-List*로 구현되어 있어서 
별도로 메모리 이동하는 시간을 갖지 않게 된다.  
따라서, `dequeue`가 동작하는데 *O(1)*만큼의 시간만 걸리게 된다.
