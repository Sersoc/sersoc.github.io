---
title: GitHub Blog 세팅하기 (3)
date: 2024-11-09 18:46:10 +09:00
categories: [SetUp, GitBlog]
tags:
  [
    github.io,
    github,
    개발
  ]

---
> 이제 가장 내 골머리를 썩혔던 부분이다. Local환경에서 동작은 잘되는데 Github에서 빌드가 계속 막혀서 잠을 못잤다.(비슷한 이유로 계속 실패하고 사소한 차이로 빌드를 못하고 있었다..) 이 부분을 해소하고 나면 앞으로 commit push 만 하면 블로그를 업데이트 할 수 있다.
![Failed List](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Failed.png?raw=true)


해답은 ([하얀눈길 블로그](https://www.irgroup.org/posts/jekyll-chirpy/))이 분의 포스트에서 찾을 수 있었다.
## 첫번째 에러
```  shell
build
 Logging at level: debug Configuration file: /github/workspace/./_config.yml Theme: jekyll-theme-chirpy github-pages 232 | Error: The jekyll-theme-chirpy theme could not be found. 
```
이 에러는 Chrirpy 테마를 찾을 수 없다는 에러인데, 자세한 이유는 잘 모르겠지만 아래의 방법대로 진행하면 해결할 수 있다.
### 저장소 세팅 변경하기
![Setting](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/PageSetting.png?raw=true)


> Repo -> settings -> pages -> build & deployment에서 source를 이미지처럼 Github Action으로 바꿔주자. 그러면 이미지에는 안나오지만 jekyll.yml파일을 추가하라고 뜬다. 이를 추가해주자   


## 두번째 에러
그런데 github action에서 이런 에러가 떳다. 이 에러도 간단하게 해결가능하다.
``` shell
build
Process completed with exit code 1.
```
![Fix Err](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Fixerr.png?raw=true)

위에서 추가한 jekyll.yml 파일에서 Build With jekyll 위에 npm 의존성을 추가해주자 그럼 깔끔하게 해결이 된다.

## 나만의 Github Blog 개설 완료
![결과창](https://github.com/Sersoc/sersoc.github.io/blob/main/assets/img/postingImage/PostBlog/Complete_Page.png?raw=true)

이제 나만의 블로그가 개설되었다. 중간중간에 빼먹은 부분이 있을지도 모르겠지만, 일단 Test용으로 만들었던 블로그도 제대로 동작하는걸 보니 문제는 없을것 같다. 

참고로 _config.yml을 이용해 블로그를 꾸밀 수 있으니 잘 찾아보며 꾸며보자   
**-The End-**