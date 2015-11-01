# 2장 uniitest 모듈을 이용한 기능 테스트 확장

## 기능 테스트를 이용한 최소 기능의 애플리케이션 설계

### 기능 테스트(Function test, FT)
- 셀레늄을 이용한 테스트 '실제 웹 브라우저에서 애플리케이션이 어떻게 동작하는지 사용자 관점에서 확인할 수 있다.'
- FT 자체가 애플리케이션 사양이 될 수 있다.
- 사용자 스토리(User story) '특정 기능을 사용자가 어떻게 사용하며 반응을 받는지를 확인하는 방식', 기능테스트 구조화에 사용
- FT는 사람이 이해할 수 있는 스토리를 가지고 있어야 한다.
- 사용자 스토리의 핵심을 정리하기 위해 주석을 작성할 수도 있다.

```python
#function_tests.py
from selenium import webdriver

browser = webdriver.Firefox()

# 에디스는 멋진 작업 목록 온라인 앱이 나왔다는 소식을 듣고
# 해당 웹 사이트를 확인하러 간다
browser.get('http://localhost:8000')

# 웹페이지 타이틀과 헤더가 'To-Do'를 표시하고 있다
assert 'To-Do' in browser.title

# 그녀는 바로 작업을 추가하기로 한다

# "공작깃털 사기"라고 텍스트 상자에 입력한다
# (에디스의 취미는 날치 잡이용 그물을 만드는 것이다)

# 엔터키를 치면 페이지가 갱신되고 작업 목록에
# "1: 공작깃털 사기" 아이템이 추가된다

# 추가 아이템을 입력할 수 있는 여분의 텍스트 상자가 존재한다
# 다시 "공작깃털을 이용해서 그물 만들기"라고 입력한다

# 페이지가 다시 갱신되고, 두 개 아이템이 목록에 보인다
# 에디스는 사이트가 입력한 목록을 저장하고 있는지 궁금하다
# 사이트는 그녀를 위한 특정 URL을 생성해준다
# 이때 URL에 대한 설명도 함께 제공된다

# 해당 URL에 접속하면 그녀가 만든 작업 목록이 그대로 있는 것을 확인할 수 있다

# 만족하고 잠자리에 든다

browser.quit()
```

예상한대로 테스트는 실패다.
- 예측된 실패(Expected failure) : 의도적으로 구현한 테스트 실패

```bash
$ python3 functional_test.py 
Traceback (most recent call last):
  File "functional_test.py", line 10, in <module>
    assert 'To-Do' in browser.title
AssertionError
```

## 파이썬 기본 라이브러리의 unittest 모듈

AssertionError 유용하게 사용하기

`assert 'To-Do' in browser.title, "Browser title was " + browser.title`

실행결과는 

`AssertionError: Browser title was Welcome to Django`

### unittest 모듈

- uniitest [온라인문서](http://docs.python.org/3/library/unittest.html)

```python
# functional_unittest.py
from selenium import webdriver
import unittest

class NewVisitorTest(unittest.TestCase):

        def setUp(self):
                self.browser = webdriver.Firefox()

        def tearDown(self):
                self.browser.quit()

        def test_can_start_a_list_and_retrieve_it_later(self):
                # 에디스는 멋진 작업 목록 온라인 앱이 나왔다는 소식을 듣고
                # 해당 웹 사이트를 확인하러 간다
                self.browser.get('http://localhost:8000')

                # 웹페이지 타이틀과 헤더가 'To-Do'를 표시하고 있다
                self.assertIn('To-Do', self.browser.title)
                self.fail('Finish the test!')

                # 그녀는 바로 작업을 추가하기로 한다

                # "공작깃털 사기"라고 텍스트 상자에 입력한다
                # (에디스의 취미는 날치 잡이용 그물을 만드는 것이다)

                # 엔터키를 치면 페이지가 갱신되고 작업 목록에
                # "1: 공작깃털 사기" 아이템이 추가된다

                # 추가 아이템을 입력할 수 있는 여분의 텍스트 상자가 존재한다
                # 다시 "공작깃털을 이용해서 그물 만들기"라고 입력한다

                # 페이지가 다시 갱신되고, 두 개 아이템이 목록에 보인다
                # 에디스는 사이트가 입력한 목록을 저장하고 있는지 궁금하다
                # 사이트는 그녀를 위한 특정 URL을 생성해준다
                # 이때 URL에 대한 설명도 함께 제공된다

                # 해당 URL에 접속하면 그녀가 만든 작업 목록이 그대로 있는 것을 >확인할 수 있다

                # 만족하고 잠자리에 든다

if __name__ == '__main__':
        unittest.main(warnings='ignore')
```

unittest를 적용한 결과 setUp, tearDown 메소드로 테스트 이후 firefox 창이 시작하고 닫힌다

```bash
$ python3 functional_unittest.py 
F
======================================================================
FAIL: test_can_start_a_list_and_retrieve_it_later (__main__.NewVisitorTest)
----------------------------------------------------------------------
Traceback (most recent call last):
  File "functional_unittest.py", line 18, in test_can_start_a_list_and_retrieve_it_later
    self.assertIn('To-Do', self.browser.title)
AssertionError: 'To-Do' not found in 'Welcome to Django'

----------------------------------------------------------------------
Ran 1 test in 3.682s

FAILED (failures=1)
```

## 암묵적 대기

implicityly_wait (암묵적 대기), 지정한 시간만큼 대기한다. 너무 신뢰하면 안된다.

```python
        def setUp(self):
                self.browser = webdriver.Firefox()
                self.browser.implicitly_wait(3)

        def tearDown(self):
```

## 커밋

```bash
$ git diff

$ git commit -a
```
