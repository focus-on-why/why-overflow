## 왜 Python에는 리스트(List)와 튜플(Tuple) 2개의 데이터 타입이 존재할까?

### 서론

`List`와 `Tuple`은 Python에서 많이 사용되는 데이터 타입이고, 둘 다 여러개의 데이터를 하나로 만들어주는 데이터 타입이다. 가장 많이 알고 있는 차이점이라고 한다면 “**List는 변경이 가능하지만, Tuple은 변경할 수 없다**" 일 것이다. 단지 이러한 이유만으로 Python 언어가 다른 데이터 타입을 만들었을까?

### 메모리 효율성

`List`는 변경이 가능하므로 Python은 List 객체가 생성된 후 크기를 확장해야 하는 경우에 대비하여 **추가 메모리 블록을 할당**한다고 한다. 반대로 `Tuple`은 변경할 수 없고 크기가 고정되어 있으므로 Python은 데이터에 필요한 **최소 메모리 블록만 할당**한다고 한다.

결론적으로 `Tuple`은 `List`보다 메모리 효율이 좋다는 뜻이다. </br>
아래 코드를 통해 동일한 값으로 List와 Tuple을 만들게 되면 메모리가 다른 것을 볼 수 있다.

```python
# 메모리 사이즈 테스트
import sys

test_list = list(range(100))
test_tuple = tuple(range(100))

print(sys.getsizeof(test_list))    # 904(bytes for the list object)
print(sys.getsizeof(test_tuple))   # 840(bytes for the tuple object)
```

그렇기 때문에 많은 수의 값들을 가진 Tuple과 List가 있다면 값 조회를 고려할 때는 Tuple이 약간 더 유리하다고 한다.

```python
# 값 조회 테스트
import time

test_list = list(range(100000))
test_tuple = tuple(range(100000))

list_start = time.time()
for l in test_list:
    data = test_list[20000]
list_time = time.time() - list_start

tuple_start = time.time()
for l in test_tuple:
    data = test_tuple[20000]
tuple_time = time.time() - tuple_start

print(list_time)  # time: 0.011872053146362305
print(tuple_time) # time: 0.009997844696044922
```

### 디버깅

디버깅과 관련하여 `List` 와 `Tuple`에서, `Tuple`은 불변성으로 인해 대규모 프로젝트에서 디버그하기가 더 쉽다고 한다.</br> 
`List`는 변경할 수 있지만 `Tuple`은 변경할 수 없으므로 Tuple을 더 쉽게 추적할 수 있기 때문이다. 

### 느낀점

간단하게 Python에서 List와 Tuple을 따로 만든 이유(?)를 알아봤다. 사실 튜플이 왜 존재하는지 알고 싶었다.

두 유형 모두 Python 데이터 타입이지만 선택시에 어떤 걸 사용하면 조금이라도 더 효율이 좋은지 알게 된 것 같다. 간단하게 요약하자면 “**변경을 하지 않는 데이터를 사용한다면 Tuple을 사용해 조금이라도 효율을 높이자**" 인 것 같다.

### 참고

- [List vs Tuple: Difference Between List and Tuple](https://www.upgrad.com/blog/list-vs-tuple/)
- [Python Tuples: When to Use Them Over Lists](https://towardsdatascience.com/python-tuples-when-to-use-them-over-lists-75e443f9dcd7)