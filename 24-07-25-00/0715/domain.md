# 도메인, domain

## 1. 개념

1. 어원: dominate
2. 이름을 붙이는 일
3. IP 주소에 매핑되는 텍스트 문자열
4. `.`로 구분되고 오른쪽에서 왼쪽으로 읽는 구조

<aside>
<p><b>💡 dominate, 지배하는 법칙</b></p>

<p>
  마치 사람의 성처럼 suffix(접미사)가 가장 상위의 개념이다.
  prefix(접두사)를 설정할 수 있다.
  prefix를 소유한 게 누구인지 알기 위해서는 domain name space를 봐야한다. 
  domain name space는 global, logical, hierarchical(tree-shaped) naming 구조이다.
</p>

</aside>

## 2. 분류

1. 최상위 도메인(Top Level Domain, TLD)
    1. 개념
        1. 도메인의 가장 오른쪽 부분
        2. ex) naver.`com` , korea.ac.`kr`
    2. 종류
        1. 일반 최상위 도메인(Generic Top Level Domain, gTLD)
            1. 특정 주제나 목적을 나타냄
            2. com: commercial
            3. net: network
            4. org: organization
        2. 국가 코드 최상위 도메인(ccTLD, country code Top Level Domain)
            1. 나라나 지역을 나타내는 코드로 구성됨
            2. ex) kr (korea), us(미국)
2. 2차도메인(Second Level Domain, SLD)
    1. 개념
        1. TLD 바로 왼쪽에 있는 것
        2. 왼쪽으로 갈수록 차수가 1씩 높아짐
        3. ccTLD의 경우에는 대개 SLD 에서 웹사이트의 특징 (원래 TLD의 역할이었던 것) 을 부가적으로 나타냄
            1. ex) ac: academic, co: commercial, go: government, mil: military, re: research
            2. 그래서 특별하게 이런 경우에는 ccSLD라고 부르거나 혹은 여기까지 합쳐서  TLD로 보기도 함
3. 루트 도메인
    1. 웹 사이트의 최상위 계층
    2. DNS의 맥락에서 루트 도메인이라는 용어는 `.` 으로 표현되는 가장 높은 계층의 도메인을 뜻함
    3. ex) 도메인: [example.com](http://example.com) ⇒ root domain: example.com
    4. 도메인 이름의 가장 단순화된 형태
    5. 같은 뜻 다른 이름
        1. 베어(bare) 도메인
        2. 에이펙스(apex) 도메인
4. 서브 도메인
    1. 개념
        1. 루트 도메인에서 용도를 구분하기 위해 여러 서브 도메인을 만들 수도 있음
        2. ex) 네이버의 경우
            1. 홈: www.naver.com
            2. 지도: map.naver.com
            3. 사전: dictionary.naver.com
        3. ex) 고려대학교
            1. 포탈: portal.korea.ac.kr
            2. 도서관: library.korea.ac.kr
            3. 우리과: and.korea.ac.kr