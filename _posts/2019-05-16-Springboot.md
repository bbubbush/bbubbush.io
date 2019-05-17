---
layout: post
title: Springboot - Intelli J로 간단한 Spring boot 프로젝트 만들기
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

이제 다시 프로젝트를 만들어보겠습니다. 새로운 프로젝트는 꼭 Gradle project로 만들어 주세요.
[참고자료: Maven vs Gradle](https://bkim.tistory.com/13)

![프로젝트 정보입력](/assets/img/springboot/2019-05-17_project_05.png){: .center .img}

프로젝트를 구성할 dependency를 선택해줍니다. 저는 최소한으로 만들기 위해 아무것도 없이 next를 눌렀습니다. 그랬더니 최소 하나는 선택해달라고 하네요...ㅠ
그래서 Web을 선택하였습니다. 이런 편리함 때문에 Spring Assistant를 사용하게 되는 것 같습니다.

![dependency 선택](/assets/img/springboot/2019-05-17_project_06.png){: .center .img}

마지막으로 생성할 프로젝트의 이름과 경로를 선택하시면 기나긴 프로젝트 생성이 마무리 됩니다.
![프로젝트명과 경로 설정](/assets/img/springboot/2019-05-17_project_07.png){: .center .img}

새로운 프로젝트가 만들어지면 아래와 같은 안내창이 뜹니다. 그러면 꼭 'Use default Gradle Wrapper' 옵션을 선택해줍니다.
Gradle Wrapper는 운영체제에 맞게 Gradle 빌드를 수행하는 배치 스크립트입니다. 별도의 설정이 필요 없으므로 해당 옵션을 사용하길 권장합니다.
![gradle import](/assets/img/springboot/2019-05-17_project_08.png){: .center .img}

자, 여기까지 하고 나면 필요한 파일을 Gradle을 통해 다운로드 받을 수 있도록 기다려줍니다.
![file download](/assets/img/springboot/2019-05-17_project_09.png){: .center .img}

이제 프로젝트를 실행할 수 있는 상태가 되었습니다. 우선 테스트파일을 통해 정상적으로 실행되는지 확인해보겠습니다.
기본으로 제공되는 테스트 메소드의 이름을 "헬로월드"로 바꿔주고 출력문도 하나 추가해줍니다.
![테스트 메소드 생성](/assets/img/springboot/2019-05-17_project_10.png){: .center .img}

메소드를 작성한 후 오른쪽 버튼을 눌러 [Run 헬로월드]를 실행해줍니다.
![테스트 메소드 실행](/assets/img/springboot/2019-05-17_project_11.png){: .center .img}

정상적으로 실행되었습니다. 짜잔! 드디어 스프링부트 프로젝트를 생성하였습니다.
![테스트 성공](/assets/img/springboot/2019-05-17_project_12.png){: .center .img}

다음으로는 실제로 내장WAS를 실행하여 결과를 확인해보겠습니다. 먼저 아래 그림과 같이 기본적인 패키지와 컨트롤러를 생성해줍니다.
![패키지 및 컨트롤러 생성](/assets/img/springboot/2019-05-17_project_13.png){: .center .img}

HelloController는 아래와 같이 만들어 기본적인 텍스트가 출력될 수 있게 코딩해줍니다.
![컨트롤러 내용](/assets/img/springboot/2019-05-17_project_14.png){: .center .img}

마지막으로 HelloApplication파일을 선택 후 오른쪽버튼을 누르면 [Run HelloApplication main()]이 있습니다.
![프로그램 실행](/assets/img/springboot/2019-05-17_project_15.png){: .center .img}

이를 클릭한 후 웹사이트 주소창에 http://localhost:8080 이렇게 입력하면 아래처럼 Hello World를 출력해줍니다.
![헬로 월드](/assets/img/springboot/2019-05-17_project_16.png){: .center .img}

이것으로 스터디 첫 번째 과제에 대한 포스팅과 더불어 스프링 부트 프로젝트 생성하기를 마치겠습니다.

#### 긴 글 읽어주셔서 감사합니다 :)