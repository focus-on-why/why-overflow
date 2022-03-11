## 서론
- 누군가 작성한 파이썬 코드를 읽다가, 함수에 넘어오는 파라미터나 클래스 속성이 어떤 자료형인지 몰라 곤란한적 있으신가요?  
- 큰 규모의 프로젝트를 진행하며 타입의 오사용으로 인한 버그를 경험해보신 적이 있으신가요?
  
**파이썬 Type Annotations**는 이럴 때를 대비하여 자료형을 '표시'하는 문법입니다. 이것은 무엇이고, 어떻게 사용하는 것인지 자세히 알아보도록 하겠습니다. 
## 파이썬 Type Annotations?
C, Java 등과 같은 정적 프로그래밍 언어에서 데이터 유형은 필수적으로 선언되어야 하며, 선언되지 않았을 경우 컴파일조차 되지 않습니다.
- Java
```java
>>> int a = 10  //  
>>> b = 20  // ! 컴파일 에러 발생
```

반면, 동적 프로그래밍 언어인 파이썬에서는 데이터 유형을 명시적으로 지정하지 않아도, 코드가 실행될 때 파이썬 인터프리터(interpreter)가 타입을 (type)을 자동으로 추론하여 지정해줍니다.
- Python
```python
>>> a = 10
>>> print(type(a))
<class 'int'>
```
따라서 동적 프로그래밍 언어는 타입에 자유로운 유연한 코딩이 가능하며, 깔끔한 프로그램을 작성할 수 있습니다. 

하지만 프로젝트의 규모가 커질수록 이러한 파이썬의 동적인 특성은 엄격하게 타입이 명시되는 정적 프로그래밍 언어에 비해 치명적인 버그로 이어질 확률이 높아지게 되며, 상대적으로 다루기 어려워지는 경향이 있습니다. 
또한 팀으로 협업하여 코드 작성을 할 때, 변수 등의 타입을 명확히 확인할 수 없어 커뮤니케이션에 방해를 주기도 합니다.

이러한 문제를 해결하기 위해 파이썬에서는 타입에 대한 힌트(Type Hinting)을 제공하는 **Type Annotations**을 제공합니다.


## 파이썬 Type Annotations 사용하기
파이썬은 3.5버전부터 'Type Annotations'기능과 함께 `typing` 내장 패키지를 추가하여 지원하기 시작하였습니다. 


> 파이썬에서의 Annotations는 정적 언어에서와 같은 강제적인 타입 체킹이 아닙니다. 다시 말해, 그저 타입에 대한 힌트(Type Hinting)를 제공하여 우리가 작성한 코드를 다른 개발자가 읽기 수월하게 해주고, 우리가 사용하는 개발 도구가 오류 없이 활용될 수 있게 도와주는 역할만을 하고 있습니다. 
이로 인해 우리는 동적 프로그래밍 언어의 장점을 잃지 않으며 타입에 대한 힌트를 제공할 수 있습니다. 

### 사례
다음과 같은 코드가 있습니다. 
언뜻 보기엔 매우 심플하게 구현된 코드 같지만, 코드를 리뷰하는 입장에선 잘 읽히지 않을 수 있습니다.
```python
# Basic code

def sgd(P, Q, b, b_u, b_i, samples, learning_rate, regularization):
    for user_id, item_id, rating in samples:
        predicted_rating = b + b_u[user_id] + b_i[item_id] + P[user_id, :].dot(Q[item_id, :].T)
        error = (rating - predicted_rating)

        b_u[user_id] += learning_rate * (error - regularization * b_u[user_id])
        b_i[item_id] += learning_rate * (error - regularization * b_i[item_id])

        P[user_id, :] += learning_rate * (error * Q[item_id, :] - regularization * P[user_id,:])
        Q[item_id, :] += learning_rate * (error * P[user_id, :] - regularization * Q[item_id,:])
```

  
다음은 같은 코드에 `doc string`과 `Type Annotations`를 추가한 코드입니다.   
코드 길이는 훨씬 더 길어졌지만 앞선 예시보다 훨씬 더 읽기 수월해졌으며, 재사용하기에도 용이해진 모습을 볼 수 있습니다.
```python
# Add doc string & type annotations

def sgd(
    P: np.ndarray,
    Q: np.ndarray,
    b: float,
    b_u: np.ndarray,
    b_i: np.ndarray,
    samples: List[Tuple],
    learning_rate: float,
    regularization: float
) -> None:
    """
    MF 모델의 파라미터를 업데이트하는 SGD
    
    :param P: (np.ndarray) 유저의 잠재 요인 행렬. shape: (유저 수, 잠재 요인 수)
    :param Q: (np.ndarray) 아이템의 잠재 요인 행렬. shape: (아이템 수, 잠재 요인 수)
    :param b: (float) 글로벌 bias
    :param b_u: (np.ndarray) 유저별 bias
    :param b_i: (np.ndarray) 아이템별 bias
    :param samples: (List[Tuple]) 학습 데이터 (실제 평가를 내린 데이터).
                    (user_id, item_id, rating) tuple을 element로 하는 list
    :param learning_rate: (float) 학습률
    :param regularization: (float) l2 정규화 파라미터
    :return: None
    """
    for user_id, item_id, rating in samples:
        
        # predicted rating
        predicted_rating = b + b_u[user_id] + b_i[item_id] + P[user_id, :].dot(Q[item_id, :].T)
        
        # error
        error = (rating - predicted_rating)
        
        # Update bias
        b_u[user_id] += learning_rate * (error - regularization * b_u[user_id])
        b_i[item_id] += learning_rate * (error - regularization * b_i[item_id])
        
        # Update w
        P[user_id, :] += learning_rate * (error * Q[item_id, :] - regularization * P[user_id,:])
        Q[item_id, :] += learning_rate * (error * P[user_id, :] - regularization * Q[item_id,:])
```

