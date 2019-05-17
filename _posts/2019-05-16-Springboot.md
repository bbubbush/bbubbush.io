---
layout: post
title: Springboot - 간단한 Hello world 출력하기
category: Springboot
categories: [Springboot]
author: bbubbush

---

Spring을 공부할 겸 새롭게 시작하는 스터디에서 첫 과제로 Springboot로 구성한 환경에서 Hello world를 출력하여 가져오기로 하였습니다.

간단한 과제인 만큼 포스팅해보는 것도 좋을 것 같아 진행한 순서대로 기록하고자 합니다.

우선 본인은 IDE로 Intelli J(인텔리제이)를 사용하였습니다.

먼저 프로젝트를 생성해보겠습니다.
![프로젝트만들기](/assets/img/springboot/2019-05-16_project_01.png){: .center .img}

다음으로 Spring Assistant를 선택하여 Spring boot 프로젝트를 만들겠습니다.
![새 프로젝트 생성](/assets/img/springboot/2019-05-17_project_02.png){: .center .img}

만약 왼쪽에 Spring Assistant 메뉴가 없다면 Preferences를 열어줍니다.(맥에서는 command + , 단축키로 열 수 있습니다.)
![Preferences 찾기](/assets/img/springboot/2019-05-17_project_03.png){: .center .img}

그 다음 plugins 메뉴에서 Spring Assistant를 검색하여 설치해줍니다. 전 이미 설치되어있기 때문에 Installed로 나오네요 : )
![Plugins에 인스톨하기](/assets/img/springboot/2019-05-17_project_04.png){: .center .img}

이제 다시 프로젝트를 만들어보겠습니다. 새로운 프로젝트는 꼭 Gradle project로 만들어 주세요
[참고자료: Maven vs Gradle](https://bkim.tistory.com/13)

![프로젝트 정보입력](/assets/img/springboot/2019-05-17_project_05.png){: .center .img}

