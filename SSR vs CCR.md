# 렌더링 (rendering)
어떠한 웹 페이지 접속시 그 페이지를 화면에 그려주는 것

# SSR (Server Side Rendering)
요청시마다 새로고침이 일어나고 서버에 새로운 페이지의 대해 요청하는 방식 <br>
![This is an image](https://goodgid.github.io/assets/img/posts/ssr_and_csr_1.png)

# CSR (Client Side Rendering) & SPA (Single Page Application)
CSR / SPA는 최초 한 번 페이지 전체를 로딩한 후 데이터만 변경하여 사용할 수 있는 애플리케이션을 의미 <br>
![This is an image](https://goodgid.github.io/assets/img/posts/ssr_and_csr_2.png)

# CSR vs SSR
![This is an image](https://goodgid.github.io/assets/img/posts/ssr_and_csr_3.png)

|구분|CSR|SSR|
|---|---|---|
|장점|1. 서버에 대한 HTTP 요청이 적다.|1. 웹 사이트 초기페이지 로드는 렌더링할 코드가 적기 때문에 빠름<br> 2. 정적 사이트에 적합 |
|단점|1. 초기 페이지로드 느림 <br> 2. 서버에서 수행해야 할 추가 단계가 있음 <br> 3. 대부분 외부 라이브러리가 필요.|1. 사이트 상호작용이 적음 <br> 2. 느린 페이지 렌더링 <br> 3. 전체 UI가 재로드됨<br>4. 빈번한 서버 요청|

## SSR 사용할 때
1. 네트워크가 느릴 때 (SSR은 각 페이지마다 나눠불러오기 때문)
2. SEO(검색 엔진 최적화)가 필요할 때
3. 최초 로딩이 빨라야하는 사이트를 개발 할 때
4. 웹 사이트가 상호작용이 별로 없을 때

## CSR 사용할 때
1. 네트워크가 빠를 때
2. 서버의 성능이 좋지 않을 때
3. 사용자에게 보여줘야하는 데이터의 양이 많을 때
4. 메인 스크립트가 가벼울 때
5. SEO가 필요 없을 때
6. 웹 app에서 사용자와 상호작용할 것들이 많을 때