# 🎯 Chapter 2: URI와 웹 브라우저 요청 흐름

## 🍄 1. URI

- URI(Uniform Resource Identifier)
- URI, URL, URN을 들어봤을텐데 이것들의 차이는 무엇일까?
- URI는 **로케이터**(locator), **이름**(name) 또는 둘다 추가로 분류될 수 있다.
- URI는 가장 큰 개념이다. URL(Resource Locator)와 URN(Resource Name)을 포함한 개념이다.
- URL과 URN은 어떻게 생겼을까?
    - URL : foo://example.com:8042/over/there?name=ferret#nose
    - URN : urn:example:animal:ferret:nose
- 거의 URL만 사용한다. URN은 사용하지 않는다.

### 🌻 1-1. URI 단어의 뜻

- Uniform : 리소스 식별하는 통일된 방식
- Resource : 자원, URI로 식별할 수 있는 모든 것(제한 없음)
- Identifier : 다른 항목과 구분하는데 필요한 정보

### 🌻 1-2. URL, URN 단어의 뜻

- URL - Locator : 리소스가 있는 위치를 지정
- URN - Name : 리소스에 이름을 부여
- 위치는 변할 수 있지만, 이름은 변하지 않는다.
- URN 이름만으로 실제 리소스를 찾을 수 있는 방법이 보편화 되지 않았다.
- URI가 URL을 포함하기 때문에 같은 의미이다. URI로 통일하여 부르자.

### 🌻 1-3. URL 문법

- **scheme://[userinfo@]host[:port][/path][?query][#fragment]** 형식으로 되어 있다.
- URL 해석
    - 주소 : https://www.google.com/search?q=hello&hl=ko
    - 프로토콜 : https
    - 호스트명 : www.google.com
    - 포트번호 : 443
    - 패스 : /search
    - 쿼리 파라미터 : q=hello&hl=ko

### 🌻 1-4. URL scheme

- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    - 예) http, https, ftp 등
- http는 80포트, https는 443 포트를 주로 사용, 포트는 생략 가능하다.
- https는 http에 보안을 추가한 것이다.(HTTP Secure)

### 🌻 1-5. URL userinfo

- URL에 사용자정보를 포함해서 인증
- 거의 사용하지 않는다.

### 🌻 1-6. URL host

- 호스트명
- 도메인명 또는 IP 주소를 직접 사용 가능하다.

### 🌻 1-7. URL port

- 포트(PORT)
- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443

### 🌻 1-8. URL path

- 리소스 경로(path), 계층적 구조
- 예)
    - /home/file1.jpg
    - /members
    - /members/100, /items/iphone12

### 🌻 1-9. URL query

- key=value 형태로 사용한다.
- `?` 로 시작, `&` 로 추가 가능하다.
    - 예) ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불린다.
- 웹 서버에 제공하는 파라미터, 문자 형태이다.

### 🌻 1-10. URL fragment

- html 내부 북마크 등에 사용한다.
- 서버에 전송하는 정보는 아니다.
- 예) #getting-started-introducing-spring-boot

## 🍄 2. 웹 브라우저 요청 흐름

- [https://www.google.com/search?q=hello&hl=ko](https://www.google.com/search?q=hello&hl=ko) 에 접속하면 어떻게 될까?
1. 먼저 DNS 서버에 [www.google.com](http://www.google.com) 이라는 것을 조회하고 해당 도메인 주소의 해당하는 IP 주소를 받아온다.
2. 웹 브라우저는 HTTP 요청 메시지를 생성한다.

```json
GET /search?q=hello&hl=ko HTTP/1.1
HOST: www.google.com
```

1. HTTP 메시지를 전송한다.
    - 웹 브라우저가 HTTP 메시지를 생성한다.
    - SOCKET 라이브러리를 통해 전달한다.
    - HTTP 메시지가 포함된 TCP/IP 패킷을 생성한다.
    - 웹 브라우저느 요청 패킷을 전달한다.
    - 구글 서버에서 HTTP 응답 메시지를 만든다.
2. 구글 서버는 요청 패킷중 TCP/IP 패킷을 까서 버리고, HTTP 메시지를 꺼낸다. 이 메시지를 가지고 해석을 하고 데이터를 찾는다.
3. 구글 서버에서 HTTP 응답 메시지를 만든다.

```json
HTTP/1.1 200 OK
Content-Type: text/html;charset=UTF-8
Content-Length: 3423

<html>
	<body>...</body>
</html>
```

1. 구글 서버는 응답 패킷을 전달한다.
2. 웹 브라우저는 구글 서버로부터 받은 응답 패킷 까서 웹 브라우저에 HTML 렌더링을 한다.