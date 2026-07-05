<div align="center">

# Quartz-Obsidian

**Obsidian 지식 베이스를 Quartz v4 정적 사이트로 배포하기 위한 저장소**

![Quartz v4](https://img.shields.io/badge/Quartz_v4-10B981?style=flat-square) ![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white) ![Node 22+](https://img.shields.io/badge/Node_22+-339933?style=flat-square&logo=nodedotjs&logoColor=white) ![Markdown](https://img.shields.io/badge/Markdown-000000?style=flat-square&logo=markdown&logoColor=white)

[English](./README.en.md)

</div>

---

## 소개

이 저장소는 Quartz v4를 기반으로 Obsidian/Markdown 지식 베이스를 정적 웹사이트로 게시하기 위한 저장소입니다. 기본 upstream README만 남아 있었지만, 실제 `content/`에는 Programming, DevOps, Mathematics, AI, Computer Science, Data Engineering, 모두의입법 관련 노트가 들어 있습니다.

Quartz 설정은 `quartz.config.ts`에서 관리하며, Obsidian flavored markdown, GFM, Table of Contents, KaTeX, content index, RSS/sitemap, custom OG image plugin을 사용합니다.

## 주요 기능

| 기능 | 설명 |
|---|---|
| 디지털 가든 게시 | `content/` 아래 Markdown 문서를 Quartz 정적 사이트로 변환합니다. |
| Obsidian 호환 Markdown | Obsidian flavored markdown과 shortest link resolution을 사용합니다. |
| 검색/인덱스 | ContentIndex, sitemap, RSS를 활성화합니다. |
| 수식/코드 지원 | KaTeX와 syntax highlighting plugin을 사용합니다. |
| 지식 영역 | Programming, AI, Computer Science, Data Engineering, 모두의입법 등 주제별 노트를 포함합니다. |

## 저장소 구조

| 경로 | 역할 |
|---|---|
| content/ | Published Markdown knowledge base |
| quartz.config.ts | Quartz site configuration |
| quartz.layout.ts | Quartz layout configuration |
| quartz/ | Quartz CLI and framework source |
| package.json | Node scripts and dependencies |

## 빠른 시작

### 의존성 설치

```bash
npm install
```

### Quartz CLI 실행

```bash
npx quartz build
```

### 로컬 미리보기

```bash
npx quartz build --serve
```

### 타입/포맷 확인

```bash
npm run check
```

## 검증

| 항목 | 명령 |
|---|---|
| Quartz check | `npm run check` |
| Build site | `npx quartz build` |

## 운영 메모

- Node.js 22 이상과 npm 10.9.2 이상이 필요합니다.
- `content/private`, `content/templates`, `.obsidian`은 Quartz ignore pattern에 포함됩니다.
- 사이트 제목, baseUrl, locale은 실제 배포 대상에 맞게 갱신하는 것이 좋습니다.

## 문서 작성 근거

이 README는 저장소 안의 다음 파일과 문서를 기준으로 작성했습니다.

- `README.md`
- `package.json`
- `quartz.config.ts`
- `content/`
