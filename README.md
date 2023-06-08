<h1>개발일지</h1>

<h3>23.06.04.</h3>

- 사이드 프로젝트 "iMymeMine" 시작
- 테이블 구성(유저, 영화 데이터 테이블)
- 유저 데이터 추가시 트리거 개발
- 앱 추가
- 페이지 추가

<h3>23.06.05.</h3>

- 영화 데이터 추가시 트리거 개발
- admin, test 계정 생성 및 각 테스트 완료
- 기본 기능 구현 완료
- 현재 Oracle account 로그인 설정, 추후 USER 테이블과 연동되도록 변경 필요

<h3>23.06.06.</h3>

- 모바일 브라우저로 테스트시 별점 터치 이슈 발견, 우선 사이즈 키워보고 추후 이슈 재확인할 것

<h3>23.06.07.</h3>

- 회원가입 페이지 생성 및 개발
- 로그인 페이지에 회원가입 바로가기 버튼 추가
- USER 테이블 컬럼 추가(이름, 생년월일, 성별)

<h3>23.06.08.</h3>

- css 적용 방식 변경: 내부 스타일시트(APEX Custom Css) -> 외부 스타일시트(Static Application Files내 파일 하나로 통합 관리)
- 구글 로그인 추가
  > 구글 OAuth2 등록 https://www.joinc.co.kr/w/man/12/oAuth2/Google
  > 
  > Oracle APEX에서 적용 https://doyensys.com/blogs/apex-login-using-google-social-sign-in/

- 구글 OAuth 생성 관련 시행착오
  > 구글 OAuth 생성시 "승인된 자바스크립트 출처" 부분의 URI는 생략해야함
  > 
  > 구글 OAuth 생성시 승인된 리디렉션 URI에 "https://apexea.oracle.com/pls/apex/apex_authentication.callback" 가 아니라 apexea 대신 apex로 작성했더니 오류 해결됨

- 구글 OAuth 생성 후 credential 생성하고 social login에는 성공하였으나 이때 로그인 페이지로 연동해두면 앱 실행하자마자 구글 로그인 페이지로 리디렉션되기 때문에 로그인 화면에서 구글 로그인용 버튼을 하나 두고 페이지 하나 추가하여 추가된 페이지로 구글 로그인 리디렉션되도록 변경함
