# Stack
```text
스택이란 첫번째로 들어온 값이 마지막에 나가게 되는 후입선출(Last-In First-Out, LIFO) 형태의 자료구조
일상 생활에 비유하면 박스 쌓기에 비유할 수 있다.
아래부터 위로 박스를 쌓게되면 첫번째로 쌓은 박스를 꺼내기 위해선 그 위에 쌓아놓은 박스들을 먼저 꺼내야 한다.
```
<img width="373" alt="image" src="https://github.com/user-attachments/assets/d27f14f6-4bcd-45af-9ef7-7c550bfc7953">  

## Methods
![Stack-1](https://github.com/user-attachments/assets/a89e716b-b98b-47dc-854f-d6a9252ea721)  

필요에 의해 더 추가될 수 있지만, 일반적으로 아래의 **5개 Methods**를 갖는다.  
1. **pop**  
    스택의 맨 위 원소를 _제거_
2. **push**  
    스택의 맨 위에 원소를 _추가_
3. **top**  
    스택의 맨 위 원소를 제거하지 않고 그 값을 반환
4. **empty**  
    스택에 원소가 하나라도 있으면 0, 하나도 없으면 1을 반환
5. **size**  
    스택의 원소 개수를 반환
  
## Implementation
파이썬에서 스택을 구현할 때는 일반적으로 **list**를 사용한다.  
pop은 `list.pop()`으로, push는 `list.append()`로 쉽게 구현할 수 있기 때문이다.

```python
class Stack:
    def __init__(self):
        self.items = []

    def empty(self):
        return 1 if not self.items else 0

    def push(self, item):
        self.items.append(item)

    def pop(self):
        self.items.pop()

    def top(self):
        try:
            return self.items[-1]
        except Exception:
            raise IndexError("Stack has no elements.") 

    def size(self):
        return len(self.items)
```
  