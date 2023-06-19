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
  * 구글 OAuth2 등록 https://www.joinc.co.kr/w/man/12/oAuth2/Google
  * Oracle APEX에서 적용 https://doyensys.com/blogs/apex-login-using-google-social-sign-in/

- 구글 OAuth 생성 관련 시행착오
  * 구글 OAuth 생성시 "승인된 자바스크립트 출처" 부분의 URI는 생략해야함
  * 구글 OAuth 생성시 승인된 리디렉션 URI에 "https://apexea.oracle.com/pls/apex/apex_authentication.callback" 가 아니라 apexea 대신 apex로 작성했더니 오류 해결됨

<h3>23.06.09.</h3>

- 앱 이름 변경: IMYMEMINE이라는 쇼핑몰 발견하여 i'Mmmn(아임ㅁㅁ)으로 변경, ㅁㅁ까지 상호명 가능한지 찾아볼 것
- 로고 제작
- 오류 발견: 구글 OAuth 생성 후 credential 생성하고 social login에는 성공하였으나 이때 로그인 페이지로 연동해두면 앱 실행하자마자 구글 로그인 페이지로 리디렉션되기 때문에 로그인 화면에서 구글 로그인용 버튼을 하나 두고 페이지 하나 추가하여 추가된 페이지로 구글 로그인 리디렉션되도록 방법 모색

<h3>23.06.12.</h3>

- 오류 발견: 로그아웃이 안됨. 로그인 리디렉션 오류 해결을 위해서 수정 중에 로그인/로그아웃 관련 앱 세팅이 깨진 것으로 추측 
  * 로그아웃을 할 때, 구글 로그아웃이 되도록 하면 안됨. 브라우저 자체의 구글이 로그아웃되어버림. 모바일 앱으로 개발 예정이기 때문에 로그인 세션 유지는 최대한 오래되어야 함. 자동 로그아웃을 빈번하게 의도할 필요없다고 판단


<h3>23.06.13.</h3>

- 로그아웃 해결: APP > Shared Components > Authentication Schemes > Post-Logout URL 부분이 Home Page와 URL을 수정하다보니 깨진 것 같다는 추측으로 URL 선택 후 로그인 페이지(f?p=&APP_ID.:9999) URL을 입력하여 해결
- 앱 시작하자마자 구글 로그인 뜨는 이슈는 앱 시작 URL을 로그인 화면으로 변경하는 것으로 해결 예정(방법 찾는 중)
- Google 계정으로 계속하기 버튼에 Dynamic Action 추가. 캐시로 아이디, 비밀번호 입력되어있는 내용으로 로그인이 되어, 해당 아이템 값이 있는 경우 clear 후 submit page 되도록 처리.

<h3>23.06.14.</h3>

- 구글 로그인 계정으로 영화 데이터 추가시 I_MOVIE 테이블에는 정상적으로 데이터가 들어가며, USER_ID에는 구글 계정의 name이 들어가는 것 확인
- 대신 구글 로그인 계정은 I_USER 테이블에 데이터가 없음 -> I_USER 테이블에 데이터가 없는 로그인 정보로 메인화면 접근시 I_USER에 회원가입 정보를 트리거로 넣을지, 구글 계정의 회원가입 정보를 따로 연동할 수 있는지 확인 후 더 이슈없을 방법으로 선택할 예정
  * 유저 데이터이기 때문에 안정성부터 고려할 것
  * 트리거로 선택하면 I_USER 테이블에 구글 계정 여부에 대한 컬럼 추가할 것

<h3>23.06.15.</h3>

- 영화 관련 오픈 API 발견 https://www.kobis.or.kr/kobisopenapi/homepg/apiservice/searchServiceInfo.do
- 영화 페이지에 들어갔을 때, 모바일 특성상 심플해야할 것 같아서 보여주는 컬럼 변경(축소)
- 테이블 변경사항(I_MOVIE)
  * 컬럼 변경 CINEMA -> PLACE
  * 컬럼 NOTE 추가
  * 테이블 수정에 따른 UI 및 Query 변경

- 영화 추가 팝업 Drawer에서 Wizard Modal Dialog로 변경
- 팝업 내 입력창들 길이 줄여서 스크롤 생기지 않고 한 눈에 모두 들어올 수 있도록 변경할 것
- 영화본 장소 select list로 추가하도록 변경. CGV 등 선택시 아이콘으로 보여지도록 할 예정

<h3>23.06.16.</h3>

- 로그인 방식을 ver1.0.0에서는 회원가입만 두는게 관리, 테스트에 용이할 것으로 판단. 로그인 방식 수정하고 유저 테이블 데이터로 회원가입 관리 가능하도록 수정할 것
- CSS 추가: 푸터의 release 1.0.0 diplay none 처리.
 * css 파일명을 변경하여 적용 다시 해야함.

<h3>23.06.17.</h3>

- 앱에서 사용 중인 css 파일 주소 변경 완료
- 로그인 credential 변경(구글 -> DB)
- 구글 로그인 버튼 안 보이게 변경

<h3>23.06.18.</h3>

- 계정이 막히는 현상을 계속 해결하지 못해서 결국 챗GPT와 대화까지 했는데, 권한 문제라는 심증이 생김. Oracle APEX의 워크스페이스 하나만 발급받는 것이 아니라 DBA 권한이 있는, DB부터 발급받아야 할 것 같아서 시도 중.
 * OCI 계정 생성 https://team-okitoki.github.io/getting-started/free-oci-promotions/#%EC%98%A4%EB%9D%BC%ED%81%B4-%ED%81%B4%EB%9D%BC%EC%9A%B0%EB%93%9C%EC%97%90-%EC%82%AC%EC%9D%B8%EC%9D%B8-%ED%95%98%EA%B8%B0
