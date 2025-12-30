# 🚀 GitHub Pages 설정 가이드

## 📋 준비물
- GitHub 계정
- 생성된 웹사이트 파일들 (index.html, privacy.html, support.html, style.css, CNAME)
- cctv.musi.co.kr 서브도메인 설정 권한

---

## 1️⃣ GitHub 레포지토리 생성

### Step 1: GitHub에 로그인
- https://github.com 접속
- 로그인

### Step 2: 새 레포지토리 생성
```
1. 오른쪽 상단 '+' 버튼 클릭
2. 'New repository' 선택
```

### Step 3: 레포지토리 설정
```
Repository name: cctvApp
Description: CCTV Viewer - App landing page and documentation
Visibility: Public (GitHub Pages는 Public 필수)
```

**중요:**
- ✅ **Public**으로 설정 (Private는 유료 계정 필요)
- ✅ "Add a README file" 체크 **안 함** (파일 직접 업로드)
- ✅ .gitignore와 license는 선택사항

### Step 4: Create repository 버튼 클릭

---

## 2️⃣ 파일 업로드

### 방법 A: 웹 인터페이스로 업로드 (권장)

#### Step 1: 파일 추가
```
1. 생성된 레포지토리 페이지에서 'uploading an existing file' 링크 클릭
   또는 'Add file' → 'Upload files' 클릭
```

#### Step 2: 파일 선택
다음 파일들을 모두 선택하여 드래그 앤 드롭:
```
index.html
privacy.html
support.html
style.css
CNAME
```

#### Step 3: Commit
```
Commit message: "Initial website setup"
Commit changes 버튼 클릭
```

### 방법 B: Git CLI로 업로드

```bash
# 1. 레포지토리 클론
git clone https://github.com/[your-username]/cctvApp.git
cd cctvApp

# 2. 파일 복사
# 생성된 파일들을 cctvApp 디렉토리로 복사

# 3. Git 추가 및 커밋
git add .
git commit -m "Initial website setup"
git push origin main
```

---

## 3️⃣ GitHub Pages 활성화

### Step 1: Settings로 이동
```
레포지토리 페이지 → Settings 탭 클릭
```

### Step 2: Pages 설정 찾기
```
왼쪽 사이드바 → Pages 클릭
```

### Step 3: Source 설정
```
Source: Deploy from a branch
Branch: main (또는 master)
Folder: / (root)
Save 버튼 클릭
```

### Step 4: 배포 확인
```
1-2분 후 페이지 새로고침
상단에 배포 완료 메시지 표시:
"Your site is live at https://[username].github.io/cctvApp/"
```

---

## 4️⃣ 커스텀 도메인 설정

### Step 1: Custom domain 입력
```
Settings → Pages → Custom domain 섹션
입력: cctv.musi.co.kr
Save 버튼 클릭
```

### Step 2: DNS 체크 대기
```
GitHub가 자동으로 DNS 설정 확인
"DNS check in progress..." 메시지 표시
```

**주의:**
- DNS 설정이 완료되어야 체크 성공
- DNS 전파까지 최대 24-48시간 소요 (보통 1-2시간)

### Step 3: HTTPS 강제 활성화 (DNS 체크 성공 후)
```
☑ Enforce HTTPS 체크박스 활성화
```

**중요:**
- DNS 체크가 완료되어야 이 옵션 활성화 가능
- 활성화하면 자동으로 Let's Encrypt SSL 인증서 발급

---

## 5️⃣ DNS 설정 (별도 진행)

GitHub Pages 설정과 별도로 도메인의 DNS 설정 필요

### 필요한 DNS 레코드:

#### CNAME 레코드 추가
```
Type: CNAME
Name: cctv (또는 cctv.musi.co.kr)
Value: [your-username].github.io
TTL: 3600 (1시간) 또는 기본값
```

**예시:**
```
CNAME  cctv  yourusername.github.io.
```

**주의:**
- Value 끝에 `.` (점) 포함할 것 (일부 DNS 제공자)
- 정확한 GitHub username 사용

---

## 6️⃣ 배포 확인

### Step 1: Actions 탭 확인
```
레포지토리 → Actions 탭
pages build and deployment 워크플로우 확인
초록색 체크마크: 배포 성공
```

### Step 2: 웹사이트 접속 테스트
```
https://cctv.musi.co.kr
```

