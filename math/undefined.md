# 부동소수점 연산의 한계

Python 또는 여러 컴퓨터언어에서 아래와 같이 연산이 정확하지 않을 때가 있다.

```python
>>> 0.1 + 0.2
>>> 0.30000000000000004
```



그렇다면 컴퓨터언어에서의 실수 연산이 왜 위와 같이 정확하지 않을까?&#x20;

그 이유는 컴퓨터는 10진수를 2진수로 변환하여 표현 및 처리하는데, 해당 과정에서 부동소수점 연산의 한계가 있어 정확하지 않기 때문이다.

부동소수점 연산에 한계가 있기 때문이다. 일단 부동소수점이 무엇인지 알고 파헤처보자.



### 부동소수점이란?

<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption><p>부동소수점 구성</p></figcaption></figure>

* 컴퓨터에서 실수를 표현하는 방법 중 하나로서, **지수(소수점의 위치와 크기)**가 변하면서 **가수(유효한 값)**부분의 값이 변경되는 표현 방식이다.



### 부동소수점 연산의 한계

그렇다면, 다시 위의 `0.1` 과 `0.2` 를 부동소수점으로 표현하면 밑에와 같다.



#### 정확한 표현 불가능

```python
# Decimal : 십진 부동소수점 연산 모듈
>>> import decimal
>>> decimal.Decimal(0.1)
Decimal('0.1000000000000000055511151231257827021181583404541015625')
>>> decimal.Decimal(0.2)
Decimal('0.200000000000000011102230246251565404236316680908203125')
```

* 위와 같이 10진수를 부동소수점 방식으로 표현하면 정확하게 나타낼 수 없기 때문에 근사치로 표현되어 정확한 연산이 되지 않는다.



#### 반올림 오차

```python
>>> a = decimal.Decimal(0.1)
>>> b = decimal.Decimal(0.2)
>>> a + b
Decimal('0.3000000000000000166533453694')
>>> 0.1 + 0.2
0.30000000000000004
```

* 위와 같이 부동소수점의 일부 연산에서 반올림 오차가 발생하여 정확하지 않은 연산이 발생



부동소수점 연산의 한계에 있어서 밑에 글에서 더 자세하게 다루고 있으니 확인해보면 좋을 듯 하다.

* [https://devocean.sk.com/blog/techBoardDetail.do?page=\&boardType=undefined\&query=\&ID=165270\&searchData=\&subIndex=](https://devocean.sk.com/blog/techBoardDetail.do?page=\&boardType=undefined\&query=\&ID=165270\&searchData=\&subIndex=)
* [https://devocean.sk.com/blog/techBoardDetail.do?page=\&boardType=undefined\&query=\&ID=165276\&searchData=\&subIndex=#none](https://devocean.sk.com/blog/techBoardDetail.do?page=\&boardType=undefined\&query=\&ID=165276\&searchData=\&subIndex=#none)



