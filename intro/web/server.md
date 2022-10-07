# Web Server와 WSGI, Web Application

## Web Server
> 클라이언트의 요청을 받아 어플리케이션에게 전달하여 응답을 받고 다시 클라이언트에게 전달하는 역할
>
> 정적파일(html, css, image, file)등은 웹서버가 자체에서 바로 응답

### 웹 서버의 역할

- 캐싱
- 로드밸런싱
- SSL
- 동적 요청을 WAS에게 전달
- 정적 파일 전달

## WAS(Web Application Server)

> 클라이언트로 동적인 리소스를 전달해주는 역할을 수행,
> 또는 웹 서버(Apache or Nginx 등)와 웹 어플리케이션(Django, FastAPI)를 연결해주는 역할

- 이떄 웹 서버는 Python언어를 통해 통신을 할 수가 없기 때문에, WSGI를 이용하여 웹서버와 웹어플리케이션이 통신가능하게한다.


## WSGI(Web Server Gateway Interface)

> 웹서버와 파이썬 웹어플리케이션간의 인터페이스 역할을 수행

- WSGI 서버(미들웨어)로 `gunicorn`, `uWSGI`, `mod_wsgi` 등이 있다.

## ASGI(Asynchronous Server Gateway Interface)

> WSGI를 비동기방식으로 동작할 때 발생하는 문제점을 해결한, 비동기 방식에 초점을 둔 웹서버와 Python 어플리케이션을 연결해주는 인터페이스


## Reference

- [wsgi와 asgi](https://nitro04.blogspot.com/2020/01/django-python-asgi-wsgi-analysis-of.html)
