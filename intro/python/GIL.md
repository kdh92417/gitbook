# Python's GIL

> Python Object에 대한 접근을 보호하는 일종의 Mutext로서 여러개의 Thread가 파이썬 코드를 동시에 실행할 수 없게 하는 것
>
> 즉, 하나의 프로세스 내에서 Python 인터프리터(CPython)은 하나의 시점에서 하나의 Thread만 실행될 수 있다.
>
> Multi Threading이 불가능 하다는 것이 아니라 병렬로 실행이 불가능 하다는 뜻. 여러 코어에서 여러 쓰레드가 동시에 실행될 수 있는데(병렬) Python에서는 병렬로 실행이 불가능하다는 뜻

\


![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FG0yFa%2Fbtq8KR1x1uD%2FVEj2oyOxwS1146fCrtqB7k%2Fimg.png)

\


## Python의 실행원리

* python의 코드를 CPython이 해석
* Python(bytecode)로 바뀜
* 실행 시 여러 thread 사용할 경우 하나의 thread만 실행하도록 lock이 걸려지도록 되어있음
* 단일 thread만이 Python Object에 접근을 제한하는 mutex(자물쇠가 있는 thread만이 공유자원에 접근할 수 있는 thread 동기화 메커니즘)

### Mutex란?

Mutex란 여러 thread가 공유자원에 접근할 때 그 공유자원에 접근하기 위한 일종의 열쇠 같은 것

\


## Why does python need GIL?

* **CPython 메모리 관리가 취약** : thread safe를 하기위해 GIL 사용
  * Python은 reference counting 방식의 GC를 수행하는데 여러 쓰레드가 동시에 실행되면 [rece condition](https://iredays.tistory.com/125)이 발생되어 GC가 제대로 수행되지 않음
* **Single Thread로도 충분히 빨르다**
* **멀티 프로세스 사용 가능** : Numpy, Scipy등 GIL 외부 영역에서 효율적으로 코딩
* **병렬 처리의 선택지가 다양** : Multiprocessing, asyncio등 선택지가 다양
* **thread 동시성 완벽 처리를 위해 다른 방법이 존재** : Jython, IronPython, Stackless Python 등이 존재
