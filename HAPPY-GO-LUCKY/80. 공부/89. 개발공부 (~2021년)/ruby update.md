---
tags:
  - ruby
Created: Invalid date
Updated: Invalid date
---
[https://pie001.github.io/entry/blog/0017/](https://pie001.github.io/entry/blog/0017/)

# **１. brew update**

## # brew update

$ brew update

permission계열의 에러가 발생할 경우엔 해당 패스로 이동

## 예

$ cd /Library/Developer/CommandLineTools

아래와 같이 표시되면 OK

Already up-to-date.

# **２. brew install**

## # brew install

$ brew install rbenv ruby-build

아래와 같은 에러가 발생한 경우엔 X-code를 인스톨

**==>** Installing dependencies **for** rbenv: autoconf, pkg-config, openssl, ruby-build

**==>** Installing rbenv dependency: autoconf

xcrun: error: invalid active developer path **(**/Library/Developer/CommandLineTools**)**, missing xcrun at: /Library/Developer/CommandLineTools/usr/bin/xcrun

Error: Failure **while** executing: git config --local --replace-all homebrew.private true

## # X-code인스톨

$ sudo xcode-select --install

# **３. 최신 버젼의 ruby를 인스톨**

## # 버젼 리스트를 확인

$ rbenv install --list

2.4.3

2.5.0-dev

2.5.0-preview1

2.5.0-rc1

2.5.0

2.6.0-dev

2.6.0-preview1

현재 확인가능한 버젼은 2.5.0가 제일 최신의 안정판으로 보이므로(?) 2.5.0를 넣을 예정

## \#ruby의 최신 버젼을 인스톨

$ rbenv install 2.5.0

# **４. 버젼이 반영되지 않을 경우**

## # ruby의 버젼 확인

$ ruby -v

ruby 2.3.3p222 **(**2016-11-21 revision 56859**) [**universal.x86_64-darwin17]

ruby의 버젼을 확인했는데 mac의 디폴트 버젼 그대로인 상황

그럼 benv의 버젼은? …제대로 2.5.0가 표시됨

## # rbenv의 버젼 확인

$ rbenv versions

system

- 2.5.0 **(**set by /Users/yjpark/.rbenv/version**)**

witch ruby커맨드의 결과가 아래의 경우는 PATH설정이 부족한게 원인

$ witch ruby

/usr/bin/ruby

해결방법은 ~/.bash_profile에 [eval "$(rbenv init -)"](rbenv init의 PATH설정)을 추가

$ rbenv init

eval "**$(**rbenv init -**)**" _\#이 내용을 복사해서~/.bash_profile에 추가_

~/.bash_profile의 내용을 수정

$ vim ~/.bash_profile

$ source ~/.bash_profile

다시 ruby의 버젼을 확인. 2.5.0가 표시되는걸 확인할 수 있음

$ ruby -v

ruby 2.5.0p0 **(**2017-12-25 revision 61468**) [**x86_64-darwin17]

which ruby도 확인해 보자

$ which ruby

/Users/**{**user_id**}**/.rbenv/shims/ruby

이걸로 설정 끝