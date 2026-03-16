# AI Dev OS Plugin — Kiro — 운영 가이드

## 목차

1. [전제 조건](#1-전제-조건)
2. [설치](#2-설치)
3. [초기 설정](#3-초기-설정)
4. [일상 워크플로우](#4-일상-워크플로우)
5. [정기 유지보수](#5-정기-유지보수)
6. [팀 온보딩](#6-팀-온보딩)
7. [언어 정책](#7-언어-정책)
8. [문제 해결](#8-문제-해결)

---

## 1. 전제 조건

- [Kiro](https://kiro.dev/) >= 1.0.0
- 프로젝트에 AI Dev OS 레이어 파일(L1-L3)이 설정되어 있을 것 (템플릿: [TypeScript](https://github.com/yunbow/ai-dev-os-rules-typescript) / [Python](https://github.com/yunbow/ai-dev-os-rules-python))

---

## 2. 설치

### 방법 A: 스티어링 규칙 복사 (권장)

```bash
git clone https://github.com/yunbow/ai-dev-os-plugin-kiro.git
cp -r ai-dev-os-plugin-kiro/steering/ .kiro/steering/
cp -r ai-dev-os-plugin-kiro/hooks/ .kiro/hooks/
cp -r ai-dev-os-plugin-kiro/checklist-templates/ .kiro/checklist-templates/
```

### 방법 B: Git Submodule

```bash
git submodule add https://github.com/yunbow/ai-dev-os-plugin-kiro.git .kiro/plugins/ai-dev-os
cp -r .kiro/plugins/ai-dev-os/steering/* .kiro/steering/
cp -r .kiro/plugins/ai-dev-os/hooks/* .kiro/hooks/
```

### 훅 설정

Kiro 훅은 Hook UI에서도 설정할 수 있습니다:
1. 명령 팔레트 열기 (`Ctrl+Shift+P` / `Cmd+Shift+P`)
2. "Kiro: Open Kiro Hook UI" 입력
3. `hooks/hooks.json`의 설정에 맞게 훅 생성

---

## 3. 초기 설정

### 설정 마법사 실행

Kiro 채팅에서 호출:
```
#ai-dev-os-init [tech-stack]
```

예시:
```
#ai-dev-os-init nextjs
```

---

## 4. 일상 워크플로우

### 4.1 구현 전 계획

```
#ai-dev-os-plan JWT 사용자 인증 추가
```

### 4.2 구현 대신 티켓 생성

```
#ai-dev-os-ticket JWT 사용자 인증 추가
```

### 4.3 코드 작성

평소처럼 코드를 작성합니다. 스티어링 규칙과 훅이 자동으로 가이드합니다.

### 4.4 커밋 전

```
#ai-dev-os-check
```

### 4.5 코드 리뷰 후

```
#ai-dev-os-extract [file-path]
```

### 4.6 규칙 이해

```
#ai-dev-os-why "왜 any 타입이 금지인가요?"
```

---

## 5. 정기 유지보수

### 월간: 건전성 감사

```
#ai-dev-os-audit
```

### 분기별: SECI 나선 진화

```
#ai-dev-os-evolve
```

### 주간/월간: 준수 보고서

```
#ai-dev-os-report 1w
#ai-dev-os-report 1m
```

---

## 6. 팀 온보딩

### 신규 구성원용

1. `ai-dev-os/01_philosophy/core-values.md` 읽기 (5분)
2. `ai-dev-os/02_decision-criteria/` 훑어보기 (10분)
3. 불분명한 규칙에 대해 `#ai-dev-os-why` 호출
4. 코딩 시작 — 스티어링 규칙과 훅이 자동으로 안내

### AI Dev OS를 도입하는 팀용

1. 프로젝트에서 `#ai-dev-os-init` 호출
2. **starter** 템플릿(L3만)으로 시작
3. 코드 리뷰마다 `#ai-dev-os-extract` 사용
4. 2-4주 후 `#ai-dev-os-audit`으로 갭 식별
5. `#ai-dev-os-evolve`로 L1-L2를 점진적으로 구축

---

## 7. 언어 정책

모든 소스 파일(steering rules, hooks, templates)은 **영어**로 관리됩니다. 이는 LLM의 최적 정확도와 폭넓은 접근성을 보장하기 위함입니다.

---

## 8. 문제 해결

### 스티어링 규칙이 활성화되지 않음

- 스티어링 파일이 `.kiro/steering/` 디렉토리에 있는지 확인
- YAML frontmatter가 유효한지 확인
- 수동 스티어링은 채팅에서 `#name`으로 호출
- 자동 스티어링은 `description` 필드가 대화 컨텍스트와 일치하는지 확인

### 훅이 트리거되지 않음

- 훅이 `.kiro/hooks/` 디렉토리에 설정되어 있는지 확인
- Kiro Hook UI에서 설정 (`Ctrl+Shift+P` → "Kiro: Open Kiro Hook UI")
- `jq`가 설치되어 있는지 확인

### Kiro Specs와 AI Dev OS 연계

Kiro의 스펙 기반 개발(요구사항 → 설계 → 태스크)은 AI Dev OS를 보완합니다:
- Kiro Specs로 기능 기획과 태스크 분해
- AI Dev OS 가이드라인은 스펙 태스크 실행 시 품질 게이트로 활용

---

Languages: [English](../../operation-guide.md) | [日本語](../ja/operation-guide.md) | [简体中文](../zh-CN/operation-guide.md) | 한국어 | [Español](../es/operation-guide.md)
