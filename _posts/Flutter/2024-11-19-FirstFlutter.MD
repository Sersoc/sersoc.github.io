---
title: Flutter입문
date: 2024-11-19 23:05:10 +09:00
categories: [Language, Flutter]
tags:
  [
    Flutter,
    Dart,
    개발
  ]

---
# Flutter 입문
> 프론트 앱이라곤 윈도우 앱 밖에 다뤄보지 못해 물경력을 쌓고 있는 사람이다. ~~그것도 Delphi WPF라는 매우 오래된 프레임워크밖에 다뤄보지 않았다~~ 그래서 경험을 쌓고자 빠르게 입문 가능한 Flutter를 선택했다.   

## Flutter 개요
### Dart라는 언어를 사용해 프론트앱을 개발하는 Google에서 개발한 프레임워크
### 위젯을 Drag&Drop으로 구성하는 듯한 편리함
### Dart가 Java와 구조가 유사하여 대학생 때의 기억을 더듬어 쉽게 배울 수 있다.(객체지향언어)
### 필요한 기능이 있으면 쉽게 package를 불러와 사용할 수 있다.

## 환경 셋업
### 준비물
- Visual Studio Code   

1. 익스텐션에서 Flutter, Dart를 다운받아 주자.
2. mac기준(cmd + shift + p)를 누르고 Flutter: New Project를 선택해주자.
3. base프로젝트 생성완료

환경변수나 다른 것을 설정해준 기억은 없다. 가끔 github에서 받은 프로젝트가 import부터 안될 때가 있는데 이는 yaml파일에서 버전이 오래된 것으로 되어있는 문제일 가능성이 크니 확인해보자.

``` dart
//생성된 기본 프로젝트
import 'package:flutter/material.dart'; //Dart관련 패키지들을 import하는 듯 하다.

void main() {                // void main() => runApp(MainApp()); 도가능
  runApp(const MainApp());              //MainApp 실행
}

class MainApp extends StatelessWidget { //StatelessWidget을 상속받은 MainApp
  const MainApp({super.key}); // 없어도 됨

  @override 
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Center(
          child: Text('Hello World!'),//화면 중앙에 Hello World!가 찍힌다.
        ),
      ),
    );
  }
}

```
Flutter 프레임워크에 대한 아키텍쳐들도 다뤄보고 싶지만 그런것들까지 다 정리할 물리적인 시간이 부족하기 때문에 공부하면서 잘안됐던 부분들을 정리할 생각이다.