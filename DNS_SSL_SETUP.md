# 🌐 DNS 및 SSL 설정 가이드

## 📋 개요

이 가이드는 musi.co.kr 도메인에 cctv.musi.co.kr 서브도메인을 추가하고, GitHub Pages와 연결하여 자동 SSL 인증서를 적용하는 방법을 설명합니다.

---

## 1️⃣ DNS 설정

### 필요한 정보 확인

먼저 GitHub username을 확인하세요:
```
GitHub 프로필 → Settings → 왼쪽 상단의 username
예: yourusername
```

### CNAME 레코드 추가

**설정해야 할 레코드:**
```
Type:  CNAME
Name:  cctv (또는 cctv.musi.co.kr)
Value: yourusername.github.io.
TTL:   3600 (또는 1 hour, 또는 자동)
```

---

## 2️⃣ DNS 제공자별 설정 방법

### 🔹 Cafe24 (카페24)

#### Step 1: 로그인
```
https://www.cafe24.com
→ 나의 Cafe24 → 도메인 관리
```

#### Step 2: 도메인 선택
```
musi.co.kr 선택 → DNS 관리
```

#### Step 3: 레코드 추가
```
1. '레코드 추가' 버튼 클릭
2. 레코드 정보 입력:
   - 레코드 타입: CNAME
   - 호스트명: cctv
   - 값/주소: yourusername.github.io.
   - TTL: 3600
3. '저장' 또는 '확인' 클릭
```

---

### 🔹 Gabia (가비아)

#### Step 1: 로그인
```
https://www.gabia.com
→ My가비아 → 서비스 관리 → 도메인
```

#### Step 2: DNS 관리
```
musi.co.kr 선택 → DNS 관리 → DNS 설정
```

#### Step 3: 레코드 추가
```
1. '레코드 추가' 클릭
2. 레코드 정보:
   - 타입: CNAME
   - 호스트: cctv
   - 값/위치: yourusername.github.io.
   - TTL: 1시간 (3600초)
3. '확인' 클릭
```

---

### 🔹 AWS Route 53

#### Step 1: Hosted Zone 선택
```
AWS Console → Route 53 → Hosted zones
→ musi.co.kr 선택
```

#### Step 2: Create Record
```
1. 'Create record' 버튼 클릭
2. Record 설정:
   - Record name: cctv
   - Record type: CNAME
   - Value: yourusername.github.io
   - TTL: 300 (5분) 또는 3600 (1시간)
   - Routing policy: Simple routing
3. 'Create records' 클릭
```

---

### 🔹 Cloudflare

#### Step 1: Dashboard 접속
```
https://dash.cloudflare.com
→ musi.co.kr 도메인 선택
```

#### Step 2: DNS 탭
```
DNS → Records
```

#### Step 3: Add Record
```
1. 'Add record' 클릭
2. 레코드 정보:
   - Type: CNAME
   - Name: cctv
   - Target: yourusername.github.io
   - Proxy status: DNS only (회색 구름)
   - TTL: Auto
3. 'Save' 클릭
```

**중요:**
- ⚠️ Proxy status를 **'DNS only'**로 설정 (회색 구름 아이콘)
- GitHub Pages의 SSL과 충돌 방지

---

### 🔹 기타 DNS 제공자

대부분의 DNS 제공자는 비슷한 인터페이스를 제공합니다:

1. DNS 관리 페이지 접속
2. 새 레코드 추가
3. 다음 정보 입력:
   ```
   타입: CNAME
   호스트/이름: cctv
   값/대상: yourusername.github.io.
   TTL: 3600 또는 기본값
   ```
4. 저장

---

## 3️⃣ DNS 전파 확인

### 온라인 도구로 확인

#### DNS Checker
```
https://dnschecker.org

입력:
- 도메인: cctv.musi.co.kr
- 레코드 타입: CNAME

결과:
전 세계 DNS 서버에서 전파 상태 확인
모두 초록색 체크: 전파 완료
```

#### What's My DNS
```
https://www.whatsmydns.net

CNAME 선택 → cctv.musi.co.kr 입력
전 세계 DNS 서버별 응답 확인
```

### 터미널에서 확인

#### macOS / Linux
```bash
# CNAME 레코드 확인
nslookup cctv.musi.co.kr

# 또는
dig cctv.musi.co.kr CNAME

# 결과 예시:
# cctv.musi.co.kr. 3600 IN CNAME yourusername.github.io.
```

