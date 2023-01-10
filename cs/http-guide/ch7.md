# 🎯 Chapter 7: HTTP 헤더1 -일반헤더

## 🍄 1. HTTP 헤더 개요

### 🌻 1-1. HTTP 헤더 예시

- header-field = field—name “:” OWS field-value OWS
- field-name은 대소문자 구문 없음
- *OWS 는 띄어쓰기 허용

```
Content-Type: text/html;charset=UTF-8
Content-Length: 3423
```

### 🌻 1-2. HTTP 헤더 용도

- HTTP 전송에 필요한 모든 부가정보
- 예) 메시지 바디의 내용, 메시지 바디의 크기, 압축, 인증, 요청 클라이언트, 서버 정보, 캐시 관리 정보…
- 표준 헤더가 너무 많음
- 필요시 임의의 헤더 추가 가능
    - helloworld: hihi

### 🌻 1-3. RFC2616(과거)

- 헤더 분류
    - General 헤더 : 메시지 전체에 적용되는 정보
        - 예: Connection: close
    - Request 헤더 : 요청 정보
        - 예: User-Agent: Mozila/5.0
    - Response 헤더 : 응답 정보
        - 예: Server: Apache
    - Entity 헤더 : 엔티티 바디 정보
        - 예: Content-Type: text/html, Content-Length: 3423

### 🌻 1-4. HTTP BODY - RFC2616(과거)

- 메시지 본문(message body)은 엔티티 본문을 전달하는데 사용
- 엔티티 본문은 요청이나 응답에서 전달할 실제 데이터
- 엔티티 헤더는 엔티티 본문의 데이터를 해석할 수 있는 정보 제공
    - 데이터 유형(html, json), 데이터 길이, 압축 정보 등

### 🌻 1-5. RFC723x 변화

- 엔티티(Entity) → 표현(Representation)
- Representation = representation Metadata + Representation Data
- 표현 = 표현 메타데이터 + 표현데이터

### 🌻 1-6. HTTP BODY - RFC7230(최신)

- 메시지 본문(message body)을 통해 표현 데이터 전달
- 메시지 본문 = 페이로드(payload)
- 표현은 요청이나 응답에서 전달할 실제 ㄷ이터
- 표현 헤더는 표현 데이터를 해석할 수 있는 정보 제공
    - 데이터 유형(html, json), 데이터 길이, 압축 정보 등
- 참고: 표현 헤더는 표현 메타데이터와, 페이로드 메시지를 구분해야 한다.

## 🍄 2. 표현

### 🌻 2-1. 표현 종류

- Content-Type: 표현 데이터의 형식
- Content-Enconding: 표현 데이터의 압축 방식
- Content-Language : 표현 데이터의 자연 언어
- Content-Length : 표현 데이터의 길이
- 표현 헤더는 전송, 응답 둘다 사용

### 🌻 2-2. Content-Type

- 표현 데이터의 형식 설명
- 미디어 타입, 문자 인코딩
- 예)
    - text/html; charset=utf-8
    - application/json
    - image/png

### 🌻 2-3. Content-Encoding

- 표현 데이터 인코딩
- 표현 데이터를 압축하기 위해 사용
- 데이터를 전달하는 곳에서 압축 후 인코딩 헤더 추가
- 데이터를 읽는 쪽에서 인코딩 헤더의 정보로 압축 해제
- 예)
    - gzip
    - deflate
    - identity

### 🌻 2-4. Content-Language

- 표현 데이터의 자연 언어
- 표현 데이터의 자연 언어를 표현
- 예)
    - ko
    - en
    - en-US

### 🌻 2-5. Content-Length

- 표현 데이터의 길이
- 바이트 단위
- Transfer-Encoding(전송 코딩)을 사용하면 Content-Length를 사용하면 안됨

## 🍄 3. 콘텐츠 협상

### 🌻 3-1. 협상(콘텐츠 네고시에이션)이란

- 클라이언트가 선호하는 표현 요청
- Accept: 클라이언트가 선호하는 미디어 타입 전달
- Accept-Charset: 클라이언트가 선호하는 문자 인코딩
- Accept-Encoding: 클라이언트가 선호하는 압축 인코딩
- Accept-Language: 클라이언트가 선호하는 자연 언어
- 협상 헤더는 요청시에만 사용한다.

### 🌻 3-2. 협상과 우선순위 1

- Quality Values(q) 값 사용
- 0 ~ 1, 클수록 높은 우선순위
- 생략하면 1
- Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
    1. ko-KR;q=1 (q생략)
    2. ko;q=0.9
    3. en-US;q=0.8
    4. en:q=0.7

```
GET /event
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
```

### 🌻 3-3. 협상과 우선순위2

- 구체적인 것이 우선한다.
- `Accept: text/*, text/plain, text/pplain;format=flowed, */*`
    1. text/plain;format=flowed
    2. text/plain
    3. text/*
    4. */*

```
GET /event
Accept: text/*, text/plain, text/pplain;format=flowed, */*
```

