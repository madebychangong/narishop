# 나리상점 업로드 안내

봄빛 나리꽃 느낌의 디아블로4 시세표 + 주문서입니다.
기능은 루피상점과 같고(가격표 편집, 카톡방 주소 저장, 주문서 담기, 주문 내용 복사), 디자인과 화면 배치만 다릅니다.

이 폴더 안의 파일을 GitHub 저장소 최상단에 올리면 됩니다. 폴더째 넣지 말고 `index.html`, `functions` 폴더, `logo.svg`, `README.md`가 바로 보이게 올리세요.

## 파일

- `index.html`: 손님 화면 + 숨김 관리자 편집 (디자인·문구 전부 이 파일 안)
- `logo.svg`: 나리꽃 로고 (직접 그린 그림이라 저작권 걱정 없음)
- `가격표.txt`: 처음 넣어둔 가격표 원본. 실제로 쓰이는 기본값은 `index.html` 안의 `rawPriceText`
- `functions/`: Cloudflare Pages Functions (로그인, 가격표 저장/불러오기)

배경 사진은 쓰지 않습니다. 화면 바탕은 연분홍·연둣빛 그라데이션으로만 되어 있어 가볍고 빠릅니다.

## Cloudflare Pages 설정

- Framework preset: `None`
- Build command: `exit 0`
- Build output directory: `/`
- Root directory: 비워두기

## 관리자 기능 설정

Cloudflare Pages 프로젝트에서 아래를 넣어야 저장이 동작합니다. **넣은 뒤 반드시 다시 배포(Retry deployment)** 해야 적용됩니다.

1. Settings > Variables and Secrets
   - `ADMIN_PASSWORD`: 관리자 비밀번호 (길고 특이하게)
   - `SESSION_SECRET`: 길고 랜덤한 문자열

2. Settings > Bindings
   - KV namespace binding
   - Variable name: `NARI_KV`
   - KV namespace: 나리상점용으로 새로 만든 KV

`NARI_KV`가 없으면 화면은 정상이지만 저장한 가격표가 손님에게 반영되지 않습니다.

## 관리자 열기

- 꽃 로고나 `나리상점` 글자를 1.5초 길게 누르기
- 또는 키보드 `Ctrl + Alt + A`
- 또는 주소 뒤에 `?admin=1`

관리자 화면에서 가격표 원문과 카톡방 주소를 저장할 수 있습니다.
카톡방 주소를 비워두면 "카톡으로 문의" 단추는 화면에서 숨겨집니다.

## 가격표 쓰는 법

```
＊＊＊＊＊＊＊＊＊＊＊＊＊＊＊

🌸골드🌸
-- 1000억 = 2,000원
-- 3000억 = 6,000원

＊＊＊＊＊＊＊＊＊＊＊＊＊＊＊
```

- `＊＊＊` 같은 구분선으로 품목 묶음을 나눕니다
- 이모지로 감싼 줄(`🌸골드🌸`)은 **제목**이 됩니다
- `-- 이름 = 값` 줄은 **품목**이 됩니다
- 맨 위 구분선 앞/첫 묶음에 값 없이 글만 쓰면 **상단 안내 카드**가 됩니다
- 값 뒤에 괄호 설명을 붙이면(`= 60,000원 (설명)`) 설명은 품목 이름 쪽으로 옮겨집니다

## 관리자 기능이 안 열릴 때

비밀번호를 넣어도 "비밀번호가 다릅니다"만 나오면 대부분 Cloudflare 설정이 빠진 경우입니다.
손님에게 내부 사정을 알리지 않으려고 화면에는 항상 같은 문구만 보여줍니다.

1. `ADMIN_PASSWORD`, `SESSION_SECRET`이 둘 다 들어있는지
2. 넣은 뒤 **다시 배포**했는지
3. KV 이름이 정확히 `NARI_KV`인지 (저장이 안 될 때)
