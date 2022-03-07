## 서론

Python을 사용하다 보면 *(별표, Asterisk)을 많이 사용하는 것을 봤을 것이다.
곱셈 및 거듭제곱에도 사용하고, 리스트 타입의 데이터를 반복적으로 확장할 때도 사용한다.

```python
# 곱셈
>>> 2 * 2
4

# 거듭제곱
>>> 2 ** 3
8
```

```python
# 리스트 타입의 데이터를 반복적으로 확장
>>> num_list = [1,2,3] * 100
>>> num_tuple = (1,2,3) * 100
```

위의 작성한 예시 외에 `*`는 추가적으로 몇 가지의 역할을 더 하고 있는데, 이에 대해 간단하게 글을 작성해 보려고 한다.

## Unpacking 역할

`*`는 unpacking 역할을 한다는 것을 알고 있었는가? 
쉽게 말해서 괄호 안에 있던 데이터들을 풀어 각각으로 만들어 준다.

```python
>>> list_data = [1,2,3,4,5]

>>> print(list_data)
[1, 2, 3, 4, 5]

>>> print(*list_data)
1 2 3 4 5
```

tuple 타입 또한 괄호 안에 있던 데이터들을 풀어 각각으로 만들어 준다.

```python
>>> tuple_data = (1,2,3,4,5)

>>> print(tuple_data)
(1, 2, 3, 4, 5)

>>> print(*tuple_data)
1 2 3 4 5
```

dictionary 타입 또한 풀어보니 key 값들로 풀어지는 것을 확인할 수 있었다.

```python
>>> dict_data = {1: "name", 2: "age", 3: "height", 4: "weight"}

>>> print(dict_data)
{1: 'name', 2: 'age', 3: 'height', 4: 'weight'}

>>> print(*dict_data)
1 2 3 4
```

한 번도 사용해 보지 않았지만 다른 형태의 unpacking 이 한 가지 더 존재한다. 데이터를 다른 변수에 가변적으로 unpacking 하여 사용하는 형태이다. 

마지막 예시에서는 `*a`, `*b` 로 받는 부분들은 우변의 리스트 또는 튜플이 unpacking된 후, 다른 변수들에 할당된 값 외의 나머지 값들을 다시 하나의 리스트로 packing 한다. 

```python
>>> data = [1, 2, 3, 4, 5, 6]

# unpacking의 좌변은 리스트 또는 튜플의 형태를 가져야하므로 단일 unpacking의 경우 *a가 아닌 *a,를 사용
>>> *a, = data
>>> print(a)
[1, 2, 3, 4, 5, 6]

>>> *a, b = data
>>> print(a)
[1, 2, 3, 4, 5]
>>> print(b)
6

>>> a, *b, = data
>>> print(a)
1
>>> print(b)
[2, 3, 4, 5, 6]

>>> a, *b, c = data
>>> print(a)
1
>>> print(b)
[2, 3, 4, 5]
>>> print(c)
6
```

## 가변인자 *arg, **kwargs

파이썬을 사용하다 보면 함수 인자 값을 받는 부분에 `*args`, `**kwargs`를 사용한 코드를 볼 수 있다. 이는 가변 인자를 처리하는 표현으로 들어오는 인자의 개수를 모른다거나, 그 어떤 인자라도 모두 받아서 처리를 해야 할 때 주로 사용한다.

위치에 따라 정해지는 인자인 '**positional arguments'**는 `*`로 사용하고, 키워드(=이름)을 갖는 인자인 '**keyword arguments**'는 `**`로 사용한다.

### positional arguements

positional arguements 만 받을 때는 아래와 같이 사용한다.
함수 인자 값으로는 `*`을 붙인 인자명을 넣어준다면, 함수를 호출할 때는 필요한 인자를 넣어줄 수 있다.

```python
def print_info(*args):
	print(args)
	print(type(args)

print_info("insutance", 99, "Male")
>>> ('insutance', 99, 'Male')
>>> <class 'tuple'>
```

### keyword arguements

keyword arguements 만 받을 때는 아래와 같이 사용한다.
함수 인자 값으로는 `**`을 붙인 인자명을 넣어주고, **함수를 호출할 때 key 통해 값을 주어야** 한다.

```python
def print_info(**kwargs):
  print(kwargs)
	print(type(kwargs))
	print(kwargs["name"])
	print(kwargs["age"])
	print(kwargs["gender"])

print_info(name="insutance", age=99, gender="Male")

>>> {'name': 'insutance', 'age': 99, 'gender': 'Male'}
>>> <class 'dict'>
>>> insutance
>>> 99
>>> Male
```

### positional arguments & keyword arguments

positional arguments 와 keyword arguments를 모두 받을 때는 아래와 같이 사용한다.
`*args` 는 임의의 개수의 positional arguments를 받고, `**kwargs` 는 임의의 개수의 keyword arguments를 받는다. 이때 `*args`, `**kwargs` 형태로 가변 인자 받는 것을 packing이라고 한다.

```python
def print_info(*args, **kwargs):
    print(args)
    print(kwargs)

print_info("insutance", 99, gender="Male")
>>> ('insutance', 99)    # args
>>> {'gender': 'Male'}   # kwargs
```

이때 **positional arguments 가 keyword arguments 보다 무조건 앞에 위치**해야 한다. 그렇지 않으면 오류를 발생시킨다. 그 이유는 positional arguments의 경우 **생략이 불가능**하며 개수대로 정해진 위치에 인자를 전달해야 하지만, keyword arguments는 디폴트 값을 설정할 수 있어 **생략이 가능**하기 때문이다.

```python
def print_info(**kwargs, *args):
    print(args)
    print(kwargs)

print_info(name="insutance", 99, gender="Male")
>>> SyntaxError: invalid syntax
```

보통 `*args`, `**kwargs` 를 많이 사용하지만 사실 `args`, `kwargs` 말고 다른 것을 사용해도 된다. 하지만 `*args`, `**kwargs` 를 대부분 사용하니까 이를 사용하는 게 좋다.

```python
def print_info(*pa, **ka):
    print(pa)
    print(ka)

print_info("insutance", 99, gender="Male")
>>> ('insutance', 99)
>>> {'gender': 'Male'}
```

## 마무리

최근 회사 프로젝트에서 코드를 작성할 때 Unpacking 기능을 유용하게 사용했기 때문에 정리 글을 작성했고, args, kwargs 는 예전부터 정리하고 싶은 부분이었다. 이렇게 한꺼번에 정리할 수 있는 주제 `*` 에게 고맙다. 대부분 알고 있는 내용일 수 있지만, 어떻게 값이 들어오고, 어떻게 값을 넣어줘야 하는지 다시 한번 생각할 수 있게 해주는 글이 되면 좋겠다.

## 참고

- [파이썬 Asterisk(*)에 대해서](https://dailyheumsi.tistory.com/41)
- [PYTHON에서의 ASTERISK는 무슨일을 하는가.](https://jangjy.tistory.com/358)
- [파이썬의 Asterisk(*) 이해하기](https://mingrammer.com/understanding-the-asterisk-of-python/)