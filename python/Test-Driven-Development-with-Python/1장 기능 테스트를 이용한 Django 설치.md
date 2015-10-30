## 기본 설치 

### [Python 3.4.3 - 2015-02-25](https://www.python.org/downloads/mac-osx/)
-- Download [Mac OS X 64-bit/32-bit installer](https://www.python.org/ftp/python/3.4.3/python-3.4.3-macosx10.6.pkg)

### [Django](https://www.djangoproject.com)
웹 프레임워크
```bash
$ sudo pip3 install django==1.8
```
책에선 1.7 이었지만 지원이 2015년 12월까지이기 때문에 1.8로 재설치하였다. 로그를 보면 깔끔하게 1.7을 삭제해준다. 
```bash
Collecting django==1.8
  Downloading Django-1.8-py2.py3-none-any.whl (6.2MB)
    100% |################################| 6.2MB 62kB/s 
Installing collected packages: django
  Found existing installation: Django 1.7
    Uninstalling Django-1.7:
      Successfully uninstalled Django-1.7

Successfully installed django-1.8
```

### Selenium 셀레늄 
기능 테스트를 위해 필요한 브라우저 자동화 툴 (파이어폭스)
```bash
$ sudo pip3 install --upgrade selenium
```

# 1장 기능 테스트를 이용한 Django 설치

## 테스팅 고트님께 복종하라! 테스트가 없으면 아무것도 하지 마라!

- 테스트를 잘하기 위한 고약한 스승이 필요하다 "Testing Goat"
- TDD에서 가장 먼저 해야 할 것 "테스트를 작성하라"

첫 번째 단계는 Django의 정상 설치 여부

```python
$ vi functional_test.py 
from selenium import webdriver

browser = webdriver.Firefox()
browser.get('http://localhost:8080')

assert 'Django' in browser.title
```

- 파이어폭스 브라우저 창을 실행하기 위해 셀레늄의 webdriver 가동
- 브라우저를 통해 로컬 PC상의 웹페이지를 연다
- 웹 페이지 타이틀에 'Django'라는 단어가 있는지 확인

```bash
$ python3 functional_test.py 
Traceback (most recent call last):
  File "functional_test.py", line 6, in <module>
    assert 'Django' in browser.title
AssertionError
```

## Django 가동 및 실행

웹 사이트의 메인 컨테이너가 될 프로젝트를 만들기 위해 Django 가동하고 실행. supserlists 폴더가 생김.

```bash
$ django-admin.py startproject superlists
```

superlists/superlists 폴더가 사이트 전역에 걸쳐 적용된다.

```bash
$ cd supserlists/
$ ls
manage.py	superlists
$ python3 manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).

You have unapplied migrations; your app may not work properly until they are applied.
Run 'python manage.py migrate' to apply them.

October 30, 2015 - 15:06:00
Django version 1.8, using settings 'superlists.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.
```

웹서버를 띄우고 새로운 터미널 창을 열어서 다시 테스트 코드를 실행한다.

```bash
$ python3 functional_test.py 
Traceback (most recent call last):
  File "functional_test.py", line 6, in <module>
    assert 'Django' in browser.title
AssertionError
```

functional_test.py 에서 포트를 8000 으로 해야 하는데, tomcat 서버인 8080 으로 해서 오류가 났다. 수정 후 다시 실행한다. 

```bash
$ python3 functional_test.py 
$
```

AssertionError가 발생하지 않음. 셀레늄에 의해 파이어폭스 창이 뜨고 웹페이지가 뜸.

서버 실행 중간에 난 오류메시지를 처리하기 위해서 migrate 명령을 실행한다.

```bash
$ python3 manage.py migrate

(메시지 중략)

$ python3 manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).
October 30, 2015 - 15:14:15
Django version 1.8, using settings 'superlists.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CONTROL-C.

```

## Git 리포지토리 실행

functional_test.py 파일을 옮기고 git 초기화

```bash
$ ls
functional_test.py	superlists
$ mv functional_test.py superlists/
$ cd superlists/
$ git init .
```

불필요한 파일 설정 (.gitignore)

```bash
$ echo "db.sqlite3" >> .gitignore
$ echo "__pycache__" >> .gitignore
$ echo "*.pyc" >> .gitignore
```

```bash
$ git add .
$ git commit -m "First Commit: First FT and basic Django config"
```