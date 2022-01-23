---
layout: post
title: "inflearn 스프링 입문 강의 정리"
tag : inflearn, spring
---

**김영한 강사님의 '스프링 입문 - 코드로 배우는 스프링 부트, 웹 MVC, DB 접근 기술' 강의 정리**

2020.12.21~02.06 진행
<br>
강의를 들으며 노션에 적어두었던 걸 보기 쉽게 정리해서 포스팅 해보려 한다.  
처음으로 스프링을 시도해보았는데 재밌고 들떴던 기억이 난다  
아무래도 무료 강의다 보니, 뒤이어 학습한 스프링 핵심원리 기본편, MVC편과 겹치는 부분이 있어

스프링 환경설정 위주로만 작성했다.

## 프로젝트 환경 설정

-   Java 11
-   IDE : IntelliJ
-   스프링 부트 스타터 사이트로 스프링 프로젝트를 생성 [https://start.spring.io](https://start.spring.io)
-   Group: 기업도메인명
-   Artifact : 프로젝트명
-   Dependencies : 필요한 라이브러리 선택
    -   Spring Web
    -   Thymeleaf ( html을 만들어주는 템플릿 엔진, 여러 종류가 있음)test도구인 junit5 라이브러리가 기본으로 포함된다. 소스 라이브러리에 톰캣(웹 서버)도 내장되어 있다.

> **maven, gradle 이란?** 필요한 라이브러리를 땡겨오고, 빌드하는 라이프사이클, 의존관계 까지 관리해주는 툴. 과거에는 maven을 많이썼지만 요즘에는 gradle로 넘어오는 추세이다.

## 스프링 부트 라이브러리

-   spring-boot-starter-web
    -   spring-boot-starter-tomcat : 톰캣 (웹서버)
    -   spring-webmvc : 스프링 웹 MVC
-   spring-boot-starter-thymeleaf : 타임리프 템플릿 엔진(View)
-   spring-boot-starter(공통) : 스프링 부트 + 스프링 코어 + 로깅
    -   spring-boot
        -   spring-core
    -   spring-boot-starter-loggin
        -   logback, slf4j

참고

-   spring-boot-devtools : html 파일을 컴파일만 해주면 서버 재시작 없이 View 파일 변경이 가능하다. (인텔리J컴파일 방법 : 메뉴 build → Recompile)

## 테스트 라이브러리

-   spring-boot-starter-test
    -   junit : 테스트 프레임워크
    -   mockito : 목 라이브러리
    -   assertj : 테스트 코드를 좀 더 편하게 작성하게 도와주는 라이브러리
    -   spring-test : 스프링 통합 테스트 지원

## welcome page

-   resources/static/index.html

## 서버 배포 시

-   프로젝트 폴더에서 gradlew build 명령어로 빌드 실행
-   프로젝트 폴더/build/libs에 생성된 jar파일을 복사해서 서버에 넣는다.
-   서버에서 java -jar <jar파일>.jar 명령어를 입력해 실행

## 정적 컨텐츠

(톰캣 서버 → 스프링컨테이너) 컨트롤러가 없으면 static 폴더에 있는 html을 그대로 반환한다.

## 동적 컨텐츠

과거에는 컨트롤러와 뷰가 따로 분리되어 있지 않아 jsp로 모두 다하는 model1 방식을 사용했다. view는 화면에 관련된 일만, controller는 비즈니스 로직으로 분리 하기 위해서는 템플릿 엔진이 필요하다.

> **템플릿 엔진이란?** JSP, PHP와 같이, 서버에서 프로그래밍 해서 html을 동적으로 바꿔주는 것. 이를 위해 컨트롤러, 모델, 뷰가 필요 → MVC