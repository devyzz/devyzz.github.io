---
layout: post
title: 이어드림스쿨 | 힙 (실습 해설)
categories: 
  - learning
  - courses 
tags : heap
excerpt_separator: <!--more-->
hide_last_modified: true
sitemap: true
---
* toc
{:toc .large-only}
이어드림스쿨  자료구조 강의 중 힙에 관한 내용과 실습 코드들을 정리한 내용입니다.

힙 자료구조에 대한 다양한 실습을 수행하며 사용 된 python의 heapq 모듈에 대해 추가적으로 정리하였습니다.

<!--more-->

## 힙

### 최소 힙 구현하기

```python
class PriorityQueue:
    def __init__(self):
        self.data = [0]

    def push(self, value):

        self.data.append(value)
        index = len(self.data) - 1

        while index != 1: # 마지막으로 삽입한 값이 루트 노드가 되면 반복문 종료
            if self.data[index//2] > self.data[index] : # 부모의 value가 자신보다 크다면
                tmp = self.data[index]
                self.data[index] = self.data[index//2]
                self.data[index//2] = tmp

                index = index // 2 # 부모 노드로 올라갔으므로, index를 바꿈
            else:
                break #완전 이진 트리 조건을 만족하므로 그냥 break

    def top(self):
        if len(self.data) == 1:
            return -1 # 아무것도 없는 빈 트리이므로 -1 반환
        else:
            return self.data[1]

    def pop(self):
        if len(self.data) == 1:
            return # pop을 처리하지 않고 return

        # 마지막 노드를 루트 노드 자리로 이동한다.
        self.data[1] = self.data[-1]
        self.data.pop()

        index = 1

        while True:
            '''
            priority 현재 노드(index)가 두 자식 중 누구랑 자리를 바꿔야할 지 선택하기 위해 사용하는 변수
            자식이 없다면 바꿀 필요 없으므로 break
            왼쪽 자식만 있다면 왼쪽 자식과 자리를 바꿔야하므로 priority = 왼쪽자식
            자식이 모두 있다면 둘 중 더 작은 자식과 자리를 바꿔야 하므로, 작은쪽의 인덱스를 priority에 저장
            --> 자식과 루트가 자리를 바꾸므로 더 작은 자식과 루트가 바뀌어야 나머지 자식도 루트와 비교했을 때 힙조건을 만족!!!
            '''
            priority = -1
            # 1. 자식이 없는 경우
            if len(self.data) - 1 < index * 2: # 전체 길이가 왼쪽자식보다 작으면 왼쪽자식이 없다는 거임
                break
            # 2. 왼쪽 자식만 있는 경우
            elif len(self.data) - 1 < index * 2 + 1: # 왼쪽 분기 통과+오른쪽 자식의 인덱스보다 작음 == 왼쪽 자식만 존재
                priority = index * 2
            # 3. 왼/오 자식이 다 있는 경우
            else:
                if self.data[index*2] < self.data[index*2 + 1]: #왼쪽 자식이 오른쪽 자식보다 값이 작다면
                    priority = index * 2            # prioirty를 왼쪽으로 옮겨줌
                else:
                    priority = index * 2 + 1        # 왼쪽 자식이 오른쪽 자식보다 크다면 priority를 오른쪽으로 옮김


            if self.data[index] > self.data[priority]:
                temp = self.data[index]
                self.data[index] = self.data[priority]
                self.data[priority] = temp
                index = priority
            else:
                break
```

### 최대 힙 구현하기

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.data = [0]

    def push(self,value):
        heapq.heappush(self.data, -value)   # 부호를 반전시켜 넣음

    def pop(self):
        if len(self.data) > 0:
            heapq.heappop(self.data)

    def top(self):
        if len(self.data) > 0:
            heapq.heappop(self.data)
```

### ✅ python - heapq

파이썬 표준 라이브러리로 제공되는 힙 자료구조를 위한 모듈. 기본적으로 최소 힙으로 동작하며, 가장 작은 원소가 루트(리스트의 0번 index)에 존재한다. 특징은 다음과 같다.

- 리스트를 기반으로 동작한다
- 자동으로 정렬되지 않는다. 
- 최소 힙이 기본이지만 최대 힙일 경우 `-value`로 구현이 가능하다.

#### `heapq.heappush(heap, item)`

힙속성을 유지하며 항목을 힙에 삽입한다.

```python
import heapq

heap = []
heapq.heappush(heap, 5)
heapq.heappush(heap, 1)
heapq.heappush(heap, 7)

print(heap)  # [1, 5, 7]
```

#### `heapq.headpop(heap)`

힙에서 가장 작은 원소를 제거하고 반환한다. 즉, 루트를 반환하고 힙 구조로 재정렬한다.

```python
print(heapq.heappop(heap))  # 1
print(heap)  # [5, 7]
```

#### `heapq.headpushpop(heap, item)`

`item`을 삽입한 후, 가장 작은 값을 제거하고 반환한다. (삽입한 값이 제일 작을 경우, 넣자마자 제거 됨)

```python
heap = [2, 4, 6]
heapq.heapify(heap)

