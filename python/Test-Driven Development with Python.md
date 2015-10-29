# Test-Driven Development with Python.md

## 설치 

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

 
