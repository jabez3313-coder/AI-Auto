📚 eBook System

AI 기반 웹 eBook 스토리북 시스템

이 프로젝트는 텍스트, 이미지, 오디오, 영상을 포함한
웹 기반 eBook 스토리북을 생성하고 읽을 수 있는 시스템입니다.

🎯 프로젝트 목표
웹 기반 eBook 생성
10페이지 스토리북 기본 구조
자동 스토리 생성
자동 이미지 생성
모바일 친화적 eBook 뷰어

ebook-system/
│
├── README.md
├── SKILL.md
├── AGENTS.md
│
├── data/
│   └── stories/
│       ├── story-01.json
│       ├── story-02.json
│       └── stories.json
│
├── public/
│   ├── images/
│   ├── audio/
│   └── video/
│
├── web/
│   ├── index.html
│   ├── viewer.html
│   └── styles.css
│
├── agents/
│   ├── story-agent.md
│   ├── image-agent.md
│   └── ebook-agent.md


📖 Story Data Format

각 스토리는 JSON 파일로 저장됩니다.

예시

{
  "id": "story-01",
  "title": "Example Story",
  "pages": [
    {
      "text": "첫 번째 이야기"
    },
    {
      "image": "/images/story-01/story-01-01.jpg",
      "text": "두 번째 이야기"
    }
  ]
}
📚 Stories List

스토리 목록 파일

data/stories/stories.json

예시

[
  {
    "id": "story-01",
    "title": "첫 번째 이야기"
  },
  {
    "id": "story-02",
    "title": "두 번째 이야기"
  }
]
🖼 이미지 구조
public/images/
 └── story-01/
     ├── story-01-01.jpg
     ├── story-01-02.jpg
🖥 웹 구조
index.html

스토리 목록 화면

기능

스토리 자동 불러오기
스토리 클릭 → viewer 이동
viewer.html

eBook 읽기 화면

기능

이미지 표시
텍스트 표시
이전 / 다음 페이지
🤖 AI Agent

이 프로젝트는 AI 에이전트를 사용합니다.

Agents:

Story Agent
Image Agent
eBook Agent
🚀 확장 기능

향후 추가 가능

오디오북
영상 스토리북
자동 생성
카테고리 분류
검색 기능
모바일 앱 변환
🎨 지원 콘텐츠

이 시스템은 다음을 지원합니다.

텍스트 스토리
이미지 스토리
오디오북
영상 스토리북
📱 목표
감성 스토리북
성경 스토리북
어린이 스토리북
🔧 사용 방법
story JSON 생성
이미지 추가
stories.json 목록 추가
index.html 자동 표시
📌 Naming Rules

스토리

story-01.json
story-02.json

이미지

story-01-01.jpg
story-01-02.jpg
🌟 프로젝트 비전

이 프로젝트는 단순한 웹사이트가 아니라
AI 기반 디지털 스토리북 플랫폼을 목표로 합니다.

Version

v1.0
Antigravity eBook System
