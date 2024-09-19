# Time complexity

> 계산 복잡도 이론(Computational complexity theory)에서 시간 복잡도는   
> 문제를 해결하는데 걸리는 시간과 입력의 함수 관계를 가리킨다.
> 알고리즘의 시간복잡도는 주로 *Big-O Notation*(빅-오 표기법)을 사용하여 나타낸다.  

만약 크기 n의 모든 입력에 대한 알고리즘에 필요한 시간이 최대 $5n^3+3n$ 의 식을 가진다면,  
이 알고리즘의 **점근적 시간 복잡도**는 $O(n^3)$ 이라고 할 수 있다.
  
## Big-O Complexity Chart
![Big-O complexity Chart](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*5ZLci3SuR0zM_QlZOADv8Q.jpeg)  
  
시간 복잡도는 위에 보이는 그래프처럼 나타낼 수 있고, 명칭은 아래와 같이 사용한다.  

| Name | Time Complexity |
|:--:|:-------------:|
| Constant Time | O(1) |
| Logarithmic Time | O(log n) |
| Linear Time | O(n) |
| Quasilinear Time | O(n log n) |
| Quadratic Time | O(n^2) |
| Exponential Time | O(2^n) |
| Factorial Time | O(n!) |

## Time Complexities

### Constant Time - O(1)
> 입력되는 값 **n에 영향을 받지 않는** 알고리즘

**Example**  

```python
if a > b:
    return True
else:
    return False
```

### Logarithmic Time - O(log n)
> 입력되는 데이터를 **전부 다 확인할 필요가 없는** 알고리즘

**Example**

```python
# Binary Search
def binary_search(data, target):
    n = len(data)
    left, right = 0, n - 1
    
    while left <= right:
        mid = (left + right) // 2
        if target < data[mid]:
            right = mid - 1
        elif target > data[mid]:
            left = mid + 1
        else:
            return mid
    
    raise ValueError("Target이 존재하지 않습니다.")
```

### Linear Time - O(n)
> 입력되는 데이터를 한번씩 확인하는 알고리즘

**Example**

```python
# Linear Search
def linear_search(data, target):
    for i in data:
        if i == target:
            return i
    raise ValueError("Target이 존재하지 않습니다.")
```

### Quasilinear Time - O(n log n)
> 입력되는 데이터의 값 하나하나마다 log n 만큼의 시간이 소요되는 알고리즘
> 일반적으로 **정렬 알고리즘**에서 주로 보임

**Example**  

![Merge sort](https://miro.medium.com/v2/resize:fit:800/format:webp/1*a7UnRSbux0RSgVqmFDN9_Q.png)  

```python
# Merge Sort
def merge_sort(data):
    if len(data) <= 1:
        return 
    
    mid = len(data) // 2
    left_data = data[:mid]
    right_data = data[mid:]
    
    merge_sort(left_data)
    merge_sort(right_data)

    left_idx = 0
    right_idx = 0
    data_idx = 0

    while left_idx < len(left_data) and right_idx < len(right_data):
        if left_data[left_idx] < right_data[right_idx]:
            data[data_idx] = left_data[left_idx]
            left_idx += 1
        else:
            data[data_idx] = right_data[right_idx]
            right_idx += 1
        data_idx += 1

    if left_idx < len(left_data):
        del data[data_idx:]
        data += left_data[left_idx:]
    elif right_idx < len(right_data):
        del data[data_idx:]
        data += right_data[right_idx:]
```

### Quadratic Time - O($n^2$)
> 입력 데이터 각각에 대해서 n 만큼의 시간이 소요되는 알고리즘

**Example**

```python
# Bubble Sort
def bubble_sort(data):
    swapped = True
    while swapped:
        swapped = False
        for i in range(len(data) - 1):
            if data[i] > data[i + 1]:
                data[i], data[i + 1] = data[i + 1], data[i]
                swapped = True
```

### Exponential Time - O($2^n$)
> 입력되는 데이터가 하나 늘어날 때마다 **소요시간이 두 배로** 늘어나는 알고리즘  
> 암호학에서, _Brute-force_ 공격은 비밀번호로 가능한 모든 요소들을 하나씩 확인함  
> 이렇게 확인하면 _Exponential_ 알고리즘이 되고 비밀번호의 길이가   
> **하나씩 길어질때마다 소요되는 시간이 기하급수적으로 늘어나게됨**

**Example**  

![Factorial](https://miro.medium.com/v2/resize:fit:1200/format:webp/1*cYlZp9gnBPKKiKpJ8r5qGQ.png)  

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)
```

### Factorial Time - O(n!)

**Example**

```python
def heap_permutation(data, n):
    if n == 1:
        print(data)
        return
    
    for i in range(n):
        heap_permutation(data, n - 1)
        if n % 2:
            data[0], data[n - 1] = data[n - 1], data[0]
        else:
            data[i], data[n - 1] = data[n - 1], data[i]
```
