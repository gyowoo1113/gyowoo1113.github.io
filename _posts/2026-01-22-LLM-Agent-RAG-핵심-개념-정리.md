---
layout: post
title: LLM / Agent / RAG 핵심 개념 정리
date: 2026-01-22
lang: ko
categories:
  - Knowledge
  - ETC
tags:
  - AI
  - 이론
typora-root-url: ../
---

---
## 서론

  최근 개발에 AI·MCP 도입이 이루어지고 있는데, 실제 AI를 개발하는 과정이나 관련 이론은 무엇인지 관심을 가지게 되어 간략하게 개념을 정리해보았습니다.

---

## LLM (Large Language Model)

- 대규모 텍스트 데이터로 학습된 언어 모델
- **입수하지 못한 정보에 대해서는 답변 불가능**
- **환각(Hallucination)**  
  - 질의를 완전히 이해하지 못했더라도 그럴듯한 답변을 생성할 수 있음
- 기본적으로 외부 시스템(DB, API, 파일)에 접근 불가

> LLM은 말을 잘하는 엔진이며, 지식을 정확히 보장하는 시스템은 아니다

---

## AGENT

> **생각(Planning) → 기억(Memory) → 도구 사용(Tool Use) →  목표 달성까지 스스로 실행하는(Autonomous) LLM**

- 단순 질의응답을 넘어 **행동 주체**로 동작
- 목표를 입력받아 작업을 분해하고 반복 실행

### 구성 요소

- **Planning**
  - 목표를 단계별 작업으로 분해
- **Memory**
  - 작업 맥락 및 과거 정보 유지
  - RAG를 통한 Knowledge Base 참조 포함
- **Tool Use**
  - DB 조회, API 호출, 파일 처리, 코드 실행 등
- **Autonomous**
  - 사람의 추가 개입 없이 다음 행동을 스스로 판단

> RAG는 Agent의 **Memory 또는 Tool 중 하나**로 사용됨

---

## RAG (Retrieval-Augmented Generation)

> **답변 생성 이전에 신뢰 가능한 정보를 검색(Retrieval)하고 해당 정보를 기반(Context)으로 답변을 생성하는 구조**

### 주요 구성 요소

- **Vector DB**
  - 임베딩된 문서를 저장하는 데이터베이스
  - 의미 기반 검색(Semantic Search)을 지원
- **Retrieval**
  - 사용자 질의와 가장 유사한 문서를 탐색하는 과정
- **Knowledge Base**
  - RAG가 Retrieval 단계에서 참조하는 지식 저장소
- **Context**
  - 검색된 문서를 LLM이 이해할 수 있도록 프롬프트에 주입한 정보

### 효과

- 환각(Hallucination) 감소
- 최신 정보 및 도메인 지식 반영
- 근거 기반 답변 생성

---

## EMBEDDING

> **자연어 텍스트를 의미를 보존한 벡터(점)로 표현하는 기술**

### 특징

- **Text-to-Vector**
  - 문장 또는 문서를 고차원 숫자 벡터로 변환
- **Vector Space**
  - 의미가 유사한 텍스트일수록 가까운 위치에 존재
- **Semantic Search**
  - 키워드가 일치하지 않아도 의미 기준으로 검색 가능
- **RAG 핵심 기술**
  - 질의와 문서를 동일한 벡터 공간에서 비교

---