### 🌻 3-4. 협상과 우선순위3

- 구체적인 것을 기준으로 미디어 타입을 맞춘다.
- Accept: text/*;q=0.3, text/html;q=0.7, text/html;level=1, text/html;level=2;q=0.4, */*;q=0.5

| Media Type | Quality |
| --- | --- |
| text/html;level=1 | 1 |
| text/html | 0.7 |
| text/plain | 0.3 |
| image/jpeg | 0.5 |
| text/html;level=2 | 0.4 |
| text/html;level=3 | 0.7 |

## 🍄 4. 전송 방식

- Transfer-Encoding
- Range, Content-Range

### 🌻 4-1. 전송 방식 종류

- 단순 전송(Content-Length)
- 압축 전송(Content-Encoding)
- 분할 전송(Transfer-Encoding)
    - Content-Length를 보내면 안된다. 길이가 예측이 안됨.
- 범위 전송(Range, Content-Range)

## 🍄 5. 일반 정보

### 🌻 5-1. 일반 정보 종류

- From : 유저 에이전트의 이메일 정보
- Referer : 이전 웹 페이지 주소
- User-Agent : 유저 에이전트 애플리케이션 정보
- Server : 요청을 처리하는 오리진 서버의 소프트웨어 정보
- Date : 메시지가 생성된 날짜

### 🌻 5-2. From

- 유저 에이전트의 이메일 정보
- 일반적으로 잘 사용되지 않음
- 검색 엔진 같은 곳에서, 주로 사용
- 요청에서 사용

### 🌻 5-3. Referer

- 이전 웹 페이지 주소
- 현재 요청된 페이지의 이전 웹 페이지 주소
- A → B로 이동하는 경우 B를 요청할 때 Referer: A를 포함해서 요청
- Referer를 사용해서 유입 경로 분석 가능
- 요청에서 사용
- 참고 : referer는 단어 referrer의 오타

### 🌻 5-4. User-Agent

- 유저 에이전트 애플리케이션 정보
- user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/ 537.36 (KHTML, like Gecko) Chrome/86.0.4240.183 Safari/537.36
- 클라이언트의 애플리케이션 정보(웹 브라우저 정보 등)
- 통계 정보
- 어떤 종류의 브라우저에서 장애가 발생하는지 파악 가능
- 요청에서 사용

### 🌻 5-5. Server

- 요청을 처리하는 ORIGIN 서버의 소프트웨어 정보
- Server: Apache/2.2.22 (Debian)
- server: nginx
- 응답에서 사용

### 🌻 5-6. Date

- 메시지가 발생한 날짜와 시간
- Date: Tue, 15 Nov 1994 08:12:31 GMT
- 응답에서 사용

## 🍄 6. 특별한 정보

### 🌻 6-1. 특별한 정보 종류

- Host: 요청한 호스트 정보(도메인)
- Location: 페이지 리다이렉션
- Allow: 허용 가능한 HTTP 메서드
- Retry-After: 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간

### 🌻 6-2. Host

- 요청한 호스트 정보(도메인)
- 요청에서 사용
- 필수
- 하나의 서버가 여러 도메인을 처리해야 할 때 사용
- 하나의 IP 주소에 여러 도메인이 적용되어 있을 때 사용

```
GET /search?q=hello&hl=ko HTTP/1.1
Host: www.google.com
```

### 🌻 6-3. Location

- 페이지 리다이렉션
- 웹 브라우저는 3xx 응답의 결과에 Location 헤더가 있으면, Location 위치로 자동 이동(리다이렉트)
- 응답코드 3xx에서 설명
- 201 (Created): Location 값은 요청에 의해 생성된 리소스 URI
- 3xx (Redirection): Location 값은 요청을 자동으로 리다렉션하기 위한 대상 리소스를 가리킴

### 🌻 6-4. Allow

- 허용 가능한 HTTP 메서드
- 405 (Method Not Allowed) 에서 응답에 포함해야함
- Allow: GET, HEAD, PUT

### 🌻 6-5. Retry-After

- 유저 에이전트가 다음 요청을 하기까지 기다려야 하는 시간
- 503 (Service Unavailable): 서비스가 언제까지 불능인지 알려줄 수 있음
- Retry-After: Fri, 31 Dec 1999 23:59:59 GMT (날짜 표기)
- Retry-After: 120(초단위 표기)

## 🍄 7. 인증

### 🌻 7-1. 인증 종류

- Authorization: 클라이언트 인증 정보를 서버에 전달
- WWW-Authenticate: 리소스 접근 시 필요한 인증 방법 정의
- 인증정보에 따라 들어가는 내용이 들어가는지 다르다(OAuth, JWT 등)

### 🌻 7-2. Authorization

- 클라이언트 인증 정보를 서버에 전달
- Authorization: Basic xxxxxxx

### 🌻 7-3. WWW-Authenticate

- 리소스 접근시 필요한 인증 방법 정의
- 401 Unauthorized 응답과 함께 사용
- WWW-Authenticate: Newauth realm="apps", type=1, title="Login to \"apps\"", Basic realm="simple”