### 변수에 Annotations 사용하기
그럼 이제 본격적으로 Annotations를 사용해보겠습니다.
변수에 Type Annotations를 사용하기 위해서는 다음과 같은 형식을 사용합니다.
```python
my_var: <type> = <value>
```
- 변수에 Annotation 적용 
  -  `str` `int` `list` `bool` `tuple` `dict`
```python
name: str = "Kim'  # str

age: int = 99  # age

friends: list = ['Kim', 'Lee', 'Park', 'Lim']  # list

is_male: bool = True  # bool

height_weight: tuple = (199, 99)  # tuple

abc: dict = {
  'a': 'A',
  'b': 'B', 
  'c': 'C'
}  # dict

```

### 함수에 Annotations 사용하기
파이썬 함수에는 인자 타입과 반환타입에 대해 타입 힌트를 제공할 수 있습니다. 
```python
def my_func(param: <type>) -> <output-type>:
  # 내용
    return # 반환
```
- 함수에 Annotation 적용

```python
def plus(n1: int, n2: int) -> int:
	return n1 + n2
    
def plus_minus(n1: int, n2: int) -> list:
	return [n1 + n2, n1 - n2]

def print_message(msg: str) -> None:
	print(msg)
    
def mystery_combine(a: str, b: str, times: int) -> str:
    return (a + b) * times
```

### Typing 라이브러리
좀 더 복잡한 Type Annotation을 사용하기 위해서는 파이썬 표준 라이브러리인 `typing` 을 사용할 수 있습니다.

- **`List`, `Dict`, `Tuple`, `Set`**  
  : python 내장 자료 구조에 대한 타입을 명시할 수 있습니다.
```python
from typing import List, Dict, Tuple, Set

names: List[str] = ['Kim', 'Lee', 'Park']

heights: Dict[str, int] = {
    'Kim': 160, 'Lee': 170, 'Park': 165
}

score: Tuple[int, float, int] = (60, 62.5, 30)

names_startswith: Set[str] = {'K', 'L', 'P'}
```

- **Type Aliases**  
  : 어떠한 타입에 별칭을 만들어서 사용할 수 있습니다.
   - 아래 예시에서는 `Dict[str, int]` 형태의 'height_type'을 만들어 `print_heights()`의 인자 타입으로 사용하였습니다. 
```python
from typing import Dict

height_type = Dict[str, int]

def print_heights(heights: height_type) -> None:
    for name, height in heights.items():
        print(f'이름: {name} / 키: {height}')
```

- **Multiple Return Values**  
  : 함수에서 여러 타입 값들을 튜플로 반환하고 싶은 경우, 다음과 같이 사용할 수 있습니다.
```python
from typing import List, Tuple

heights: List[int] = [160, 170, 165]

def mean_heights(heights: List[int]) -> Tuple[str, int]:
    return ('mean', sum(heights) // len(heights))
```
  

- **Union**  
  : 힌트 내에 여러 개의 타입을 허용합니다.
```python
from typing import Union

def print_plus(n1: Union[int, float], n2: Union[int, float]]) -> None:
	print(n1 + n2)
```

- **Final**  
  : 상수에 대한 Type Annotations입니다

```python
from typing import Final

PI: Final[float] = 3.1415
```

- **Optional**  
  : 함수에서 None이 허용되는 매개변수에 대한 타입을 명시합니다.
```python
from typing import Optional

def say_hi(additional_msg: Optional[str] = None) -> None:
    if additional_msg is not None:
        print('hi' + additional_msg)
    else:
        print('hi')
```

- **Callable**  
  : 파이썬에서는 함수를 변수 안에 저장하거나 다른 함수의 인자로 넘기는 등의 일을 할 수 있습니다. `Callable`은 이러한 함수에 대한 Type을 명시합니다.
  - `Callable[[인자 타입(input)], 반환 타입(output)]`
  - 아래 예시에서는 단어를 concat시키는 `concat_words()`를 통해 1개의 str타입 인자를 받아 `print_words()`를 실행시킵니다.
```python
from typing import Callable

def print_words(concat_words: Callable[[str, str], str]) -> None:
    print(concat_words)
```



## 마무리
좋은 개발자는 '컴퓨터'가 아닌 '사람'이 이해할 수 있는 코드를 짠다고 말하곤 하죠. 클린 코드로 한 발짝 더 다가가기 위해 접근하기 쉽고 부담 없는 Type Annotations(Type Hinting)을 한 번 활용해 보는 것은 어떨까요?


## Reference
- https://docs.python.org/3/library/typing.html
- https://wikidocs.net/134883
- https://www.daleseo.com/python-type-annotations/
- https://towardsdatascience.com/type-annotations-in-python-d90990b172dc

## Further Reading
- [typing document](https://docs.python.org/3/library/typing.html)
- [mypy document](http://mypy-lang.org/)
: 타입을 체크하고 문제가 있다면 오류를 발생시키는 모듈(정적 타입 검사기)