res = heapq.heappushpop(heap, 1)
print(res)     # 1
print(heap)    # [2, 4, 6]
```

#### `heapq.heapreplcae(heap,item)`

힙의 가장 작은 항목을 제거하고 `item`을 삽입한다. 제거가 먼저 일어나므로 item은 무조건 삽입된다.<br>headpop() &rarr; headpush() 를 사용하는 것과 같은 효과를 보이지만, heapreplace가 성능적으로 더 우수하다.

```python
heap = [2, 4, 6]
heapq.heapify(heap)

res = heapq.heapreplace(heap, 3)
print(res)     # 2
print(heap)    # [3, 4, 6]
```

#### `heap.heapify(x)`

리스트 x를 힙구조로 변환한다.

```python
arr = [4, 1, 7, 3, 8, 5]
heapq.heapify(arr)
print(arr)  # [1, 3, 5, 4, 8, 7]
```

#### `heapq.nlargest(n, iterable, key=...)`

iterable객체에서 n개의 가장 큰 원소를 반환한다.

```python
nums = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
print(heapq.nlargest(3, nums))  # [9, 8, 7]
```

#### `heapq.nsmallest(n, iterable, key=...)`

iterable객체에서 n개의 가장 작은 원소를 반환한다.

```python
nums = [1, 3, 5, 7, 9, 2, 4, 6, 8, 0]
print(heapq.nsmallest(3, nums))  # [0, 1, 2]
```

### 절대값 힙 구현하기

절대값이 작을수록 우선순위가 높은 경우 (절대값이 같은 값이 2개 이상이면 가장 작은 수의 우선순위가 더 높음)

```python
import heapq
class PriorityQueue:

    def __init__(self):
        self.data = []

    def push(self, value):
        heapq.heappush(self.data, (abs(value), value))  # 절대값, 원래값을 튜플형태로 입력함

    def pop(self):
        if len(self.data) > 0:
            heapq.heappop(self.data)

    def top(self):
        if len(self.data) == 0:
            return -1
        else:
            return self.data[0][1]
```

###  힙 정렬 구현하기

```python
import heapq

class PriorityQueue:
    def __init__(self):
        self.data = []

    def push(self,value):
        heapq.heappush(self.data, value)

    def pop(self):
        if self.data:
            return heapq.heappop(self.data)

    def top(self):
        if self.data:
            return self.data[0]
        return -1

def heapSort(items):
    result = []

    pq = PriorityQueue()

    for item in items:
        pq.push(item)

    for i in range(len(items)):
        result.append(pq.pop())

    return result
```

### 점토 놀이

```python
# 엘리스씨는 가장 적은 힘을 사용하여 주어진 모든 점토를 합치고 싶어졌습니다.
# 엘리스씨를 도와 n개의 점토를 하나의 덩이로 합치기 위해 필요한 힘의 크기의 합의 최솟값을 구하는 프로그램을 작성하세요.

'''
4
1 5 7 3
'''
import heapq

#구현
def getMinForce(weights):
    '''
    n개의 점토를 하나로 합치기 위해 필요한 힘의 합의 최솟값을 반환하는 함수
    '''
    heapq.heapify(weights)  # weights를 최소 힙으로 변환
    result = 0

    while len(weights) > 1:
        # 가장 가벼운 두 개를 꺼내서 합친다
        x = heapq.heappop(weights)
        y = heapq.heappop(weights)
        force = x + y
        result += force
        heapq.heappush(weights, force)  # 합친 점토를 다시 넣음

    return result

#실행
n = int(input())
weights = list(map(int, input().split()))
print(getMinForce(weights))
```

### 중간값 찾기

```python
# n개의 숫자가 차례대로 주어질 때, 매 순간마다 “지금까지 입력된 수 중에서 중간값”을 반환하는 프로그램을 작성하세요.
'''
10
1 2 3 4 5 6 7 8 9 10
-->
1 1 2 2 3 3 4 4 5 5
'''

import heapq

#구현
def find_mid(numbers):
    left = []   # 최대 힙 (중간값 이하)
    right = []  # 최소 힙 (중간값 초과)

    result = []

    for number in numbers:
        #왼쪽 힙은 최대 힙 -> 파이썬은 최소 힙만 제공하므로 음수로 넣음
        if not left or number <= -left[0]:
            heapq.heappush(left, -number)
        else:
            heapq.heappush(right, number)

        #힙 크기 맞추기 (왼쪽이 항상 같거나 1개 더 많게)
        if len(left) > len(right) + 1:
            heapq.heappush(right, -heapq.heappop(left))
        elif len(right) > len(left):
            heapq.heappush(left, -heapq.heappop(right))

        # Step 3. 중간값은 항상 왼쪽 힙의 루트
        result.append(-left[0])

    return result

#실행
n = int(input())
numbers = list(map(int, input().split()))
print(*find_mid(numbers))
```

