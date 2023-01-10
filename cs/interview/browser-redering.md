# 🎯 브라우저 렌더링 과정(Critical Rendering Path)

우리가 주소창에 url를 입력하고, 브라우저는 해당 서버로 요청을 보내고 서버는 응답으로 HTML 데이터를 내려주는데, 이 HTML 데이터를 실제 우리가 보이는 화면으로 그리까지 단계를 `critical rendering path` 라고 부른다.

1. 브라우저는 서버에서 응답을 받은 HTML 데이터를 파싱한다. 텍스트로 이루어진 이 파일을 파싱하면서 `DOM Tree` 를 만들어 나간다.
2. 파싱하는 중 CSS파일 링크를 만나면 CSS 파일을 요청해서 받아오고 CSS를 파싱해 `CSSOM` 을 만든다.
3. CSS 파싱이 종료되면 잠시 중단되었던 html을 다시 읽고 DOM Tree를 만들어나가다 JavaScript 파일을 만나면 해당 파일을 받아오고 실행할 때까지 파싱을 멈춘다. 이때 제어 권한을 JavaScript engine에 넘기고 JavaScript코드 또는 파일을 로드해서 파싱하고 실행한다.
4. HTML 파싱한 결과로 `DOM Tree`를 완성시킨다.
5. `DOM Tree`와 `CSSOM`이 모두 만들어지면 이 둘을 사용해 `Render Tree`를 만든다. 이`Render Tree`는 실제로 눈에 보이는 것들로 이루어진다.
6. `Render Tree`에 있는 각각의 노드들이 화면의 어디에 어떻게 위치할 것인가를 계산하는 Layout 과정을 거치니는데 만약 브라우저 창이 변경되면 `Render Tree`를 만드는 과정은 생략되고, Layout이 일어나게 된다.
7. `Render Tree` 각 노드들을 실제로 화면에 그리게 되는 Paint 과정을 거친다.