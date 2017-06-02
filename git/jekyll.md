# Jekyll 설치 on mac

올해 목표 중 하나인 github에서 블로그를 운영하기 위해 Jekyll(지킬)을 설치한다. 구글 검색을 해보면 좋은 설치 자료도 많지만 읽을만한 구축 후기들이 많았다. 나도 깃헙 블로그를 구축하면서 앞으로 어떻게 운영할지 생각도 해보려고 한다. 2016년에는 왜 미루기만 했는지 반성도 필요하다.

## 설치 문서

[Jekyll 공식 설치 문서](http://jekyllrb-ko.github.io/docs/installation/)

## 참고 자료

* [GitHub Pages](https://pages.github.com)
* [Setting up your GitHub Pages site locally with Jekyll](https://help.github.com/articles/setting-up-your-github-pages-site-locally-with-jekyll)
* [운영체제별 지킬 설치와 사용](http://vjinn.github.io/install-jekyll)
* [지킬로 깃허브에 무료 블로그 만들기](https://nolboo.kim/blog/2013/10/15/free-blog-with-github-jekyll)
* [kakao 기술 블로그가 GitHub Pages로 간 까닭은](http://tech.kakao.com/2016/07/07/tech-blog-story)
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

계속 오류가 발생하는 경우 커맨드라인 툴을 설치한다.

```
$ xcode-select --install
xcode-select: note: install requested for command line developer tools

```

> https://stackoverflow.com/a/35875745/4622153

이미 설치가 되어 있다면

```
sudo xcodebuild -license
```

```
$ sudo gem install jekyll
Building native extensions.  This could take a while...
Successfully installed ffi-1.9.18
Fetching: rb-inotify-0.9.8.gem (100%)
Successfully installed rb-inotify-0.9.8
Fetching: listen-3.0.8.gem (100%)
ERROR:  While executing gem ... (Errno::EPERM)
    Operation not permitted - /usr/bin/listen
```

다시 에러가 발생했다.

```
$ sudo su
sh-3.2# sudo gem install -n /usr/local/bin compass
Fetching: multi_json-1.12.1.gem (100%)
Successfully installed multi_json-1.12.1
Fetching: compass-core-1.0.3.gem (100%)
Successfully installed compass-core-1.0.3
Fetching: compass-import-once-1.0.5.gem (100%)
Successfully installed compass-import-once-1.0.5
Fetching: chunky_png-1.3.8.gem (100%)
Successfully installed chunky_png-1.3.8
Fetching: compass-1.0.3.gem (100%)
    Compass is charityware. If you love it, please donate on our behalf at http://umdf.org/compass Thanks!
Successfully installed compass-1.0.3
Parsing documentation for multi_json-1.12.1
Installing ri documentation for multi_json-1.12.1
Parsing documentation for compass-core-1.0.3
Installing ri documentation for compass-core-1.0.3
Parsing documentation for compass-import-once-1.0.5
Installing ri documentation for compass-import-once-1.0.5
Parsing documentation for chunky_png-1.3.8
Installing ri documentation for chunky_png-1.3.8
Parsing documentation for compass-1.0.3
Installing ri documentation for compass-1.0.3
5 gems installed
sh-3.2# exit
```

터미널을 다시 열고 jekyll 설치를 시도한다.

```
$ sudo gem install jekyll
ERROR:  While executing gem ... (Errno::EPERM)
    Operation not permitted - /usr/bin/listen
```

에러 메시지를 보니 `listen`을 새로 설치해야 할 것 같다. 엄한 `compass` 를 설치했다.

```
$ sudo su
sh-3.2# sudo gem install -n /usr/local/bin listen
Fetching: ruby_dep-1.5.0.gem (100%)
ERROR:  Error installing listen:
	ruby_dep requires Ruby version >= 2.2.5, ~> 2.2.
```

`listen`을 설치하려고 보니 ruby 버전이 낮아서 실패.

```
# ruby --version
ruby 2.0.0p648 (2015-12-16 revision 53162) [universal.x86_64-darwin15]
```

ruby 업데이트를 진행한다.

> https://stackoverflow.com/a/38194139/4622153

[RVM](http://rvm.io) 설치

```
\curl -sSL https://get.rvm.io | bash -s stable
```

ruby 2.4.0 설치

```
$ rvm install ruby-2.4.0
```

진행하다가 RVM 보다 rbenv 가 좋다고 하여 메모로 남겨놓는다. MacOS 를 새로 설치할 예정이어서 이번에는 RVM을 사용한다.

> http://theeye.pe.kr/archives/1798
RVM이 사용하기 복잡하고 시스템 환경을 너무 많이 변경시킨다는 말씀들을 하시더군요. rbenv(Ruby Environment)의 경우 매우 간단한 구조로 되어있다고 하여 저도 갈아타기로 하였습니다.

```
$ ruby --version
ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-darwin15]
```

ruby 2.4.0 설치 완료. jekyll 설치를 다시 시도한다.

```
$ sudo gem install jekyll
```

성공. 결국 ruby 버전이 낮아서 계속 오류가 발생했다.

이제 github 페이지로 사용할 jekyll 사이트를 만들자.

```
$ jekyll new misocharles.github.com
  Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at https://jekyllrb.com/help/!
jekyll 3.4.3 | Error:  bundler
```

실패.

Bundler를 설치한다.

```
$ gem install bundler
```

```
$ jekyll new misocharles.github.com
# New jekyll site installed in .../misocharles.github.com.
```

jekyll 설치가 완료되었다. jekyll애서 제공하는

```
$ jekyll serve --watch
# Server address: http://127.0.0.1:4000/
# Server running... press ctrl-c to stop.
```

http://127.0.0.1:4000/ 로 접근하여 생성된 사이트를 확인한다.
