# fusion-mcp-claude
이 파일은 AuraFriday의 클로드 데스크톱과 퓨전 360을 MCP로 연결하는 방법을 체계적으로 정리한 목록이다.

## 목차 

- [소개](#-소개)
- [주요 기능](#-주요-기능)
- [시작하기 (설치 및 실행)](#-시작하기)
- [사용 방법](#-사용-방법)
- [자료 정리](#-자료-정리)

## 소개
이 파일은 AuraFriday의 클로드 데스크톱과 퓨전 360을 MCP로 연결하는 방법을 체계적으로 정리한 목록이다.
이 프로젝트는 MCP를 이용해 클로드 데스크톱과 퓨전 360을 연결하여 자연어로 모델링 하는데 목적을 두고 있다.

## 주요 기능
- 기능 1: 클로드를 이용한 자연어 모델링 

## 시작하기 (Getting Started)

### 요구 사항 (Prerequisites)
- 클로드 데스크톱
- 퓨전 360
- Node.js (LTS)
- npm (Node.js 설치 시 함께 설치됨)
- 깃허브(필수는 아님)
- vs code

### 설치 및 실행

1. MCP Link Server 설치

운영 체제에 맞는 MCP Link Server 실치. [https://github.com/AuraFriday/mcp-link-server/releases/tag/latest](https://github.com/AuraFriday/mcp-link-server/releases/tag/latest)

2. 저장소 클론
```bash
git clone [https://github.com/AuraFriday/Fusion-360-MCP-Server.git](https://github.com/AuraFriday/Fusion-360-MCP-Server.git)
```
클론 한 폴더 저장 위치: C:\Users\(사용자 이름) (내PC -> 로컬 디스크(c) -> (사용자 이름))
폴더 이름: Fusion-360-MCP-Server

3. 퓨전 ADD-IN 추가

- 퓨전에서 새 디자인 생성 후 상단 매뉴에서 유틸리티 선택
- "ADD-INS" 클릭 
- 상단에 "+" 누르기
- 클론 한 폴더 찾기(Fusion-360-MCP-Server)
- 폴더 선택
- "MCP-Link"가 추가 됐는지 확인
- "Run", "Run on startup" 체크
- 닫기
- "Ctrl + Alt + C" 입력 후 하단에 "TEXT COMMANDS" 생성됨
- "TEXT COMMANDS" 옆에 "+" 버튼 누르기
- 오른쪽 하단에 "Txt", "Py", "Js" 중 "Py" 선택

4. 클로드랑 퓨전 MCP 연결

- 클로드 대스크톱에서 "설정 -> 개발자 -> Edit config"
- 파일 탐색기가 열리면 "claude_desktop_config.json" 파일 VS Code로 샐행
- 아래 코드 붙여넣기
```json
{
  "mcpServers": {
    "mypc": {
      "command": "npx.cmd",
      "args": [
        "-y",
        "mcp-remote@latest",
        "https://127-0-0-1.local.aurafriday.com:31173/sse",
        "--header",
        "Authorization: Bearer (개인 API 키 입력)"
      ],
      "env": {
        "NODE_TLS_REJECT_UNAUTHORIZED": "0"
      }
    }
  },
  "preferences": {
    "menuBarEnabled": false,
    "legacyQuickEntryEnabled": false,
    "coworkScheduledTasksEnabled": false,
    "ccdScheduledTasksEnabled": false,
    "sidebarMode": "chat",
    "coworkWebSearchEnabled": true
  }
}
```

5. 

## 사용 방법



## 자료 정리

AuraFriday 깃허브. [https://github.com/AuraFriday/Fusion-360-MCP-Server](https://github.com/AuraFriday/Fusion-360-MCP-Server)
AuraFriday MCP link server. [https://github.com/AuraFriday/mcp-link-server/releases/tag/latest](https://github.com/AuraFriday/mcp-link-server/releases/tag/latest)
Node.js 다운로드. [https://nodejs.org/ko/download](https://nodejs.org/ko/download)
