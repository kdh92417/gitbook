# RESTfull API

![REST API](../basic\_knowledge/rest\_api/img\_1.png)

## REST API란 무엇인가?

### API

* 어떤 응용프로그램에서 데이터를 주고받기위한 방법을 의미한다.
* 어느 특정 사이트에서 정보를 공유할경우 어떤식으로 정보를 요청해야하는지 그리고 어떠한 정보들을 제공받을 수 있는지에 대한 규격

### REST(Representational State Transfer)

* 웹(HTTP Protocol)의 장점을 최대한 활용할 수 있는 아키텍처
* URI는 자원을 HTTP method로는 각 요청의 의도를 파악할 수 있게 만드는 것을 REST라 한다.

### RESTFul API

* Rest 기반의 규칙들을 지켜서 설계된 API
* REST API는 REST 아킥텍처가 있는 API라는 뜻이고, RESTFul API는 완벽히 REST 규칙들을 지킨 API라한다.

\


## REST API의 등장과 필요

### REST API의 등장

> 멀티 플랫폼, 멀티 디바이스 시대로 넘어옴으로써 기존에 브라우저만 지원하면 되었던 것과는 달리,\
> 최근 서버는 브라우저를 포함하여 안드로이드, 아이폰과 통신에 대응 할 수 있어야한다.
>
> 따라서 플랫폼에 맞추어 서버를 만드는 것이 아니라 범용적으로 사용성을 보장하는 API 디자인이 필요해졌다.

### REST API의 필요

* 디바이스(TV, 스마트폰, 태블릿 등등)의 다양화로 인해 특정 플랫폼에 제약두지 않기 위해
* 위와 비슷한 맥락에서 Server는 Client Side를 고려하지 않고 JSON 또는 XML 같은 형태로 응답하고 Client는 이를 바로 객체로 변환하여 데이터를 바로 사용할 수 있게 되었다.
  * Server와 Client의 역할 분리

\


## REST API의 구성과 특징

### REST API의 구성

> REST API는 밑의 3가지 구성으로 이루어진다.

* 자원(Resource) : URI
* 행위(Verb) : HTTP Method
* 표현(Representations)

### REST API의 특징

#### 1. Uniform(Uniform Interface)

* URI로 지정한 리소스에대한 조작을 통일, 한정적인 인터페이스로 수행하는 아키텍처
* 특정언어나 기술에 얽매이지 않는다.

#### 2. Stateless - 무상태성

* `REST API` 는 `HTTP Protocol`을 이용하기 떄문에 클라이언트의 상태를 서버에서 저장하지 않는다.
* 따라서 단순히 서버는 클라이언트에서 오는 요청만 처리
* 자유도가 높아지고, 서버에서 불필요한 정보를 따로 저장하지 않기 떄문에 구현이 단순해짐

#### 3. Cacheable - 캐시가능

* `HTTP Protocol` 의 기존 웹표준을 사용하기 때문에 `HTTP` 가 가진 캐시기능을 적용가능하다.
* `Last-Modified`나 `E-tag`를 이용하여 구현 가능

#### 4. Self-Descriptiveness - 자체 표현 구조

* `REST API` 메세지만 보고도 쉽게 이해 가능한 자체 표현 구조로 되어있다.

#### 5. Server - Client 구조

* 서버는 REST API 제공, 클라이언트는 유저의 인증 및 컨텍스트(세션, 로그인 정보)등을 관리
  * Server와 Client의 역할이 확실히 분리
  * 서버에서 개발해야될 것과 클라이언트에서 개발해야될 것이 명확해짐 -> 서로간 의존성이 낮아짐

#### 6. 계층형 구조

* `REST` 서버는 다중 계층으로 구성될 수 있다.
* 로드 밸런싱, 암호화 계층 등을 추가해 구조상의 유연상을 둘 수 있음
* `PROXY` , `Gateway` 같은 네트워크 기반의 중간매체를 사용할 수 있게한다.

\


## REST API 디자인 가이드

### 1. URI는 정보의 자원을 표현해야 된다.

리소스명은 동사보다 명사를 사용

*   bad case

    ```shell
    DELETE /users/delete/1
    ```
*   good case

    ```shell
    DELETE /users/1
    ```

### 2. 슬래시 구분자(/)는 계층관계를 나타내는 데 사용

또한 마지막 문자로 슬래시(/)를 포함하지 않는다.

```shell
GET /mart/products/coffee/1
```

### 3. 하이픈(-)은 URI 가독성을 높이는 데 사용

```shell
GET /mart/products/decaffeinated-coffee/1
```

### 4. 밑줄(\_)은 URI 에 사용하지 않는다.

가독성에 좋지않고 문자가 가려지기도 하여 밑줄 대신 하이픈을 사용한다.

### 5. URI 경로에는 소문자가 적합

대소문자에 따라 다른 리소스로 인식하기 때문

* RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고 대소문자를 구별하도록 규정

### 6. 파일 확장자는 URI에 포함시키지 않는다.

*   bad case

    ```shell
    GET /users/1/profile.jpg
    ```
*   good case

    ```shell
     GET /users/1/profile
    ```

## Reference

* [Restfull API](https://github.com/JaeYeopHan/Interview\_Question\_for\_Beginner/tree/master/Development\_common\_sense#restful-api)
* [RESTful-API-이란](https://velog.io/@somday/RESTful-API-%EC%9D%B4%EB%9E%80)
* [REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
