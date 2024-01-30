# Python's GIL(Global Interpreter Lock)

> Python Object에 대한 접근을 보호하는 일종의 Mutext로서 여러개의 Thread가 파이썬 코드를 동시에 실행할 수 없게 하는 것
>
> 즉, 하나의 프로세스 내에서 Python 인터프리터(CPython)은 하나의 시점에서 하나의 Thread만 실행될 수 있다.
>
> Multi Threading이 불가능 하다는 것이 아니라 병렬로 실행이 불가능 하다는 뜻. 여러 코어에서 여러 쓰레드가 동시에 실행될 수 있는데(병렬) Python에서는 병렬로 실행이 불가능하다는 뜻

* Mutex란 여러 thread가 공유자원에 접근할 때 그 공유자원에 접근하기 위한 일종의 열쇠 같은 것
* 인터프리터 : 고수준 프로그래밍 언어를 한줄한줄 기계어로 번역한 뒤에 바로 실행 시켜주는 프로그램
* Thread : 프로세스 내에서 작은 실행흐름 단위



![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2\&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FG0yFa%2Fbtq8KR1x1uD%2FVEj2oyOxwS1146fCrtqB7k%2Fimg.png)



### Why does python need GIL?

파이썬은 reference counting 방식으로 모든 객체의 수명을 관리한다. reference counting 방식이란 Python 의 모든 객체들이 참조되어질 때마다 카운팅을 하고 카운팅이 0이 될때 해당 객체를 삭제 하는 것입니다. 이 때 여러 쓰레드가 동시에 하나의 파이썬 오브젝트에게 접근을 하게되면 동시성 문제가 발생될 수 있기에 **GIL** 을 거는 것이 필요하게되었습니다.



이 때, Python 오브젝트 모두에게 뮤텍스를 거는 것은 굉장히 비효율적이기에 파이썬 인터프리터 자체에 락을 걸어 효율적으로 동시성을 관리하는 것이다. 즉 하나의 쓰레드만이 파이썬 인터프리터에 접근하고 상호작용하도록 하는 것이 GIL 이다.





파이썬에서 일반적으로는 위의 GIL 을 사용하고 있어 멀티 쓰레딩의 이점을 가져가지 못하고, 오히려 멀티 쓰레딩은 컨텍스트 스위칭(쓰레딩간에 전환)시에 비용이 발생되어, 성능이 저하 된다.



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



### 파이썬에서 멀티 쓰레딩을 사용하면 안되나? No!

파이썬은 I/O 바운드 작업(파일 읽기/쓰기/다운로드, 네트워크 통신 등..)을 할때는 I/O 바운드 작업 대기 중(다운로드 또는 네트워크 통신을 위한 작업 대기)에 다른 I/O 바운드 작업을 진행을 하여 멀티 쓰레딩을 이용해서 성능 향상을 기대할 수 있다.



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



### I/O 바운드 작업이 아닌 일반 작업에서 멀티 쓰레딩으로 향상시킬 수 있는 대안

* GIL 을 이용하는 CPython 으로 구현된 파이썬 인터프리터가 아니라 다른 파이썬 구현체(Jython, IronPython 등..)을 이용해서 멀티 쓰레딩으로 성능을 향상 시킬 수 있다.



