# Python's GIL(Global Interpreter Lock)

> Python에서 GIL(Global Interpreter Lock)은 한 번에 하나의 스레드만 Python 코드를 실행하도록 하는 일종의 뮤텍스(Mutex)입니다. 이것은 Python 인터프리터(CPython) 내부의 자원을 보호하고, 여러 스레드가 동시에 Python 객체에 접근하는 것을 방지합니다. GIL을 통해 Python 객체에 대한 접근을 보호하여 데이터 무결성을 유지하고 스레드 간에 충돌을 방지합니다.



* Mutex란 여러 thread가 공유자원에 접근할 때 그 공유자원에 접근하기 위한 일종의 열쇠 같은 것
* 인터프리터 : 고수준 프로그래밍 언어를 한줄한줄 기계어로 번역한 뒤에 바로 실행 시켜주는 프로그램
* Thread : 프로세스 내에서 작은 실행흐름 단위



![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FG0yFa%2Fbtq8KR1x1uD%2FVEj2oyOxwS1146fCrtqB7k%2Fimg.png)

***

### Why does python need GIL?

파이썬은 모든 객체의 수명을 관리하기 위해 참조 계수(Reference Counting) 방식을 사용합니다. 참조 계수 방식은 파이썬의 모든 객체가 참조될 때마다 참조 횟수를 증가시키고, 참조 횟수가 0이 되면 해당 객체를 삭제하는 방식입니다. 이 때 여러 스레드가 동시에 하나의 Python 객체에 접근하면 동시성 문제가 발생할 수 있기 때문에 GIL(Global Interpreter Lock)을 도입하게 되었습니다.



Python의 모든 객체에 뮤텍스(Mutex)를 거는 것은 비효율적이므로, 파이썬 인터프리터 자체에 락을 걸어 효율적으로 동시성을 관리하는 것입니다. 다시 말해, 하나의 스레드만이 파이썬 인터프리터에 접근하고 상호작용하도록 하는 것이 GIL입니다.



***

### Single Threading VS Multi Threading

파이썬에서는 일반적으로 GIL을 사용하고 있어 멀티 쓰레딩의 이점을 가져갈 수 없으며, 오히려 멀티 쓰레딩은 컨텍스트 스위칭(쓰레딩 간 전환) 시에 비용이 발생하므로 성능이 저하될 수 있습니다.

아래는 싱글 스레딩과 멀티 스레딩을 사용한 CPU 바운드 작업의 예제 코드입니다.

#### Example

```python
import time
import threading

def cpu_bound_operation():
    count = 0
    for i in range(100000000):
        count += i

# 싱글스레딩
start_time = time.time()
cpu_bound_operation()
cpu_bound_operation()
end_time = time.time()
print(f"싱글스레딩 시간: {end_time - start_time}")

# 멀티스레딩
start_time = time.time()
thread1 = threading.Thread(target=cpu_bound_operation)
thread2 = threading.Thread(target=cpu_bound_operation)
thread1.start()
thread2.start()
thread1.join()
thread2.join()
end_time = time.time()
print(f"멀티스레딩 시간: {end_time - start_time}")

```



***

### 파이썬에서 멀티 쓰레딩을 사용하면 안되나? No!

파이썬에서 멀티 쓰레딩을 사용하여 성능을 향상시킬 수 있는 경우는 I/O 바운드 작업을 수행할 때입니다. I/O 바운드 작업(파일 읽기/쓰기, 네트워크 통신, 데이터베이스 쿼리 등)은 주로 대기 시간이 발생하고 CPU가 대부분 대기 상태에 있기 때문에, 멀티 스레딩을 사용하여 여러 작업을 동시에 처리할 수 있습니다.

예를 들어, 다음은 멀티 스레딩을 사용하여 여러 URL에서 웹 페이지를 다운로드하는 예제 코드입니다.

#### Example

```python
import threading
import requests
import time

urls = ["http://example.com", "http://example.org", "http://example.net"]

def download(url):
    response = requests.get(url)
    print(f"{url}: {len(response.content)} bytes")

# 멀티스레딩
start_time = time.time()
threads = [threading.Thread(target=download, args=(url,)) for url in urls]

for thread in threads:
    thread.start()
for thread in threads:
    thread.join()

end_time = time.time()
print(f"멀티스레딩 시간: {end_time - start_time}")


# 싱글 스레딩
start_time = time.time()
for url in urls:
    download(url)
end_time = time.time()

print(f"싱글 스레딩 시간: {end_time - start_time}")

```



***

### I/O 바운드 작업이 아닌 일반 작업에서 멀티 쓰레딩으로 향상시킬 수 있는 대안

* GIL 을 이용하는 CPython 으로 구현된 파이썬 인터프리터가 아니라 다른 파이썬 구현체(Jython, IronPython 등..)을 이용해서 멀티 쓰레딩으로 성능을 향상 시킬 수 있다.