#### Windows (CMD / PowerShell)
```cmd
nslookup cctv.musi.co.kr

# 결과에서 확인:
# cctv.musi.co.kr canonical name = yourusername.github.io
```

---

## 4️⃣ SSL 인증서 설정 (자동)

### GitHub Pages의 자동 SSL

GitHub Pages는 **Let's Encrypt**를 사용하여 자동으로 SSL 인증서를 발급합니다.

#### 활성화 조건:
1. ✅ Custom domain이 설정되어 있어야 함
2. ✅ DNS 체크가 성공해야 함
3. ✅ CNAME 파일이 레포지토리에 있어야 함

#### 활성화 방법:

##### Step 1: DNS 체크 완료 대기
```
GitHub 레포지토리 → Settings → Pages
→ Custom domain 섹션에서 DNS 체크 성공 확인
```

**표시 메시지:**
```
✅ DNS check successful
```

##### Step 2: HTTPS 강제 활성화
```
Settings → Pages 하단
☑ Enforce HTTPS 체크박스 활성화
```

**주의:**
- DNS 체크 실패 시 이 옵션 비활성화됨
- 체크 후 인증서 발급까지 수 분 소요

##### Step 3: 인증서 발급 확인
```
1-5분 후 웹사이트 접속:
https://cctv.musi.co.kr

브라우저 주소창에 🔒 자물쇠 아이콘 확인
```

---

## 5️⃣ SSL 인증서 확인

### 브라우저에서 확인

#### Chrome / Edge
```
1. https://cctv.musi.co.kr 접속
2. 주소창 자물쇠 아이콘 클릭
3. '연결이 안전함' 확인
4. '인증서' 또는 'Certificate' 클릭
5. 발급자: Let's Encrypt 확인
6. 유효기간 확인 (90일)
```

#### Firefox
```
1. https://cctv.musi.co.kr 접속
2. 주소창 자물쇠 아이콘 클릭
3. '연결 보안' → '자세히 보기'
4. 인증서 정보 확인
```

#### Safari
```
1. https://cctv.musi.co.kr 접속
2. 주소창 자물쇠 아이콘 클릭
3. '인증서 보기' 클릭
4. 발급자 및 유효기간 확인
```

### 온라인 도구로 확인

#### SSL Labs
```
https://www.ssllabs.com/ssltest/

입력: cctv.musi.co.kr
분석 완료 후 등급 확인 (A 이상 권장)
```

#### SSL Checker
```
https://www.sslshopper.com/ssl-checker.html

입력: cctv.musi.co.kr
인증서 체인 및 설정 확인
```

---

## 6️⃣ 문제 해결

### ❌ DNS가 전파되지 않음

**증상:**
- `nslookup` 결과가 나오지 않음
- dnschecker.org에서 빨간 X 표시

**해결:**
```
1. DNS 레코드 설정 재확인
   - 타입: CNAME (A 레코드 아님)
   - 이름: cctv (앞에 @ 없음)
   - 값: yourusername.github.io. (끝에 점)

2. TTL 시간 대기
   - 최소: 5분
   - 최대: 48시간 (보통 1-2시간)

3. DNS 캐시 삭제
   macOS/Linux: sudo dscacheutil -flushcache
   Windows: ipconfig /flushdns

4. 시크릿 모드에서 테스트
```

---

### ❌ "DNS check failed"

**증상:**
- GitHub Pages에서 DNS 체크 실패

**해결:**
```
1. CNAME 파일 확인
   - 파일명: CNAME (대문자, 확장자 없음)
   - 내용: cctv.musi.co.kr (한 줄, 개행 없음)
   - 위치: 레포지토리 루트

2. DNS 전파 확인
   - dnschecker.org에서 전 세계 확인
   - 대부분 초록색이 될 때까지 대기

3. Custom domain 재설정
   - Settings → Pages → Custom domain 삭제
   - Save
   - 다시 cctv.musi.co.kr 입력
   - Save

4. 24시간 대기
```

---

### ❌ HTTPS 체크박스가 비활성화됨

**증상:**
- "Enforce HTTPS" 체크박스를 클릭할 수 없음

**원인:**
- DNS 체크가 아직 완료되지 않음

