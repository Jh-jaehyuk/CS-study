# Linked List
```text
Linked List란 데이터들이 연결된 형태로 저장되는 자료구조
각 데이터는 노드(Node)라고 불리며, 노드는 데이터 값(Value)과 다음 노드를 가리키는 포인터(Next)로 구성
```
![Singlelinkedlist](https://github.com/user-attachments/assets/57d7b578-e36d-43a9-b871-d36fd5e5e453)  

## Advantages
1. **원소 추가와 삭제가 빠름**
2. **고정된 크기나 초기 크기 설정이 필요하지 않음**

## Disadvantages
1. **일반적인 list보다 많은 메모리를 사용함**
2. **특정 위치의 데이터를 탐색하는 데에는 더 많은 시간이 걸림**

## Variations
![linkedlist](https://github.com/user-attachments/assets/ba5d8a1e-d011-43fc-b16b-7a968fb2b3d3)  
1. **Singly Linked List(단일 연결 리스트)**  
    각 노드가 *오직 다음 노드를 가리키는 포인터*를 가짐
2. **Doubly Linked List(이중 연결 리스트)**  
    각 노드가 *이전 노드와 다음 노드를 가리키는 두 개의 포인터*를 가짐
3. **Circular Linked List(환형 연결 리스트)**  
    *마지막 노드가 첫번째 노드를 가리키는 형태*의 연결 리스트

## Implementation
위에서 언급한 것과 같이 Linked List의 형태에는 여러 가지가 있지만  
*Singly Linked List*만 구현하도록 한다.

```python
class Node:
    def __init__(self, value):
        self.value = value # 노드가 저장하는 데이터
        self.next = None # 다음 노드를 가리키는 포인터

class LinkedList:
    def __init__(self, head=None):
        self.head = head # 리스트의 첫 노드를 가리키는 포인터
    
    # 리스트의 끝에 노드 추가
    def append(self, data):
        new_node = Node(data) # 새로운 노드 생성
        if self.head is None:
            self.head = new_node # 리스트가 비어있다면 head가 새로운 노드를 가리키도록 설정
            return 
        last_node = self.head
        while last_node.next:
            last_node = last_node.next # 마지막 노드 찾음
        last_node.next = new_node # 마지막 노드의 next가 새로운 노드를 가리키도록 설정
    
    # 특정 값을 가지는 노드 삭제
    def delete(self, key):
        current_node = self.head
        
        # 첫번째 노드가 삭제할 노드일 경우
        if current_node and current_node.data == key:
            self.head = current_node.next # head를 다음 노드로 변경
            current_node = None # 현재 노드를 삭제
            return 
        
        # 삭제할 노드 탐색
        prev = None
        while current_node and current_node.value != key:
            prev = current_node
            current_node = current_node.next
        
        # 노드가 리스트에 없을 경우
        if current_node is None:
            return 
        
        # 이전 노드가 다음 노드를 건너뛰도록 설정하여 현재 노드를 삭제
        prev.next = current_node.next
        current_node = None
    
    # 리스트의 크기(노드 개수) 반환
    def __len__(self):
        cnt = 0
        current_node = self.head
        while current_node:
            cnt += 1
            current_node = current_node.next
        return cnt
    
    # 리스트의 노드 출력
    def __str__(self):
        res = ""
        current_node = self.head
        while current_node:
            print(current_node.value, end=" -> ")
            res += f"{current_node.value} -> "
            current_node = current_node.next
        res += "None"
        return res
```