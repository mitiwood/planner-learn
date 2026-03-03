# PlannerAI — Git & Vercel 배포 가이드

## 프로젝트 구조

plannerai/
├── public/
│   ├── login.html      (소셜 로그인 페이지)
│   ├── mobile.html     (모바일 앱 — 다크모드 포함)
│   └── admin.html      (관리자 대시보드)
├── vercel.json         (Vercel 라우팅 설정)
├── .gitignore
└── README.md

---

## STEP 1 — 로컬 폴더 세팅

mkdir plannerai
cd plannerai
mkdir public

# 다운로드한 파일들을 public/ 폴더에 복사
cp ~/Downloads/login.html    public/login.html
cp ~/Downloads/mobile.html   public/mobile.html
cp ~/Downloads/admin.html    public/admin.html

# vercel.json, .gitignore 도 루트에 복사
cp ~/Downloads/vercel.json   vercel.json
cp ~/Downloads/.gitignore    .gitignore

---

## STEP 2 — Git 초기화 및 GitHub 푸시

# Git 초기화
git init

# 최초 커밋
git add .
git commit -m "feat: PlannerAI 초기 프로젝트 세팅

- 소셜 로그인 (Google / Kakao / Naver)
- 모바일 앱 (라이트/다크 모드)
- 관리자 대시보드 (프롬프트 CRUD, 사용자 관리, 분석)"

# GitHub에 새 레포 생성 후 연결
# (GitHub에서 'plannerai' 레포 먼저 생성)
git remote add origin https://github.com/YOUR_USERNAME/plannerai.git
git branch -M main
git push -u origin main

---

## STEP 3 — Vercel 배포 (방법 A: CLI)

# Vercel CLI 설치
npm install -g vercel

# 로그인
vercel login

# 배포 (프로젝트 루트에서)
vercel

# 프로덕션 배포
vercel --prod

---

## STEP 3 — Vercel 배포 (방법 B: GitHub 연동 — 권장)

1. https://vercel.com 접속 후 로그인
2. "Add New Project" 클릭
3. GitHub 레포 'plannerai' 선택
4. Framework Preset: Other (Static Site)
5. Root Directory: ./ (루트 그대로)
6. "Deploy" 클릭

=> 이후 main 브랜치에 git push 하면 자동 배포됨

---

## STEP 4 — 이후 업데이트 워크플로우

# 파일 수정 후
git add public/mobile.html
git commit -m "feat: 다크모드 UI 개선"
git push origin main
# => Vercel이 자동으로 재배포

---

## 배포 후 URL 구조

https://plannerai.vercel.app/           → login.html (메인 진입)
https://plannerai.vercel.app/app        → mobile.html (모바일 앱)
https://plannerai.vercel.app/admin      → admin.html (관리자)

---

## 자주 쓰는 Git 명령어 모음

# 상태 확인
git status

# 전체 스테이징 + 커밋
git add . && git commit -m "커밋 메시지"

# 특정 파일만 커밋
git add public/mobile.html
git commit -m "fix: 모바일 앱 버그 수정"

# 원격 최신 코드 받기
git pull origin main

# 브랜치 생성 및 전환 (기능 개발 시)
git checkout -b feature/quiz-improvement

# PR 머지 후 main 동기화
git checkout main
git pull origin main

# 커밋 로그 확인
git log --oneline --graph

# 실수로 수정한 파일 되돌리기
git checkout -- public/mobile.html

# 마지막 커밋 수정 (push 전에만)
git commit --amend -m "수정된 커밋 메시지"
