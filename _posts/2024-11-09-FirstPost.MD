---
title: GitHub Blog 세팅하기 (1)
date: 2024-11-09 02:45:10 +09:00
categories: [SetUp, GitBlog]
tags:
  [
    github.io,
    github,
    개발
  ]

---
> 공부를 하면서 정리도 하고 복습도 겸행하기 위해 여러 블로그들(Tstory,velog,WordPress 등)을 알아봤지만 특별한게 없을까 하다가 평소 두려워서 도전해보지 못했던 Gitblog를 도전해보기로 했다. 자료를 찾아보고 세팅을 하는데 22시부터 4시30분까지 여름이었으면 거의 동이 틀 무렵까지 진행했다.   

> Setting 기준은 ruby, jekyll 등이 설치되어 있지 않았던 MacOS에서 진행했다.(기억을 더듬어가면서 기록하기 때문에 중간중간 빠져있는 부분이 있을 수 있다.)

### _ruby_ 설치 순서
## 1.rbenv 설치
``` shell
$ brew install rbenv
```
rbenv로 원하는 버전의 ruby를 설치하고 버전을 쉽게 바꿀 수 있다.
## 2._ruby_ 설치
``` shell
// ruby 버전이 낮으면 여러가지 에러가 뜰 수 있기 때문에 
// 아래 커맨드로 최신 버전을 확인하고 설치하는게 좋다.Ex.(Gem::FilePermissionError)
// 실제로 에러가 한참 떠서 찾아보니 ruby버전이 낮아서 그랬다.
$ rbenv install -l 

// 버전 확인 후 원하는 버전 입력하여 설치
$ rbenv install 3.1.6

// 설치된 버전으로 세팅
$ rbenv global 3.1.6
```

## 3._ruby_ Path 등록
``` shell
// vi로 ruby path를 등록해준다.
$ vi ~/.zshrc
// 편집기 실행 후 하단의 path등록 
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
// 저장할 땐 :입력 후  wq를 치고 엔터를 치면 저장이 된다.
// source로 해당 내용 적용
$ source ~/.zshrc
```
이제 gem명령어를 실행할 수 있다.   
jekyll을 설치해주자.
## jekyll&bundler install
jekyll&bundler 설치는 간단하다.
```shell
$ gem install jekyll  
$ gem install bundler

// 설치가 끝나면  -v 명령어로 버전확인 및 설치가 제대로 됐는지 학인하자
$ jekyll -v
$ bundler -v 
```
## What's Next
이제 블로그 개설에 필요한 프로그램 세팅은 끝났으니 블로그를 만들 차례다.   
[GitHub Blog 세팅하기 (2)](https://sersoc.github.io/posts/SecondPost/)
