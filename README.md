# 예찬 ♥ 현주 모바일 청첩장

정적 웹사이트(HTML/CSS/JS)라서 GitHub Pages에 그대로 올리면 됩니다. 빌드 과정은 없습니다.

```
index.html        페이지 구조
style.css         디자인
app.js            동작 (인트로, 메뉴, 달력, 카운트다운, 갤러리, 폼 등)
config.js         ★ 내용 설정 (이름, 날짜, 계좌, 시트 주소)
images/full       크게 보기용 사진 (긴 변 1600px)
images/thumb      원형 갤러리용 정사각 사진
images/og.jpg     카톡 등 링크 미리보기 이미지
apps-script/Code.gs  구글 시트 연동 코드
```

## 1. 먼저 고칠 것 (config.js)

- `date` — **예식 일시** (지금은 임시값). 예: `"2027-03-20T12:30:00+09:00"`
- `venue.hall`, `venue.tel` — 홀 이름, 예식장 전화번호
- `accounts` — 계좌 정보
- `showFlowerNotice` — 화환을 받지 않는 예식장이면 `true`
- `greeting` — 인사말 문구

달력, 카운트다운, 팝업 문구 등은 전부 이 값으로 자동 생성됩니다.

## 2. 구글 시트 연결 (참석 여부 수집)

1. 구글 드라이브에서 새 **구글 스프레드시트** 만들기
2. 메뉴 **확장 프로그램 → Apps Script**
3. 기본 코드를 지우고 `apps-script/Code.gs` 내용을 붙여넣은 뒤 저장
4. 오른쪽 위 **배포 → 새 배포** → 톱니바퀴에서 **웹 앱** 선택
   - 실행 사용자: **나**
   - 액세스 권한이 있는 사용자: **모든 사용자**
5. **배포** → 권한 승인 (“고급 → 안전하지 않은 페이지로 이동”을 눌러 진행)
6. 나온 **웹 앱 URL**(`https://script.google.com/macros/s/.../exec`)을 복사해서
   `config.js`의 `rsvpEndpoint: ""` 따옴표 안에 붙여넣기

이후 응답이 오면 시트의 `참석여부` 탭에 한 줄씩 쌓입니다.
코드를 수정했다면 **배포 → 배포 관리 → 수정 → 새 버전**으로 다시 배포해야 반영됩니다.

## 3. GitHub Pages에 올리기

1. GitHub에서 새 저장소 생성 (예: `wedding`, Public)
2. 이 폴더의 파일을 전부 업로드 (**Add file → Upload files**에 폴더 내용 통째로 끌어다 놓기)
3. 저장소 **Settings → Pages** → Source: `Deploy from a branch`, Branch: `main` / `(root)` → Save
4. 1~2분 뒤 `https://<아이디>.github.io/wedding/` 주소로 접속

### 카카오톡 미리보기 이미지
링크 미리보기는 절대 주소가 필요합니다. 배포 후 `index.html`의
`<meta property="og:image" content="images/og.jpg">`를
`https://<아이디>.github.io/wedding/images/og.jpg`로 바꿔주세요.
(이미 공유해서 예전 미리보기가 남아 있다면 카카오 개발자 사이트의 “공유 디버거”에서 캐시를 초기화하면 됩니다.)

## 사진 바꾸기
`images/full/01.jpg`~`12.jpg`(원본)와 `images/thumb/`(정사각형)을 같은 이름으로 교체하세요.
01번이 커버 사진입니다. 장수를 바꾸면 `config.js`의 `photos` 개수(`length: 12`)도 바꿔주세요.
