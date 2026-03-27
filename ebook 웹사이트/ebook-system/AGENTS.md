🤖 AGENTS.md
eBook System Agents

이 프로젝트는 AI 에이전트를 사용하여
스토리 생성, 이미지 생성, eBook 구성 작업을 자동화합니다.

📚 Agent 구조
agents/
├── story-agent
├── image-agent
├── ebook-agent
├── index-agent
└── upload-agent
1️⃣ Story Agent
역할

스토리 생성

기능
10 페이지 스토리 생성
감성적인 스토리 생성
성경 스토리 생성
어린이 스토리 생성
출력
{
 "title": "Story Title",
 "pages": [
  {
   "text": "story text"
  }
 ]
}
규칙
따뜻한 분위기
감성적인 톤
쉬운 문장
10페이지 기본
2️⃣ Image Agent
역할

스토리 이미지 생성

기능
페이지별 이미지 생성
스타일 유지
캐릭터 일관성 유지
입력
story text
스타일
출력
public/images/story-01/

예

story-01-01.jpg
story-01-02.jpg
3️⃣ eBook Agent
역할

스토리 + 이미지 결합

기능
JSON 생성
페이지 구성
스토리 저장
출력
data/stories/story-01.json
4️⃣ Index Agent
역할

스토리 목록 자동 생성

기능
stories.json 생성
목록 자동 업데이트
출력
data/stories/stories.json

예

[
 {
  "id":"story-01",
  "title":"Story Title"
 }
]
5️⃣ Upload Agent
역할

파일 업로드 관리

기능
이미지 업로드
JSON 저장
자동 연결
Agent Workflow

전체 흐름

Story Agent
    ↓
Image Agent
    ↓
eBook Agent
    ↓
Index Agent
    ↓
Web Viewer
자동 생성 흐름

예

사용자 입력

Create story about Peter

실행

Story Agent 생성
Image Agent 생성
eBook Agent 저장
Index Agent 목록 추가
Naming Rules

스토리

story-01
story-02
story-03

이미지

story-01-01.jpg
story-01-02.jpg
확장 가능한 Agent

향후 추가 가능

audio-agent
video-agent
translate-agent
summary-agent
Future Agents

추천

narration-agent (오디오북)
animation-agent (영상 생성)
thumbnail-agent (표지 생성)
Project Goal

이 Agent 시스템은

자동 eBook 생성
자동 이미지 생성
자동 웹 업데이트

를 목표로 합니다.

Version

v1.0
Antigravity eBook Agent System
