# Jekyll

올해 목표 중 하나인 github에서 블로그를 운영하기 위해 Jekyll(지킬)을 설치한다. 구글 검색을 해보면 좋은 설치 자료도 많지만 읽을만한 구축 후기들이 많았다. 나도 깃헙 블로그를 구축하면서 앞으로 어떻게 운영할지 생각도 해보려고 한다. 2016년에는 왜 미루기만 했는지 반성도 필요하다.

## 설치 문서

[Jekyll 공식 설치 문서](http://jekyllrb-ko.github.io/docs/installation/)

## 참고 자료

* [운영체제별 지킬 설치와 사용](http://vjinn.github.io/install-jekyll/)
* [지킬로 깃허브에 무료 블로그 만들기](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll/)
* [kakao 기술 블로그가 GitHub Pages로 간 까닭은](http://tech.kakao.com/2016/07/07/tech-blog-story/)
* [우아한형제들의 Baby Steps](http://woowabros.github.io/woowabros/2016/06/30/woowabros_cto.html)
* [Jekyll을 이용하여 github에 블로그 만들기](https://brunch.co.kr/@hee072794/39)

## 설치

```
$ gem install jekyll
```

모든 gem 의존요소들을 신경쓸 것 없이 설치하는 가장 좋은 방법

```
$ sudo gem install jekyll
Password:
Fetching: public_suffix-2.0.5.gem (100%)
Successfully installed public_suffix-2.0.5
Fetching: addressable-2.5.1.gem (100%)
Successfully installed addressable-2.5.1
Fetching: colorator-1.1.0.gem (100%)
Successfully installed colorator-1.1.0
Fetching: sass-3.4.24.gem (100%)
Successfully installed sass-3.4.24
Fetching: jekyll-sass-converter-1.5.0.gem (100%)
Successfully installed jekyll-sass-converter-1.5.0
Fetching: rb-fsevent-0.9.8.gem (100%)
Successfully installed rb-fsevent-0.9.8
Fetching: ffi-1.9.18.gem (100%)
Building native extensions.  This could take a while...
ERROR:  Error installing jekyll:
	ERROR: Failed to build gem native extension.

    /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin/ruby extconf.rb
checking for ffi.h... *** extconf.rb failed ***
Could not create Makefile due to some reason, probably lack of necessary
libraries and/or headers.  Check the mkmf.log file for more details.  You may
need configuration options.
```

루비 설치 오류가 발생했다. 공식 홈페이지에서 [해결방법](http://jekyllrb-ko.github.io/docs/troubleshooting/)을 제공한다.

RubyGems 을 업데이트 해준다.

```
$ sudo gem update --system
```

> 맥 OS X 을 업그레이드 한다고 해서 Xcode 까지 자동으로 업그레이드 되지는 않는다는 것과 (Xcode 업그레이드는 App Store 에서 별도로 수행합니다).
최신 버전이 아닌 Xcode.app 은 앞서 설명한 명령행 도구와 충돌을 일으킬 수 있다는 점에 주의하기 바랍니다. 이런 문제가 발생한다면, Xcode 를 업그레이드 하고 최신 명령행 도구를 설치하세요.
