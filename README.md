# ⛏️ 파닉스 광산 (Phonics Mine)

시윤이랑 엄마 폰으로 같이 하는 파닉스 놀이. 마인크래프트 느낌의 블록 캐기 + 크래프팅으로
낱소리(phonics) → 블렌딩(CVC 단어)까지.

- 서버/설치 없음. `index.html` 한 파일이 앱 전체.
- 소리는 폰 내장 TTS(Web Speech API). `audio/<글자>.mp3`를 넣으면 그 글자는 mp3가 우선.
- 진도는 폰 브라우저(localStorage)에 저장.

## 놀이 구조

| 월드 | 테마 | 소리 (Jolly Phonics 순서) | 예시 단어 |
|---|---|---|---|
| 1 | 땅속 광산 ⛏️ | s a t i p n | sat, pin, tap, ant, pan |
| 2 | 기차역 🚂 | c k e h r m d | cat, hat, red, car, map |
| 3 | 공항 활주로 ✈️ | g o u l f b | bus, sub, dog, sun, cup |
| 4 | 우주 정거장 🚀 | j z w v y x | jet, van, box, fox, six |

- **캐기**: 블록을 3번 두드리면 깨짐. 두드릴 때마다 소리 재생 → 따라 하기. 깨지면 글자 카드(입모양 + 엄마 팁).
- **만들기**: 캔 글자로 단어 조립. 글자를 누르면 소리, 다 채우면 블렌딩(한 소리씩 → 단어). 완성하면 💎.
- **가방**: 캔 글자/만든 단어 다시 듣기.
- 앞 월드의 블록을 다 캐면 다음 월드 열림.
- **엄마 화면**: 진도, 음성 선택/속도, 초기화.

## 폰에서 열기

### 방법 A — GitHub Pages (추천, 링크 하나로 끝)
1. 이 폴더를 GitHub 저장소(public)로 푸시.
2. 저장소 Settings → Pages → Branch: `main` / root → Save.
3. `https://<계정>.github.io/<저장소>/` 를 폰 Chrome으로 열기 → 메뉴(⋮) → **홈 화면에 추가**.
   - https라서 오프라인 캐시(sw.js)도 동작.

### 방법 B — 파일 직접 복사
`index.html`, `manifest.json`, `icon-*.png`를 폰에 복사하고 Chrome에서 `file://` 로 열기.
(TTS는 되지만 홈 화면 추가/오프라인 캐시는 제한적.)

## 안드로이드 TTS 품질 올리기
설정 → 일반(또는 접근성) → 텍스트 음성 변환 → Google 음성 서비스 → 영어(미국) 음성 데이터 다운로드.
앱의 **엄마 화면**에서 음성을 고를 수 있음.

## 커스터마이즈
`index.html` 상단 `SOUNDS` / `WORLDS` 객체만 고치면 됨.
- 글자 추가: `SOUNDS`에 `{ipa, tts, kw, em, ko, mouth, tip}`.
- 단어 추가: 해당 월드 `words`에 `['단어','뜻','이모지']`. (그 시점까지 배운 글자만 쓰기)
- 이름 변경: `load()`의 `name:'NiceSiyun'`.

## 파일
```
index.html     앱 본체 (HTML/CSS/JS 단일 파일)
manifest.json  홈 화면 추가용
sw.js          오프라인 캐시 (https에서만)
icon-192.png / icon-512.png
audio/         (선택) 낱소리 mp3 — s.mp3, a.mp3 ... 넣으면 TTS 대신 재생
```

## 다음 단계 아이디어
- 미니게임: 소리 듣고 맞는 블록 찾기 (수용 → 산출 순서)
- 월드 5+: 이중자(ai, ee, sh, ch, th...)
- 엄마 목소리 녹음 기능 (MediaRecorder → audio/)
- 진도 리포트: 자주 틀리는 소리
