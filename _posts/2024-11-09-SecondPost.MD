---
title: GitHub Blog 세팅하기 (2)
date: 2024-11-09 17:49:10 +09:00
categories: [SetUp, GitBlog]
tags:
  [
    github.io,
    github,
    개발
  ]

---
> 개요 : 앞서 필요 프로그램들의 설치를 끝냈으니 서버를 포스팅하기 전에 로컬에서 블로그를 띄워볼 차례다.

## Github 저장소 생성
먼저 github에서 **{$_GithubID_}.github.io** 형식으로 저장소를 새로 만들어준다.
![저장소 생성 페이지](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/MakeRepo.png?raw=true)
> 현재 이미 블로그를 개설한 상태기 때문에 에러가 뜬다. 처음 생성할 땐 에러가 뜨지 않으며 이후 세팅을 위해 readme나 ignore 같은건 생성하지 말자   
(파일이 하나라도 있다면 jekyll로 프로젝트 생성 시 에러가 뜸)

## Project Setting
> 많은 사람들이 템플릿을 Chirpy를 사용해 개설을 했길래 같은 템플릿을 가져와 진행하였다.   
> ([Chirpy 템플릿 링크](http://jekyllthemes.org/themes/jekyll-theme-chirpy/))
> 만약 템플릿을 적용해보고 싶다면 링크로 들어가서 설치 후 압축을 풀어두자   
> 현재 포스트에서는 좀 더 쉬운 이해를 위해 처음부터 Test라는 폴더를 생성해 로컬 환경에서 실행하는 과정을 나타낸다.

이제 빈 저장소가 생성이 됐을 것이다. 이를 로컬 저장소에 git clone을 통해 불러오자.
이제 jekyll를 사용해 프로젝트를 세팅해준다.
``` shell
// 터미널이 열려있는 위치에 기본 세팅이 된다.
$ jekyll new ./
```
![jekyll new in terminal](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Terminal_jekyll_new.png?raw=true)

installed in ~ 이라고 뜨면 초기 셋업은 완료됐다. 로컬 저장소에서 생성된 파일들을 확인해보자.
## 템플릿 적용
![jekyll new in terminal](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Result_jekyll_new.png?raw=true)

> 이제 템플릿 링크에서 받은 파일을 전부 옮겨준다.

템플릿 이동 후 삭제해줘야 되는 파일들이 있다.
 - _posts folder(앞으로 블로그에 게시할 포스트 항목들을 저장하는 폴더)
 - Gemfile.lock file (bundler install 실행 후 다시 생긴다)
 - _docs folder
삭제가 완려되었으면 아래의 명령들을 실행시켜주자 그럼 삭제했던 파일 몇개가 다시 생성될 것이다.
``` shell
$ bundler install
$ bundler update 
$ bundler exec jekyll serve 
```
![jekyll new in terminal](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Ip.png?raw=true)
> 이미지에 보이는 것처럼 server address가 나온다. 여기로 치고 들어가면

![jekyll new in terminal](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Result_page.png?raw=true)
> 위 이미지처럼 Chirpy 템플릿이 적용된 블로그가 생성되었다. 이제 이를 Github에 등록하고 즐겨보자

## What's Next
[GitHub Blog 세팅하기 (3)](https://sersoc.github.io/posts/ThirdPost/)
