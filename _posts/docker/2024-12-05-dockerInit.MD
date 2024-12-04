---
title: DockerFile로 이미지 만들기
date: 2024-12-05 01:00:10 +09:00
categories: [Cloud, Docker]
tags:
  [
    Docker,
    Go
  ]

---
# Docker image(with. Go)
```go
//Server
package main

import (
	"fmt"
	"net"
)

func requestHandler(c net.Conn) {
	data := make([]byte, 4096)  //주고 받을 데이터는 슬라이스로 선언

	for {                       //무한 반복 
		n, err := c.Read(data)  //받은 데이터 읽기
		if err != nil {
			fmt.Println(err)
			return
		}

		fmt.Println(string(data[:n])) // 받은 데이터 출력

		c.Write(data[:n])    //받은 데이터 리턴

		if err != nil {
			fmt.Println(err)
			return
		}
	}
}

func main() {
	ln, err := net.Listen("tcp", ":3000")   //3000port 대기

	if err != nil {
		fmt.Println(err)
		return

	}

	defer ln.Close()                        //main 함수 종료 시 호출 되어 대기 멈춤

	for {
		conn, err := ln.Accept()            // port에 신호가 들어오면 전달

		if err != nil {
			fmt.Println(err)
			continue
		}

		defer conn.Close()

		go requestHandler(conn)             // go routin으로 실행
	}
}

```
```go
//Client
package main

import (
	"fmt"
	"net"
	"strconv"
	"time"
)

func main() {
	client, err := net.Dial("tcp", "127.0.0.1:3000")

	if err != nil {
		fmt.Println(err)
		return

	}
	defer client.Close()

	go func(c net.Conn) {
		data := make([]byte, 4096)

		for {
			n, err := c.Read(data)
			if err != nil {
				fmt.Println(err)
				return

			}
			fmt.Println(string(data[:n]))

			time.Sleep(1 * time.Second)
		}

	}(client)

	go func(c net.Conn) {
		i := 0
		for {
			s := strconv.Itoa(i)

			c.Write([]byte(s))
			if err != nil {
				fmt.Println(err)
				return
			}

			i++
			time.Sleep(1 * time.Second)
		}
	}(client)

	fmt.Scanln()
}

```

>코드는 localhost에서 3000port를 열고 통신을 하는 코드다. 이중에 서버쪽 코드를 Dockerfile로 이미지를 만들고 컨테이너를 실행시켜보았다.
### 1. DockerFile 준비

``` docker
# 빌드 단계
FROM golang:1.20 AS builder
WORKDIR /app
COPY . .
RUN CGO_ENABLED=0 GOOS=linux go build -o main .

# 실행 단계
FROM scratch
WORKDIR /app
COPY --from=builder /app/main .
EXPOSE 3000
CMD ["./main"]

```

### 2. docker build
```shell
$ docker build . -t goserver
```
이렇게 하면 goserver라는 docker image가 생성된다. 이제 컨테이너로 실해시키자.

### 3. Container run
```shell
$ docker run --name testserver --rm -p 3000:3000 goserver
```
--name  은 컨테이너의 이름을 설정, --rm은 컨테이너가 종료될 시 컨테이너를 삭제한다는 선언, -p 3000:3000 호스트에서 3000번대로 접근하고 컨테이너 내부적으로도 3000번대를 연결시킨다.

### 4. 신호 날려보기
이제 클라이언트 코드를 실행시켜 통신이 되는지 확인해보자. 
