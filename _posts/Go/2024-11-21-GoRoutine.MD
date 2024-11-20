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
# Go Routine
> 다른 언어들에 나오는 Thread보다 간단하고 리소스를 적게 생성하는 Go의 병렬처리를 담당하는 기능이다.   

사용법은 정말 간단하다 go f() 그저 함수 앞에 go를 붙이면 끝. 하지만 그저 여러 개의 쓰레드를 돌리기만 한다면 메리트는 딱히 없다고 생각한다.~~물론 다양한 환경에서 다중 쓰레드를 많이 써본적은 없다.~~ 그래서 go에는 channel이나 셀렉터 등등 다양한 고루틴을 활용하는 방법들이 있다.

## Channel
> 고루틴끼리 데이터를 주고 받고 흐름을 제어할 수 있는 기능

변수 := make(chan type) 식으로 선언하면 된다.   
변수 := make(chan type,buffer size) 이런 식으로 사이즈를 지정해서 사용도 가능하다. 

``` go
func main(){
    ch := make(chan int,3)

    go func(){
        for i:=0;i<100;i++{
            ch<-i   //여기서 ch가 가득차게 되면 대기를 시작
        }
    }()
    
    for i:=0;i<100;i++{
        <-ch    //여기에서 ch에 쌓인 데이터를 꺼냄 값이 없다면 대기함.
    }
}
```
따라서 위의 코드는 
1. ch에 값이 3개 들어갈 때 까지 위쪽 go 함수가 실행
2. 가득차면 아래의 for문이 실행된다.
3. 값을 다 꺼내게되면 반복