**테스트 항목:**
- [ ] 메인 페이지 로딩
- [ ] 개인정보처리방침 페이지 작동
- [ ] 지원 페이지 작동
- [ ] CSS 스타일 적용 확인
- [ ] 링크들이 정상 작동
- [ ] HTTPS 자물쇠 아이콘 표시

---

## 🔧 문제 해결

### ❌ "DNS check failed"
**원인:** DNS 설정이 완료되지 않음

**해결:**
1. DNS 설정 확인 (CNAME 레코드)
2. DNS 전파 대기 (최대 24-48시간)
3. DNS 전파 확인: https://dnschecker.org
4. 캐시 삭제 후 재시도

### ❌ 404 Not Found
**원인:** 파일 경로 문제

**해결:**
1. index.html이 루트 디렉토리에 있는지 확인
2. 파일명 대소문자 확인 (대소문자 구분)
3. Actions 탭에서 배포 로그 확인

### ❌ CSS가 적용 안 됨
**원인:** 파일 경로 또는 HTTPS 문제

**해결:**
1. style.css 파일 존재 확인
2. HTML에서 경로 확인 (`<link rel="stylesheet" href="style.css">`)
3. 브라우저 캐시 삭제 (Ctrl+Shift+R 또는 Cmd+Shift+R)

### ❌ "Enforce HTTPS" 체크박스 비활성화
**원인:** DNS 체크가 아직 완료되지 않음

**해결:**
1. DNS 체크 성공 대기
2. 24시간 후에도 안 되면 Custom domain 제거 후 재설정

### ❌ Mixed Content 경고
**원인:** HTTP 리소스를 HTTPS 페이지에서 로드

**해결:**
모든 외부 리소스 URL을 HTTPS로 변경:
```html
<!-- 잘못된 예 -->
<script src="http://example.com/script.js"></script>

<!-- 올바른 예 -->
<script src="https://example.com/script.js"></script>
```

---

## 📊 배포 상태 확인

### GitHub에서 확인
```
레포지토리 → Settings → Pages
→ "Your site is live at https://cctv.musi.co.kr"
```

### 브라우저에서 확인
```
1. https://cctv.musi.co.kr 접속
2. 주소창 자물쇠 아이콘 확인 (HTTPS 활성화)
3. 모든 페이지 정상 작동 확인
```

### DNS 전파 확인
```
https://dnschecker.org
입력: cctv.musi.co.kr
타입: CNAME
→ 전 세계 DNS 서버에서 전파 상태 확인
```

---

## 🔄 파일 업데이트 방법

### 웹 인터페이스로 수정
```
1. GitHub 레포지토리에서 수정할 파일 클릭
2. 연필 아이콘(Edit) 클릭
3. 내용 수정
4. Commit changes
```

### 전체 파일 교체
```
1. Add file → Upload files
2. 새 파일 드래그 앤 드롭 (기존 파일 덮어씀)
3. Commit changes
```

**배포 시간:**
- 파일 수정 후 자동 배포: 1-5분
- Actions 탭에서 진행 상황 확인 가능

---

## ✅ 완료 체크리스트

배포 완료 전 최종 확인:

- [ ] GitHub 레포지토리 생성 (cctvApp)
- [ ] 모든 파일 업로드 (HTML, CSS, CNAME)
- [ ] GitHub Pages 활성화 (main 브랜치, root 폴더)
- [ ] Custom domain 설정 (cctv.musi.co.kr)
- [ ] DNS CNAME 레코드 추가
- [ ] DNS 체크 성공
- [ ] HTTPS 강제 활성화
- [ ] 웹사이트 정상 접속 확인
- [ ] 모든 페이지 작동 확인
- [ ] SSL 인증서 확인 (HTTPS)

---

## 🎯 다음 단계

1. **App Store Connect 설정**
   - Privacy Policy URL: https://cctv.musi.co.kr/privacy.html
   - Support URL: https://cctv.musi.co.kr/support.html
   - Marketing URL: https://cctv.musi.co.kr

2. **웹사이트 개선**
   - 스크린샷 추가
   - 앱 다운로드 링크 업데이트 (App Store URL)
   - Google Analytics 추가 (선택사항)

3. **유지보수**
   - 정기적인 개인정보처리방침 업데이트
   - FAQ 추가
   - 앱 버전 업데이트 시 "새로운 기능" 섹션 추가

---

## 📞 도움이 필요하신가요?

- GitHub Pages 문서: https://docs.github.com/en/pages
- GitHub Community: https://github.community/
- DNS 전파 확인: https://dnschecker.org

배포 성공을 기원합니다! 🎉