**해결:**
```
1. DNS 체크 성공 대기
   Settings → Pages에서 상태 확인

2. DNS 전파 완료 확인
   dnschecker.org 사용

3. 강제 새로고침
   - Custom domain 재설정
   - 1-5분 대기 후 페이지 새로고침
```

---

### ❌ SSL 인증서 오류

**증상:**
- "Your connection is not private" 경고
- NET::ERR_CERT_COMMON_NAME_INVALID

**해결:**
```
1. HTTPS 활성화 확인
   Settings → Pages → Enforce HTTPS 체크

2. 인증서 발급 대기
   - 첫 활성화 시 최대 10분 소요
   - Actions 탭에서 진행 상황 확인

3. 브라우저 캐시 삭제
   - Ctrl+Shift+Delete (Windows)
   - Cmd+Shift+Delete (Mac)
   - 캐시된 이미지 및 파일 삭제

4. 시크릿 모드에서 테스트

5. 24시간 후에도 안 되면
   - Custom domain 제거
   - HTTPS 체크 해제
   - 5분 대기
   - Custom domain 재설정
   - HTTPS 재활성화
```

---

### ❌ "NET::ERR_CERT_DATE_INVALID"

**원인:**
- 컴퓨터 시간이 잘못 설정됨

**해결:**
```
시스템 시간 확인 및 수정
- Windows: 설정 → 시간 및 언어
- Mac: 시스템 환경설정 → 날짜 및 시간
- 자동 설정 권장
```

---

## 7️⃣ 유지보수

### SSL 인증서 갱신

**Let's Encrypt 인증서:**
- 유효기간: 90일
- 자동 갱신: GitHub Pages가 자동으로 처리
- 조치 필요: 없음 (완전 자동)

### 모니터링

정기적으로 확인:
```
월 1회:
- https://cctv.musi.co.kr 접속 확인
- SSL 인증서 유효기간 확인
- DNS 레코드 확인

변경 시:
- DNS 제공자 변경 시 레코드 재설정
- GitHub username 변경 시 DNS 업데이트
```

---

## 8️⃣ 참고 자료

### 공식 문서
- GitHub Pages: https://docs.github.com/en/pages
- GitHub Pages Custom Domain: https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site
- Let's Encrypt: https://letsencrypt.org/

### 도구
- DNS Checker: https://dnschecker.org
- SSL Labs: https://www.ssllabs.com/ssltest/
- What's My DNS: https://www.whatsmydns.net

---

## ✅ 설정 완료 체크리스트

DNS 및 SSL 설정 완료 확인:

- [ ] DNS CNAME 레코드 추가 완료
- [ ] DNS 전파 확인 (dnschecker.org)
- [ ] nslookup으로 CNAME 확인
- [ ] GitHub Pages에서 DNS check successful
- [ ] HTTPS 강제 활성화
- [ ] SSL 인증서 발급 확인 (🔒 아이콘)
- [ ] 모든 페이지 HTTPS로 접속 가능
- [ ] SSL Labs에서 A 등급 이상
- [ ] HTTP → HTTPS 자동 리다이렉트 확인

---

## 🎯 예상 소요 시간

| 단계 | 소요 시간 |
|------|----------|
| DNS 레코드 추가 | 5분 |
| DNS 전파 대기 | 1-2시간 (최대 48시간) |
| GitHub DNS 체크 | 자동 (DNS 전파 후) |
| SSL 인증서 발급 | 1-10분 |
| **총 예상 시간** | **2-3시간** |

---

## 💡 Pro Tips

1. **DNS 전파 시간 단축**
   - TTL을 짧게 설정 (300초)
   - 변경 후 TTL을 다시 길게 (3600초)

2. **Cloudflare 사용 시**
   - Proxy status를 'DNS only'로 설정
   - GitHub Pages SSL과 충돌 방지

3. **www 서브도메인 추가**
   ```
   CNAME  www.cctv  cctv.musi.co.kr.
   ```
   www.cctv.musi.co.kr도 접근 가능

4. **Apex 도메인 사용**
   서브도메인 대신 musi.co.kr 직접 사용 시:
   ```
   A  @  185.199.108.153
   A  @  185.199.109.153
   A  @  185.199.110.153
   A  @  185.199.111.153
   ```

---

DNS 및 SSL 설정 완료를 축하합니다! 🎉
