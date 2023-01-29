# 🎯 ‘www.google.com’을 주소창에서 입력하면 일어나는 일

💡 [참고링크](https://velog.io/@eassy/www.google.com%EC%9D%84-%EC%A3%BC%EC%86%8C%EC%B0%BD%EC%97%90%EC%84%9C-%EC%9E%85%EB%A0%A5%ED%95%98%EB%A9%B4-%EC%9D%BC%EC%96%B4%EB%82%98%EB%8A%94-%EC%9D%BC)

### 1. 사용자가 웹 브라우저 검색창에 `www.google.com` 을 입력한다.

### 2. 웹 브라우저는 DNS 캐시 탐색을 통해 해당 도메인 주소와 대응하는 IP주소를 확인한다.

- 캐싱된 기록이 없을 경우 다음단계로 넘어간다.

### 3. 웹 브라우저가 HTTP를 사용하여 DNS에게 입력된 도메인 주소를 요청한다.

### 4. DNS가 웹브라우저에게 찾은 사이트의 IP주소를 응답한다.

- ISP(Internet Service Provider)의 DNS서버가 호스팅하고 있는 서버의 IP주소를 찾기 위해 DNS query를 날린다.
- DNS query : DNS 서버들을 검색해서 해당 사이트의 IP 주소를 찾는데 사용한다. IP 주소를 찾을 때까지 DNS서버에서 다른 DNS서버를 오가며 반복적으로 검색한다.

### 6. 웹브라우저와 서버가 TCP 연결을 한다.

- TCP 3 way handshake

### 7. 웹브라우저가 웹서버에 HTTP 요청을 한다.

- TCP로 연결이 되면, 브라우저는 HTTP 프로토콜로 `GET` 요청을 통해 서버에게 `www.google.com` 의 웹페이지 데이터를 요구한다.

### 6. 서버가 request를 처리하고 response를 생성한다.

- 웹브라우저로부터 request를 받아 처리한다. 그리고 response를 생성해 응답한다.
- request에서는 http 요청을 통해 받아온 다양한 헤더 정보와 데이터들로 요청을 처리하고 response를 생성한다. 이때 response는 특정한 포멧(JSON, HTML, XML 등)으로 작성한다.

### 8. 서버가 HTTP response를 보낸다.

- 서버의 response에는 HTTP 프로토콜에 따른 헤더 정보와 데이터들을 보낸다. 이때 html 데이터를 포함해서 포내며 status code를 사용하여 response 상태를 표현한다.

### 9. 웹브라우저는 HTML content를 보여준다.

- 브라우저가 렌더링과정을 거치게 된다.