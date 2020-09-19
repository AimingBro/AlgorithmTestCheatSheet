# 알고리즘 문제 풀이를 위한 Python

>  Pythonic way for algorithm problem solving

[🏠Home](https://github.com/batboy118/Study_Note)

[◀Previous page ](./README.md)

---

<!-- TOC -->

- [1. Python 기초](#1-python-기초)
- [2. 몫과 나머지 구하기](#2-몫과-나머지-구하기)
- [3. 10진수로 변환](#3-10진수로-변환)
- [4. 문자열 포맷팅](#4-문자열-포맷팅)
- [5. 소문자, 대문자, 알파벳, 숫자](#5-소문자-대문자-알파벳-숫자)
- [6. 정렬](#6-정렬)
- [7. 전치 행렬](#7-전치-행렬)
- [8. zip](#8-zip)
- [9. map](#9-map)
- [10. join](#10-join)
- [11. * 연산자](#11--연산자)
- [12. 곱집합](#12-곱집합)
- [13. 2차원 배열 => 1차원 배열](#13-2차원-배열--1차원-배열)
- [14. 순열, 조합, 멱집합](#14-순열-조합-멱집합)
- [15. 각 요소가 몇번 나왔는지 찾기](#15-각-요소가-몇번-나왔는지-찾기)
- [16. List comprehension](#16-list-comprehension)
- [17. for else](#17-for-else)
- [18. swap](#18-swap)
- [19. 이진 탐색](#19-이진-탐색)
- [20. 가장 큰 수, inf](#20-가장-큰-수-inf)
- [21. index와 함께 순회하기](#21-index와-함께-순회하기)
- [22. slice](#22-slice)
- [23. math 팩토리얼, 공약수, 올림, 내림, 절대값](#23-math-팩토리얼-공약수-올림-내림-절대값)
- [24. 아스키 코드](#24-아스키-코드)
- [25. 자료구조 : deque, heapq](#25-자료구조--deque-heapq)
- [26. 순서가 있는 dict](#26-순서가-있는-dict)
- [27. 재귀의 제한 늘리기](#27-재귀의-제한-늘리기)
- [28. 날짜 관련](#28-날짜-관련)
- [29. 부분집합 확인하기](#29-부분집합-확인하기)
- [30. append와 extend 차이](#30-append와-extend-차이)

<!-- /TOC -->

## 1. Python 기초

> 참고) [Python 3.6 Documentation](https://docs.python.org/3/index.html)와 [PEP](https://www.python.org/dev/peps/)

- [iterable](https://docs.python.org/3/glossary.html#term-iterable): 자신의 멤버를 한 번에 하나씩 리턴할 수 있는 객체입니다. list, str, tuple, dict 등이 여기에 속합니다.
- [sequence](https://docs.python.org/3/glossary.html#term-sequence): int 타입 인덱스를 통해, 원소에 접근할 수 있는 iterable 입니다. iterable의 하위 카테고리라고 생각하시면 됩니다. list, str, tuple이 여기 속합니다. ( dictionary는 다양한 타입을 통해 원소에 접근할 수 있기 때문에 sequence에 속하지 않습니다.)
- 탭 대신 space 4개
-  줄의 문자 길이 < 80
- 변수, 함수는 lowercase_underscore
- protected는 _leading_underscore
- private는 __double_leading_underscore
- 클래스명은 CapitalizedWord
- 상수는 ALL_CAPS
- if len(somelist)==0 대신 if not somelist

- ### 시간 복잡도

  List 연산

  | 연산  | 복잡도      |
  | ---- | ---- |
  | len(lst)       | O(1)     |
  | lst[i]        | O(1)   |
  | lst[i:j]      | O(n) |
  | item in lst | O(n) |
  | lst.count(item) | O(n)|
  | lst.index(item) | O(n) |
  | lst.append(item) | O(1) |
  | lst.pop(item) | O(1) |
  | lst.pop(0)    | O(n) |
  | del lst[i]    | O(n) |
  | lst.sort()    | O(nlogn) |
  | min(lst), max(lst) | O(n)  |
  | lst.reverse() | O(n)  |


- ### 입력

  input으로 받아도 되지만, sys.stdin이 더 빠르다.

  ```python
  #int형으로 입력
  import sys
  n = int(sys.stdin.readline())

  #한 줄에 여러가지 입력이 필요할 때
  import sys
  arr = sys.stdin.readline().split()

  #한 줄에 여러 가지 입력을 받은 후, int 객체로의 형 변환이 필요할 때.
  import sys
  arr = list(map(int, sys.stdin.readline().split()))

  #한 줄에 여러 가지 입력을 받은 후, 함수를 이용한 데이터 조작이 필요할 때.
  import sys
  arr = [int(x) * 2 + 1 for x in sys.stdin.readline().split()]
  ```

- ### 출력

  print로 출력해도 되지만, sys.stdout이 더 빠르다.

  print는 자동개행이지만, sys.stdout은 자동개행되지 않는다.

  ```python
  #print와
  import sys
  print(1)
  sys.stdout.write(str(1) + '\n')
  ```

- ### 초기화된 리스트 만들기

  ```python
  # 0으로 초기화된 1차월 list
  list = [0 for i in range(n)]

  # 0으로 초기화된 2차원 list
  matrix = [[0 for col in range(n)] for row in range(n)]
  ```

- ### deepcopy (재귀적으로 수행)

  ```python
  import copy
  List=['high',['low']]

  cp=copy.copy(List) #얕은복사
  dcp=copy.deepcopy(List) #깊은복사
  ```

- ### 1단계 deepcopy

  ```python
  lst = [1,2,3,4,5];
  lst_copy = [i for i in lst]
  ```

## 2. 몫과 나머지 구하기

- divmod와 unpacking(*) 이용하기

  ```python
  a = 7
  b = 5
  print( *divmod(a, b) )
  ```

## 3. 10진수로 변환

- int함수를 이용하여 n진수를 10진수로 변경 가능

```python
num = '3212'
base = 5
answer = int(num, base)
```

## 4. 문자열 포맷팅

```python
s = "123"
n = 5

s.ljust(n) # 좌측 정렬 "123  " 반환
s.center(n) # 가운데 정렬 " 123 " 반환
s.rjust(5) # 우측 정렬 => "  123" 반환
s.rjust(5, "a") #"aa123" 반환
s.zfill(5) # 은 "00123" 반환
```

## 5. 소문자, 대문자, 알파벳, 숫자

- 모든 알파벳 출력하기

    ```python
    import string

    string.ascii_lowercase # 소문자 abcdefghijklmnopqrstuvwxyz
    string.ascii_uppercase # 대문자 ABCDEFGHIJKLMNOPQRSTUVWXYZ
    string.ascii_letters #대소문자 모두 abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ
    string.digits # 숫자 0123456789
    ```

- 소문자 => 대문자, 대문자 => 소문자, 반전

  ```python
  "abc".upper() #ABC
  "ABC".upper() #abc
  "aBc".swapcase() #AbC
  "abcde fghi".capitalize() # 'Abcde fghi'
  "abcde fghi".title() # 'Abcde Fghi'
  ```

- 소문자, 대문자, 숫자, 알파벳 판별

  ```python
  'abc'.islower() # True
  'aCc'.islower() # False
  'abC'.isupper() # False
  'ABC'.isupper() # True
  'aBC'.isalpha() # True
  'a1C'.isalpha() # False
  '123'.isdigit() # True
  '1a3'.isdigit() # False
  ```

## 6. 정렬

- sorted : 원본 유지

```python
list1 = [3, 2, 1]
list2 = sorted(list1)
```

- sort : 원본 변경

```python
list1 = [3, 2, 1]
list2 = [i for i in list1] # 또는 copy.deepcopy를 사용
list2.sort()
```

- 정렬 방식
  - `list.sort()` 는 리스트 내부에서 정렬 (`list.sort()` 는 반환 값 없음)
  -  `sorted()` 는 정렬된 값을 반환
- 정렬 가능 대상
  - `list.sort()` 는 **리스트 형**에 한해서만 동작
  - `sorted()` 는 **iterable(순회가능) 한 자료형**에 대해서 동작

- key parameter
  - 둘 다 `key` 파라미터를 비교 하는 기준으로 사용

  - key 파라미터는 `함수`여야 한다.

    ```python
    sorted("This is a test string from Andrew".split(), key=str.lower)
    ['a', 'Andrew', 'from', 'is', 'string', 'test', 'This']

    student_tuples = [
        ('john', 'A', 15),
        ('jane', 'B', 12),
        ('dave', 'B', 10),
    ]
    sorted(student_tuples, key=lambda student: student[2])
    # sort by age
    [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
    ```

    ```python
    class Student:
        def __init__(self, name, grade, age):
            self.name = name
            self.grade = grade
            self.age = age
        def __repr__(self):
            return repr((self.name, self.grade, self.age))

    student_objects = [
        Student('john', 'A', 15),
        Student('jane', 'B', 12),
        Student('dave', 'B', 10),
    ]
    sorted(student_objects, key=lambda student: student.age)
    # sort by age
    [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
    ```

  - key 파라미터에 operator 모듈의 `itemgetter`, `attrgetter`를 사용하면 더 쉽게 비교할 수 있다.

    ```python
    from operator import itemgetter, attrgetter

    sorted(student_tuples, key=itemgetter(2))
    [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]

    sorted(student_objects, key=attrgetter('age'))
    [('dave', 'B', 10), ('jane', 'B', 12), ('john', 'A', 15)]
    ```

  - operator 모듈 함수는 다중 수준의 정렬을 허용합니다. 예를 들어, 먼저 *grade*로 정렬한 다음 *age*로 정렬하려면, 이렇게 합니다:

    ```python
    sorted(student_tuples, key=itemgetter(1,2))
    [('john', 'A', 15), ('dave', 'B', 10), ('jane', 'B', 12)]
    ```

    ```python
    sorted(student_objects, key=attrgetter('grade', 'age'))
    [('john', 'A', 15), ('dave', 'B', 10), ('jane', 'B', 12)]
    ```

  - 자주 쓰이지는 않지만, methodcaller()는 특정한 이름을 가지는 메서드를 호출시켜 준다.

    ```python
    from operator import methodcaller
    f = methodcaller('name')
    class B():
    	def name(self):
    		print("test")

    b = B()
    f(b)
    #test
    ```

- 오름차순 / 내림차순

  - [`list.sort()`](https://docs.python.org/ko/3/library/stdtypes.html#list.sort)와 [`sorted()`](https://docs.python.org/ko/3/library/functions.html#sorted)는 모두 불리언 값을 갖는 *reverse* 매개 변수를 받아들입니다. 내림차순 정렬을 지정하는 데 사용됩니다. 예를 들어, 학생 데이터를 역 *age* 순서로 얻으려면, 이렇게 합니다:

    ```python
    >>> sorted(student_tuples, key=itemgetter(2), reverse=True)
    [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
    ```

    ```python
    >>> sorted(student_objects, key=attrgetter('age'), reverse=True)
    [('john', 'A', 15), ('jane', 'B', 12), ('dave', 'B', 10)]
    ```

- Stable

  - 정렬은 stable을 지원한다.

## 7.  전치 행렬

- 파이썬스럽지 않은 코드

```python
def solution(mylist): # mylist = [ [1,2,3], [4,5,6], [7,8,9] ]
    answer = []
    for i in range(len(mylist)):
        answer.append([])
        for j in range(len(mylist[0])):
            answer[i].append(mylist[j][i])
    return answer
```

- zip과 unpacking을 이용한 코드

```python
mylist = [ [1,2,3], [4,5,6], [7,8,9] ]
new_list = list(map(list, zip(*mylist)))
```

> zip(*mylist)는 zip<1,4,7>, zip<2,5,8>, zip<3,6,9>를 만들어 낸다. (같은 index의 요소들을 묶음)
>
> map(list, zip(*mylist)) => [1,4,7] , [2,5,8], [3,6,9]

## 8. zip

> zip(*iterables)는 각 iterables 의 요소들을 모으는 이터레이터를 만듭니다.
>
> 튜플의 이터레이터를 돌려주는데, i 번째 튜플은 각 인자로 전달된 시퀀스나 이터러블의 i 번째 요소를 포함합니다.

```python
mylist = [ 1,2,3 ]
new_list = [ 40, 50, 60 ]
for i in zip(mylist, new_list):
    print (i)

(1, 40)
(2, 50)
(3, 60)
```

- 리스트 두개로 딕셔너리 만들기

```python
animals = ['cat', 'dog', 'lion']
sounds = ['meow', 'woof', 'roar']
answer = dict(zip(animals, sounds)) # {'cat': 'meow', 'dog': 'woof', 'lion': 'roar'}
```

## 9. map

- map(함수, 이터러블);

  ```python
  list1 = ['1', '100', '33']
  list2 = list(map(int, list1)) #[1, 100, 33]
  ```

  list1의 모든 숫자에 int()를 적용

## 10. join

- join : 문자열 배열 또는 문자열 tuple을 join을 통해 하나로 묶을 수 있습니다.

  join은 string 클래스에 메서드이기 때문에, 주로 빈 string인 ''.join()형식으로 사용

  ```python
  my_list = ['1', '100', '33']
  answer = ''.join(my_list)
  ```

## 11. * 연산자

- *연산자로 문자열이나 리스트를 복제하여 더 길게 만들수 있다.

  ```python
  n = 3
  answer1 = 'abc'*n # 'abcabcabc'
  answer2= [123, 456]*n # [123, 456, 123, 456, 123, 456]
  ```

## 12. 곱집합

- 두 스트링 'ABCD', 'xy' 의 곱집합은 Ax Ay Bx By Cx Cy Dx Dy 입니다.

  ```js
  import itertools

  iterable1 = 'ABCD'
  iterable2 = 'xy'
  iterable3 = '1234'
  itertools.product(iterable1, iterable2, iterable3)
  ```

## 13. 2차원 배열 => 1차원 배열

파이썬의 다양한 기능을 사용하면, for 문을 사용하지 않고도 리스트를 이어붙일 수 있습니다.

```python
my_list = [[1, 2], [3, 4], [5, 6]]

# 방법 1 - sum 함수
answer = sum(my_list, [])

# 방법 2 - itertools.chain
import itertools
list(itertools.chain.from_iterable(my_list))

# 방법 3 - itertools와 unpacking
import itertools
list(itertools.chain(*my_list))

# 방법4 - list comprehension 이용
[element for array in my_list for element in array]

# 방법 5 - reduce 함수 이용1
from functools import reduce
list(reduce(lambda x, y: x+y, my_list))

# 방법 6 - reduce 함수 이용2
from functools import reduce
import operator
list(reduce(operator.add, my_list))

# 방법 7 - numpy 라이브러리의 flatten 이용
import numpy as np
np.array(my_list).flatten().tolist()
```

## 14. 순열, 조합, 멱집합

```python
cc = [0 for i in range(100)]

def rec(depth, lst, res, tmp):
    if(depth == len(lst)):
        res.append([i for i in tmp])
        return
    for i in range(len(lst)):
        if cc[i] == 0 :
            cc[i] = 1;
            tmp.append(lst[i])
            rec(depth + 1, lst, res, tmp)
            tmp.pop()
            cc[i] = 0

def solution(mylist):
    answer = []
    mylist.sort()
    rec(0, mylist, answer, [])
    return answer
```

- ### 순열, 조합

  ```python
  import itertools

  pool = ['A', 'B', 'C']
  print(list(map(''.join, itertools.permutations(pool)))) # 3개의 원소로 수열 만들기
  print(list(map(''.join, itertools.permutations(pool, 2)))) # 2개의 원소로 수열 만들기
  ```

  [itertools.permutation](https://docs.python.org/3/library/itertools.html#itertools.permutations)과  [itertools.combinations](https://docs.python.org/3/library/itertools.html#itertools.combinations)의 사용법은 비슷하다.

  ```python
  # permutations : 순열, 중복 허용 X
  # product : 순열, 중복 허용 O
  # combinations : 조합, 중복 허용 X
  # combinations_with_replacement : 조합, 중복 허용 O
  from itertools import permutations, combinations, product, combinations_with_replacement

  p = list(permutations(lst, 2))  # 순열 : n개 중 2개 선택
  p = list(product(lst, repeat=2)) # 순열 : n개 중 2개 선택, 중복 허용
  p = list(combinations(lst, 2)) # 조합 : n개 중 2개 선택
  p = list(combinations_with_replacement(lst, 2)) # 조합 : n개 중 2개 선택, 중복허용
  ```

- ### PowerSet(멱집합)

  itertools 이용한 방법

  ```python
  from itertools import chain, combinations

  def powerset(iterable): #range(1, len(s) 빈 집합을 제외한 모든 부분집합
      "powerset([1,2,3]) --> (1,) (2,) (3,) (1,2) (1,3) (2,3) (1,2,3)"
      s = list(iterable)
      return chain.from_iterable(combinations(s, r) for r in range(1, len(s)+1))

  def powerset(iterable): #range(0, len(s)빈 집합 포함 모든 부분집합
      "powerset([1,2,3]) --> (1,) (2,) (3,) (1,2) (1,3) (2,3) (1,2,3)"
      s = list(iterable)
      return chain.from_iterable(combinations(s, r) for r in range(0, len(s)+1))

  #모든 경우를 보지 않고 만족하는게 있는지만 체크할 때는 제너레이터의 yield 를 활용하여 이터레이터 형식을 잘 활용하는 것이 좋다.
  #next(p)활용
  #하나씩 확인하는 방법
  p = powerset(lst);
  for l in p :
      #...

  p = list(powerset(lst))
  ```

  bit마스킹 이용방법

  ```python
  def powerset(s):
  	masks = [ 1 << i for i in range(len(s)) ]
  	for i in range( 1 << len(s) ):
  		yield [ss for ss,mask in zip(s,masks) if mask & i ]

  #모든 경우를 보지 않고 만족하는게 있는지만 체크할 때는 제너레이터의 yield 를 활용하여 이터레이터 형식을 잘 활용하는 것이 좋다.

  #하나씩 확인하는 방법
  p = powerset(lst);
  for l in p :
      #...

  #모든 요소 출력하는 방법
  p = list(powerset(lst))
  ```

## 15. 각 요소가 몇번 나왔는지 찾기

- collections모듈의 Counter 클래스 사용

```python
import collections import Counter
my_list = [1, 2, 3, 4, 5, 6, 7, 8, 7, 9, 1, 2, 3, 3, 5, 2, 6, 8, 9, 0, 1, 1, 4, 7, 0]
answer = Counter(my_list)

print(answer.most_common()) # Counter.most_common(x)는 초가장 많이 등장한 키를 x개 반환한다.
print(answer[1]) # = 4
print(answer[3])  # = 3
print(answer[100]) # = 0
```

## 16. List comprehension

[Displays for lists, sets and dictionaries](https://docs.python.org/3/reference/expressions.html?highlight=list comprehension#displays-for-lists-sets-and-dictionaries)

```python
mylist = [3, 2, 6, 7]
answer = [ i**2 for i in mylist if i %2 == 0]
```

- 컴프리헨션이 클 때는 제너레이터 사용하기

컴프리헨션은 새 리스트를 통째로 생성함 => 메모리 많이 필요

따라서 크기가 클 때는 이터레이터를 사용하는 제너레이터를 사용하자.

```python
mylist = [3, 2, 6, 7]
answer = (i**2 for i in mylist if i %2 == 0)
```

## 17. for else

for문에서 어떤 조건을 만족하는 경우를 찾았을 때, 보통 flag를 이용한 방법으로 문제를 많이 풀지만 파이썬에서는 for else를 사용하면 flag가 필요 없다.

for문을 다 돌고도 break;가 발생하지 않았다면, else 구문이 실행이 된다.

```python
import math

numbers = [int(input()) for _ in range(5)]
multiplied = 1
for number in numbers:
    multiplied *= number
    if math.sqrt(multiplied) == int(math.sqrt(multiplied)):
        print('found')
        break
else:
    print('not found')
```

> 위 코드는, 리스트에 속한 숫자들을 차례대로 계속해서 곱했을 때 제곱에 해당하는 수가 한번이라도 나오면 found, 아니면 not found를 출력

## 18. swap

```python
a = 3
b = 'abc'

a, b = b, a
```

## 19. 이진 탐색

- bisect 모듈

  `bisect` 모듈은 **이미 정렬되어 있는 `list`의 정렬 상태를 유지하기 위해** 사용되는 모듈입니다. 이를 이용해서, 기존에 있는 `list`의 정렬 상태를 유지 할 수 있고, 이를 응용해서 `Binary Search` 또한 구현할 수 있습니다.

  - 삽입 되어야 하는 `index` 찾기

  ```python
  import bisect
  arr = [1, 2, 3, 3, 4, 5]

  print(bisect.bisect_left(arr, 6))   # 6이 들어가야 하는 Index인 6을 반환
  print(bisect.bisect_right(arr, 6))  # arr에 6이 없기 때문에 위와 똑같은 값을 반환한다.

  print(bisect.bisect_left(arr, 3))   # 중복 되는 값 제일 왼쪽, 2를 반환한다.
  print(bisect.bisect_right(arr, 3))  # 중복 되는 값 제일 오른쪽 + 1, 4를 반환한다.

  bisect.insort_left(arr, 3)  # 중복 되는 값 왼쪽에 삽입
  bisect.insort_right(arr, 3) # 중복 되는 값 오른쪽에 삽입

  print(arr)
  ```

  - `Binary Search` 구현

  ```python
  from bisect import bisect_left
  arr = [1, 2, 3, 3, 4, 5]

  def bs(arr, x):
      i = bisect_left(arr, x)             # 들어가야 하는 '제일 왼쪽' index 반환
      if i != len(arr) and arr[i] == x:   # 들어가야 하는 index가
          return i                        # 마지막 index + 1 이라면, arr에 x가 없는 것
      else:                               # arr[i] == x가 아니라면, arr에 x가 없는 것
          return -1

  a  = [1, 2, 4, 4, 8]
  x = 4
  res = bs(a, x)
  if res == -1:
      print(x, "는 없습니다!")
  else:
      print("첫번째", x, "가 등장한 위치는", res)
  ```

## 20. 가장 큰 수, inf

inf는 어떤 숫자와 비교해도 무조건 크다고 판정됩니다.

```python
min_val = float('inf')
min_val > 10000000000
```

`inf`에는 음수 기호를 붙이는 것도 가능합니다.

```python
max_val = float('-inf')
```

## 21. enumerate : index함께 사용하기

- enumerate를 사용

```python
t = [1, 5, 7, 33, 39, 52]
for p in enumerate(t):
    print(p)

#(0, 1)
#(1, 5)
#(2, 7)
#(3, 33)
#(4, 39)
#(5, 52)

for i, v in enumerate(t):
    print("index : {}, value: {}".format(i,v))

#index : 0, value: 1
#index : 1, value: 5
#index : 2, value: 7
#index : 3, value: 33
#index : 4, value: 39
#index : 5, value: 52
```

- range보다 enumerate 이용하는 것이 좋다.

```python
# range 사용하는 방법
for i in range(len(flavor_list)):
    flavor = flavor_list[i]
    print('%d %s' % (i+1, flavor))

# enumerate 사용하는 방법
for i, flavor in enumerate(flavor_list, 1): #1부터 enum 시작
    print('%d: %s' % (i, flavor))
```

## 22. slice

- **시퀀스객체[시작인덱스:끝인덱스:증가폭]**

  ```python
  a = [0, 10, 20, 30, 40, 50, 60, 70, 80, 90]
  a[2:8:3]    # 인덱스 2부터 3씩 증가시키면서 인덱스 7까지 가져옴
  #[20, 50]
  ```

## 23. math 팩토리얼, 공약수, 올림, 내림, 절대값

```python
import math

print(math.factorial(5))    # 5! = 120 반환
print(math.gcd(40, 30))     # 40과 30의 공약수 반환
print(math.floor(2.5))		# 2.5의 내림 반환 (2)
print(math.ceil(2.5))		# 2.5의 올림 반환 (3)
print(math.fabs(-5))		# -5의 절댓값 반환 (5)
```

## 24. 아스키 코드

```python
chr(103) #'g'
ord("A") # 65
```

## 25. 자료구조 : deque, heapq

- ### deque

   `deque`는 양방향 큐로, **큐**로도 사용 가능하고, **스택**으로도 사용 가능하고, **양방향 큐**로도 사용 가능합니다. `collections` 모듈에 있습니다.

```python
from collections import deque

# 스택
append(), pop()

# 큐
appendleft(), pop(), append(), popleft()

# deque 확장
extend(), extendleft()

# list 처럼 사용, remove는 왼쪽부터 제거
insert(), remove()
#dq.insert(0, 'K')

# 내용 반전
reverse()
```

- ### heapq

  `heapq` 모듈은 일반 `list`를 `heap`처럼 사용할 수 있도록 도와주는 모듈입니다. 기본적으로 `Python`에 내장 되어 있는 `heapq` 모듈은 **최소 힙**을 위해 만들어 졌기 때문에 **최대 힙**을 만들기 위해서는 데이터의 처리가 필요합니다. (숫자라면 -를 붙이는 방법이 대표적입니다.) **우선순위 큐**를 만드는 데에 주로 사용합니다. 삽입, 제거의 시간 복잡도는 **O(log n)** 입니다.

- 아무 것도 없는 `list` 객체에서 `heap` 사용하기.

```python
import heapq

h = []
heapq.heappush(h, 3)	# 첫 번째 파라미터에는 list 객체가
heapq.heappush(h, 9)	# 두 번째 파라미터에는 삽입하려는 객체가 들어간다.
heapq.heappush(h, 7)
heapq.heappush(h, 8)
heapq.heappush(h, 5)
heapq.heappush(h, 1)

for _ in range(6):
	print(heapq.heappop(h))	# 작은 값부터 출력된다.
```

- **최대 힙** 만들기 : -를 곱해서 넣어주고 사용할 때 다시 -를 곱해준다.

```python
import heapq

h = []
heapq.heappush(h, -3)	# 첫 번째 파라미터에는 list 객체가
heapq.heappush(h, -9)	# 두 번째 파라미터에는 삽입하려는 객체가 들어간다.
heapq.heappush(h, -7)	# 단, 원래 넣으려는 값에 -를 붙여주고
heapq.heappush(h, -8)	# 출력시에도 -을 붙여준다.
heapq.heappush(h, -5)
heapq.heappush(h, -1)

for _ in range(6):
	print(-heapq.heappop(h))	# 큰 값부터 출력된다.
```

- 기존에 있는 list 객체로 **힙 정렬** 만들기

```python
import heapq

h = [3, 9, 1, 4, 2]
heapq.heapify(h)	# 파라미터로 list 객체를 받는다.

for _ in range(6):
	print(heapq.heappop(h))	# 작은 값부터 출력된다.
```

## 26. 순서가 있는 dict

```python
from collections import OrderedDict

# 인자 X 혹은 last=true 라고 주면 마지막 값을 리턴하고 제거
ordered_dict.popitem()

# last=False 라고 주면 첫번째 값을 리턴하고 제거
ordered_dict.popitem(last=False)

# 한꺼번에 딕셔너리 생성
od = OrderedDict.fromkeys('red')
#OrderedDict([('r', None), ('e', None), ('d', None)])

# 'r'키값을 제일 마지막으로 이동
od.move_to_end('r')

# 'r'키값을 제일 처음으로 이동
od.move_to_end('r', last=False)
```

## 27. 재귀의 제한 늘리기

```python
import sys
sys.setrecursionlimit(10**6)
```

## 28. 날짜 관련

```python
from datetime import datetime, timedelta
dt = datetime.strptime('2018/02/22 10:56','%Y/%m/%d %H:%M:%S.%f')
another_year = timedelta(weeks=40, days=84, hours=23, minutes=50, seconds=600)
d.strftime('%Y-%m-%d %H:%M:%S')  # 날짜/시간 객체를 문자열로 만들기
```

## 29. 부분집합 확인하기

```python
a = [1,2,3]
b = [2,3]
s1 = set(a)
s2 = set(b)
if s1 ==s1.intersection(s2) :
    print("a는 b의 부분집합입니다!")
elif s2==s1.intersection(s2):
    print("b는 a의 부분집합입니다")

#b는 a의 부분집합입니다
```

## 30. append와 extend 차이

```python
#append - 리스트에 요소 추가
x = [1, 2, 3]
x.append([4, 5])# -> append의 object를 통째로 맨 뒤에 추가
#결과 :
#[1, 2, 3, [4, 5]]


#extend - 리스트에 같은 배열로 추가(확장)
x = [1, 2, 3]
x.extend([4, 5]) # - extend의 object 의 엘레멘트들을 추가
#결과 :
#[1, 2, 3, 4, 5]
```

## 31. 문자열 수정, index

`str.replace(old , new)` : str속의 문자열중, old를 찾아서 new로 바꿈

```python
string = "i am Jason"
new_string = string.replace("i am", "You are")
print(new_string)
```

`str.find(찾을문자)`

`str.index(찾을문자)`

```python
string = "i am Jason"
print(string.index("am"))
print(string.find("Jason"))
#출력결과
2
5
```

> find와 index는 둘다 같은 기능을 하지만, 차이점이 있다.
>
> string에 포함되지 않은 문자를 찾게되면 **index()는 에러**를 발생하지만, find()는 -1을 리턴
>
> 그리고 **index**()는 **list에서도 사용이 가능**하지만 **find**()는 **문자열에서만** 사용 가능합니다.

- 역순으로 만들기

  ```python
  #슬라이싱 [::-1]
  string = "i am happy"
  print(string[::-1])

  #출력결과
  #yppah ma i

  #reversed()
  string = "i am happy"
  print("".join(reversed(string))

  #출력결과
  #yppah ma i
  ```

  - 그냥 reversed(string)을 출력하게되면, 메모리값이 나오게됨
