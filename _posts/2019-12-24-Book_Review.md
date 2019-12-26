---
layout: post
title: <그림으로 배우는 Http Network Basic> Chapter4. 결과를 전달하는 HTTP 상태 코드
category: Book_Review
categories: Book_Review
author: bbubbush
comments: true
---
"404" 를 보시면 어떤 생각이 드시나요? 개발자는 물론이고 개발에 관심 없는 분이여도 숫자 4가 주는 부정한 기운에 선뜻 좋은 의미로 느껴지진 않습니다. 하지만 어떤 미신이든 유래를 알고 나면 시시해지기 마련입니다. 

한자에서는 4는 '죽은 사'와 동일한 발음으로 사용되어 부정적인 의미로 사용되며, 한자 문화권인 한국 역시 동일하게 생각하였습니다. 일본에서도 4는 '시'로 발음이 되며 이는 죽음을 의미하는 단어와 같은 발음으로 읽힙니다. 

마찬가지로 개발을 처음 할 때 느끼는 404에 대한 두려움은 원인을 이해함으로써 극복할 수 있습니다. 

서버에서 전달되는 response에는 status 라는 결과의 상태를 표시하는 값이 있습니다. 404로 이에 대한 한 종류에 속합니다. 아래는 각 상태값의 대분류와 소분류의 의미들을 표기한 내용입니다.

> 1xx : request를 처리하는 중
>
> 2xx : request를 정상적으로 처리
>
> - 200 OK: request를 정상적으로 처리
> - 204 Not Content : request를 정상적으로 처리하였으나 돌려줄 response body 값이 없음
> - 206 Partial Content : 서버가 부분적인 request를 받았을 경우, 해당 상태로 응답
>
> 3xx : request를 완료하기 위해 브라우저 측에서 추가 작업이 필요
>
> - 301 Moved Permanently : request 된 URI가 새로운 URI로 '완전히' 변경된 경우
> - 302 Found : request 된 URI가 새로운 URI로 '임시적인' 변경이 된 경우
> - 303 See Other : 302와 동일하지만, 'redirect 장소를 GET으로 얻어야 한다고 명확하게 정의' 된 점이 다름 
> - 304 Not Modified : 이전의 동일한 요청과 비교하여 변화가 없는 경우. 단 시간의 반복적인 요청에 대한 해결방법이 된다.
> - 307 Temporary Redirect : 302와 동일하나 Method의 변경을 금지
>
> 4xx : 클라이언트의 잘못된 요청
>
> - 400 Bad Request : request가 잘못 요청된 경우. 브라우저는 200과 동일하게 취급
> - 401 Unauthorized : request에 HTTP 인증 정보가 필요한 경우
> - 404 Not Found : request한 리소스가 없는 경우
>
> 5xx : 서버의 처리 중 오류가 발생
>
> - 500 Internal Server Error : 서버에서 처리하는 중 에러가 발생한 경우
> - 503 Service Unavaliable : 서버가 과부하거나 점검 중이여서 request를 처리할 수 없는 경우

포스팅의 서두에 언급된 404 상태코드는 **Request에 요청된 리소스가 없는 경우** 입니다. 즉, 요청하는 URI정보를 검토해보거나, 서버측헤 해당 URI가 존재하는지 확인해보는 방법을 통해 해결할 수 있습니다. 뿐만 아니라 위 상태 코드들은 개발하면서 자주 만나게 될 테니 본인만의 방법으로 기억해두면 트러블 슈팅을 보다 빠르게 할 수 있습니다.



##### 결론

웹 개발 시에 오류가 발생하면 [개발자 도구 - 네트워크] 탭을 통해 각 request와 response의 상태값을 확인하여 무엇이 문제인지 유추하는 습관을 기르면 좋다!!



오늘도 읽어주셔서 감사합니다 : )