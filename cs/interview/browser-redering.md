# ๐ฏ ๋ธ๋ผ์ฐ์  ๋ ๋๋ง ๊ณผ์ (Critical Rendering Path)

์ฐ๋ฆฌ๊ฐ ์ฃผ์์ฐฝ์ url๋ฅผ ์๋ ฅํ๊ณ , ๋ธ๋ผ์ฐ์ ๋ ํด๋น ์๋ฒ๋ก ์์ฒญ์ ๋ณด๋ด๊ณ  ์๋ฒ๋ ์๋ต์ผ๋ก HTML ๋ฐ์ดํฐ๋ฅผ ๋ด๋ ค์ฃผ๋๋ฐ, ์ด HTML ๋ฐ์ดํฐ๋ฅผ ์ค์  ์ฐ๋ฆฌ๊ฐ ๋ณด์ด๋ ํ๋ฉด์ผ๋ก ๊ทธ๋ฆฌ๊น์ง ๋จ๊ณ๋ฅผ `critical rendering path` ๋ผ๊ณ  ๋ถ๋ฅธ๋ค.

1. ๋ธ๋ผ์ฐ์ ๋ ์๋ฒ์์ ์๋ต์ ๋ฐ์ HTML ๋ฐ์ดํฐ๋ฅผ ํ์ฑํ๋ค. ํ์คํธ๋ก ์ด๋ฃจ์ด์ง ์ด ํ์ผ์ ํ์ฑํ๋ฉด์ `DOM Tree` ๋ฅผ ๋ง๋ค์ด ๋๊ฐ๋ค.
2. ํ์ฑํ๋ ์ค CSSํ์ผ ๋งํฌ๋ฅผ ๋ง๋๋ฉด CSS ํ์ผ์ ์์ฒญํด์ ๋ฐ์์ค๊ณ  CSS๋ฅผ ํ์ฑํด `CSSOM` ์ ๋ง๋ ๋ค.
3. CSS ํ์ฑ์ด ์ข๋ฃ๋๋ฉด ์ ์ ์ค๋จ๋์๋ html์ ๋ค์ ์ฝ๊ณ  DOM Tree๋ฅผ ๋ง๋ค์ด๋๊ฐ๋ค JavaScript ํ์ผ์ ๋ง๋๋ฉด ํด๋น ํ์ผ์ ๋ฐ์์ค๊ณ  ์คํํ  ๋๊น์ง ํ์ฑ์ ๋ฉ์ถ๋ค. ์ด๋ ์ ์ด ๊ถํ์ JavaScript engine์ ๋๊ธฐ๊ณ  JavaScript์ฝ๋ ๋๋ ํ์ผ์ ๋ก๋ํด์ ํ์ฑํ๊ณ  ์คํํ๋ค.
4. HTML ํ์ฑํ ๊ฒฐ๊ณผ๋ก `DOM Tree`๋ฅผ ์์ฑ์ํจ๋ค.
5. `DOM Tree`์ `CSSOM`์ด ๋ชจ๋ ๋ง๋ค์ด์ง๋ฉด ์ด ๋์ ์ฌ์ฉํด `Render Tree`๋ฅผ ๋ง๋ ๋ค. ์ด`Render Tree`๋ ์ค์ ๋ก ๋์ ๋ณด์ด๋ ๊ฒ๋ค๋ก ์ด๋ฃจ์ด์ง๋ค.
6. `Render Tree`์ ์๋ ๊ฐ๊ฐ์ ๋ธ๋๋ค์ด ํ๋ฉด์ ์ด๋์ ์ด๋ป๊ฒ ์์นํ  ๊ฒ์ธ๊ฐ๋ฅผ ๊ณ์ฐํ๋ Layout ๊ณผ์ ์ ๊ฑฐ์น๋๋๋ฐ ๋ง์ฝ ๋ธ๋ผ์ฐ์  ์ฐฝ์ด ๋ณ๊ฒฝ๋๋ฉด `Render Tree`๋ฅผ ๋ง๋๋ ๊ณผ์ ์ ์๋ต๋๊ณ , Layout์ด ์ผ์ด๋๊ฒ ๋๋ค.
7. `Render Tree` ๊ฐ ๋ธ๋๋ค์ ์ค์ ๋ก ํ๋ฉด์ ๊ทธ๋ฆฌ๊ฒ ๋๋ Paint ๊ณผ์ ์ ๊ฑฐ์น๋ค.