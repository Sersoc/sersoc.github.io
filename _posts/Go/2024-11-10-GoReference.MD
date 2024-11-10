---
title: Go 포인터 & 레퍼런스 타입(Slice,Map,Channel)
date: 2024-11-10 18:24:10 +09:00
categories: [Language, GoLang]
tags:
  [
    Go,
    GoLang,
    개발
  ]

---
> 레퍼런스 타입을 이해하기 위해서는 먼저 포인터를 이해할 필요가 있다.

## Pointer
### Pointer 선언
```go
var p *int // 초기화를 해주지 않으면 값을 nil로 생성됨 
           // 이렇게 nil로 되어 있는 포인터에는 값을 변경할 수 없음.

var p *int = new(int) //int 타입의 새로운 주소가 할당됨

var *p = 1 // 할당받은 주소에 역참조를 통해 값을 대입
```
포인터는 메모리 주소값을 저장하여 바로 할당된 주소에 접근할 수 있게 해준다. 위와 같이 변수 p에 대한 값만 변경하면 일반 변수랑 크게 다를바 없어 보인다. 아래의 예시를 보자
``` java
public class HelloWorld {
    public static int add(int num){ //num + 1 을 반환하는 메서드
      return num + 1;
    }
    public static void main(String[] args) {
        int num = 1;
        num = add(num);
        System.out.println(num);
    }
}
```
java에서는 직접 메모리 주소에 접근할 수 없기 때문에 값을 리턴받고 다시 대입해줘야한다.
``` go
import "fmt"

func add(num *int){   //int형 타입의 메모리 주소값을 파라미터로 받는 함수
  *num += 1
}
func main(){
  var num = 1       // num 선언
	add(&num)         // &num으로 주소값을 넘겨줌
	fmt.Println(num)  //출력값은 2
}
```
java에서와 달리 add라는 함수도 리턴값이 없고 num변수에 값을 새로 대입하지 않아도 num변수의 값은 변경되어 있다. 메모리 주소를 전달 받았고 그것을 역참조해서 값을 입력해줬기 때문이다.   
이렇게 메모리에 직접 엑세스할 수 있도록 해주는 것이 포인터고 이를 이해하고 레퍼런스 타입을 보면 좀 더 이해가 수월할 것이라고 생각된다.~~(그래도 나는 아직 조금 레퍼런스 타입이 어렵다.)~~

## 레퍼런스 타입
> 레퍼런스 타입은 포인터 처럼 메모리 주소값을 참조하는 타입이다. 하지만 주소값을 직접 드러내는 일은 없고 내부에서 참조해서 처리하는 타입이다. 따라서 레퍼런스 타입의 변수를 선언하고 이를 다른 변수에 대입시켰을 때 둘 중 하나의 값이 변경되면 같이 값이 변경된다. 
### 1.Slice
배열과 유사하지만 엄연히 다르다. 아래는 일반적인 Go의 배열
``` go
var arr [3]int = [3]int{1,2,3}//크기가 3인 배열 
var arr = [3]int{1,2,3}//크기가 3인 배열
arr :=[...]int{1,2,3} //크기가 3인 배열
```
Slice
``` go
// make([]type,길이,용량)을 사용해 공간할당 
var arr []int = make([]int,5)//길이가 5인 int type slice
var arr = make([]int,5)
arr := make([]int,5)


```
