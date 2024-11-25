---
title: GoRoutine
date: 2024-11-21 00:07:10 +09:00
categories: [Language, GoLang]
tags:
  [
    Go,
    GoLang,
    개발
  ]

---
# Go프로젝트 관리
## Gopath
나는 계속 Go를 책을 보며 공부를 하고 있다. 그런데 Go 프로젝트를 만들 때 마다 Gopath를 설정해야 된다거나, 이번에 새로 공부한 Go Custom Package를 만들 때 또한 Gopath 하위에서 관리를 하는 등 매우 불편한 상황이 이만저만이 아니었다. 그래서 찾아보니 1.16버전부터는 **Go모듈**로 패키지를 보다 수월하게 관리할 수 있다고 한다. 

기존 프로젝트구조를 잠깐 보고 넘어가자.   

Project(Gopath)   
|   
|__pkg   
|__bin   
|__src   

이런 식으로 프로젝트가 고정으로 되어있었다.하지만 **GO모듈**을 사용하면 훨씬 자유롭다.

## Go모듈로 프로젝트 구성하기

일단 프로젝트 구조가 기존에 비해 자유로워졌다. 새로 프로젝트를 생성할 때 마다 Gopath를 설정할 필요 없다.
``` shell
$ go mod init ProjectName
```
이런식으로 터미널에 입력해주면 go.mod go.sum이란 파일이 생성되어 프로젝트 의존성 관리를 해준다. 아래는 테스트 용으로 만든 프로젝트 구조다.   
> go mod tidy명령어로 의존성을 정리할 수 있다.    



Project   
|go.mod   
|go.sum   
|main.go  
|calc   
|__sum.go   
|__multi.go   

새로운 프로젝트 모듈을 초기화해서 __go.mod__ __go.sum__ 파일이 생겼고, 추가로 calc라는 패키지 디렉토리를 생성해 Sum(),Multi()라는 함수를 언제든 사용할 수 있게 했다.
``` go
//sum.go
package calc

func Sum(a int, b int) int {
	return a + b
}
//multi.go
package calc

func Multi(a int, b int) int {
	return a * b
}
```
## 패키지 
Go를 공부하면서 게속 흥미가 생기지만 지금 더욱 마음에 드는 것이 패키지를 쉽게 배포하고 쉽게 관리할 수 있다는 점이다.
먼저 패키지를 배포하는 방법을 보자
### 패키지 배포하기
1. 배포하고자 하는 폴더에 들어가서 __go mod init github.com/username/repository__ 실행   
2. 이제 레포지토리에 푸쉬하면 끝

### 패키지 불러오기
1. 프로젝트 폴더에 들어간다.
2. __go get github.com/username/repository__    

패키지 설치는 끝났다. 이제 실제로 사용해보자.
```go
package main

import (
	"fmt"

	"github.com/Sersoc/calc"
)

func main() {
	fmt.Println(calc.Sum(1, 2))   //3
	fmt.Println(calc.Multi(2, 3)) //6
}
```

> 버전 관리도 git tag V1.0.0 이렇게 태그로 관리할 수 있다. 이렇게 버전 관리를 해주면 go get ~~@Version 이런 식으로 필요헌 패키지를 필요한 버전으로 불러올 수 있다.


