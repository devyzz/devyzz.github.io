# 🌐 devyzz.github.io

![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-%F0%9F%93%9A-blue?logo=github&logoColor=white)
![Blog](https://img.shields.io/badge/Tech%20Blog-%F0%9F%93%9D-lightgrey)
![Status](https://img.shields.io/badge/Status-Active-brightgreen)

> **개발자 devyzz의 기술 블로그**  
> 개발 여정과 학습 기록, 프로젝트 후기 및 코딩 철학을 담고 있습니다.  
> 직접 구성하고 꾸민 GitHub Pages 기반의 정적 블로그입니다.

---

## 🧭 블로그 주소

[https://devyzz.github.io](https://devyzz.github.io)

---

## ✍️ 블로그 주요 콘텐츠

- 📌 **Learning Log**: 개발 및 데이터 엔지니어링 학습 기록  
- ⚙️ **CS 지식**: 운영체제, 네트워크, 자료구조/알고리즘 정리  
- 🧪 **프로젝트**: 개인 및 팀 프로젝트 회고와 구현기  
- 🔍 **기술 분석**: 개발 이슈와 트렌드, 기술 리서치  

---

## 🛠️ 사용 스택

| 구성 요소       | 기술 |
|----------------|------|
| 정적 블로그 프레임워크 | [Jekyll](https://jekyllrb.com/) (또는 직접 구성) |
| 배포 플랫폼     | GitHub Pages |
| 마크다운 스타일링 | Markdown + HTML |
| 테마/스타일     | 직접 커스터마이징 (또는 Minimal/Hyde 등 사용) |

---

## 📁 폴더 구조 (예시)

```bash
.
├── _posts/             # 블로그 글
├── _layouts/           # 레이아웃 템플릿
├── _includes/          # 공통 컴포넌트 (헤더, 푸터 등)
├── assets/             # 이미지, 스타일 파일
├── index.html          # 메인 페이지
└── _config.yml         # Jekyll 설정

## 로컬 실행방법
# 1. Jekyll 설치
gem install bundler jekyll

# 2. 의존성 설치
bundle install

# 3. 로컬 서버 실행
bundle exec jekyll serve

# 4. 브라우저에서 확인
http://localhost:4000