## 🍄 8. 쿠키

### 🌻 8-1. 쿠키의 종류

- Set-Cookie: 서버에서 클라이언트로 쿠키 전달(응답)
- Cookie: 클라이언트가 서버에서 받은 쿠키를 저장하고, HTTP 요청시 서버로 전달

### 🌻 8-2. 쿠키를 사용할 때와 사용하지 않을때

- 쿠키를 사용하지 않을 때는 로그인 이후 로그인 상태가 유지되지 않는다. 서버가 클라이언트가 로그인한지 안한지 확인할 수 있는 방법이 없다.
- 쿠키를 사용한다면 위 문제를 해결할 수 있다.
- HTTP가 무상태(Stateless)프로토콜이기 때문에 쿠키를 사용해야 한다.

### 🌻 8-3. 모든 요청에 정보를 넘기는 문제

- 쿠키를 사용하지 않고 모든 요청에 정보를 넘긴다면 문제가 많다.
- 모든 요청에 사용자 정보가 포함되도록 개발 해야한다.
- 브라우저를 완전히 종료하고 다시 열면? 기억을 하지 못한다.

### 🌻 8-4. 쿠키 사용

- 웹 브라우저에서 서버로 로그인 요청을 보내면 서버는 Set-Cookie를 담음 메시지를 클라이언트에게 전송한다.

```
HTTP/1.1 200 OK
Set-Cookie: user=이재준

이재준님이 로그인했습니다.
```

- 웹 브라우저는 쿠키 저장소에 `user=이재준` 이라는 정보를 저장한다.
- 이후 다시 로그인이 필요한 페이지에 접근할 때 쿠키 저장소에서 조회해서 Cookie 헤더에 담에 메세지를 전달한다.

```
GET /welcome HTTP/1.1
Cookie: user=이재준
```

- 쿠키는 모든 요청에 쿠키 정보를 자동으로 포함한다.

```
GET /welcome HTTP/1.1
Cookie: user=이재준
```

```
GET /board HTTP/1.1
Cookie: user=이재준
```

```
GET /xxx HTTP/1.1
Cookie: user=이재준
```

### 🌻 8-5. 쿠키에 대해서

- 예) set-cookie: sessionId=abcde1234; expires=Sat, 26-Dec-2020 00:00:00 GMT; path=/; domain=.google.com; Secure
- 사용처
    - 사용자 로그인 세션 관리
    - 광고 정보 트래킹
- 쿠키 정보는 항상 서버에 전송됨
    - 네트워크 트래픽 추가 유발
    - 최소한의 정보만 사용(세션 id, 인증 토큰)
    - 서버에 전송하지 않고, 웹 브라우저 내부에 데이터를 저장하고 싶으면 웹 스토리지(localStorage, sessionStorage) 참고
- 주의해야할 점
    - 보안에 민감한 데이터는 저장하면 안된다.(주민번호, 신용카드 번호 등)

### 🌻 8-6. 쿠키 - 생명주기(Expires, max-age)

- Set-Cookie: expires=Sat, 26-Dec-2020 04:39:21 GMT
    - 만료일이 되면 쿠키 삭제
- Set-Cookie: max-age=3600 (3600초)
    - 0이나 음수를 지정하면 쿠키 삭제
- 세션 쿠키 : 만료 날짜를 생략하면 브라우저 종료시 까지만 유지
- 영속 쿠키 : 만료 날짜를 입력하면 해당 날짜까지 유지

### 🌻 8-7. 쿠키 - 도메인

- 쿠키를 아무 사이트에서나 사용하면 문제가 있을 것이다.
- 예) domain=example.org
- 명시: 명시한 문서 기준 도메인 + 서브 도메인 포함
    - domain=example.org를 지정해서 쿠키 생성
        - example.org는 물론이고
        - dev.example.org도 쿠키 접근
- 생략: 현재 문서 기준 도메인만 적용
    - example.org에서 쿠키를 생성하고 domain 지정을 생략
        - example.org 에서만 쿠키 접근
        - dev.example.org는 쿠키 미접근

### 🌻 8-8. 쿠키 - 경로

- 예) path=/home
- 이 경로를 포함한 하위 경로 페이지만 쿠키 접근
- 일반적으로 path=/ 루트로 지정
- 예)
    - path=/home 지정
    - /home → 가능
    - /home/level1 → 가능
    - /home/level1/level2 → 가능
    - /hello → 불가능

### 🌻 8-9. 쿠키 - 보안

- Secure
    - 쿠키는 http, https를 구분하지 않고 전송
    - Secure를 적용하면 https인 경우에만 전송
- HttpOnly
    - XSS 공격 방지
    - 자바스크립트에서 접근 불가(document.cookie)
    - HTTP 전송에만 사용
- SameSite
    - XSRF 공격 방지
    - 요청 도메인과 쿠키에 설정된 도메인이 같은 경우만 쿠키 전송