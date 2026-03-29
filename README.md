# AuraFriday fusion-mcp-claude 다운로드 한국어 버전 
이 프로젝트는 AuraFriday의 클로드 데스크톱과 퓨전 360을 MCP로 연결하는 방법을 체계적으로 정리한 목록이다.

## 목차 

- [소개](#-소개)
- [주요 기능](#-주요-기능)
- [시작하기 (설치 및 실행)](#-시작하기)
- [사용 방법](#-사용-방법)
- [자료 정리](#-자료-정리)

## 소개
이 프로젝트는 AuraFriday의 클로드 데스크톱과 퓨전 360을 MCP로 연결하는 방법을 체계적으로 정리한 목록이다.
이 프로젝트는 MCP를 이용해 클로드 데스크톱과 퓨전 360을 연결하여 자연어로 모델링 하는데 목적을 두고 있다.

## 주요 기능 
- 클로드를 이용한 자연어 모델링

## 시작하기 (Getting Started)

### 요구 사항 (Prerequisites)
- 클로드 데스크톱 [다운로드](https://claude.com/ko-kr/download)
- 퓨전 360 [다운로드](https://www.autodesk.com/products/fusion-360/personal)
- Node.js (LTS) [다운로드](https://nodejs.org/ko/download)
- npm (Node.js 설치 시 함께 설치됨)
- 깃허브 데스크톱(클론 하려면 필요함, 필수는 아님) [다운로드](https://desktop.github.com/download/)
- vs code [다운로드](http://code.visualstudio.com/Download)

### 설치 및 실행

1. **MCP Link Server 설치**

  - 운영 체제에 맞는 MCP Link Server 실치. [https://github.com/AuraFriday/mcp-link-server/releases/tag/latest](https://github.com/AuraFriday/mcp-link-server/releases/tag/latest)

2. **저장소 클론**

- **깃허브 데스크톱이 있는 겨우**

  - cmd를 열고 아래 명령어 입력
  ```bash
  git clone https://github.com/AuraFriday/Fusion-360-MCP-Server.git
  ```
  클론 한 폴더 저장 위치: C:\Users\(사용자 이름) (내PC -> 로컬 디스크(c) -> (사용자 이름))
  폴더 이름: Fusion-360-MCP-Server

- **깃허브 데스크톱을 다운로드 안한 경우**

  - 여기로 이동 [https://github.com/AuraFriday/Fusion-360-MCP-Server](https://github.com/AuraFriday/Fusion-360-MCP-Server)
  - 녹색 Code 버튼 클릭
  - Download ZIP 클릭
  - 다운로드 폴더에 있는 파일 압축 풀기
  - C:\Users\(사용자 이름) (내PC -> 로컬 디스크(c) -> (사용자 이름))으로 압축 푼 폴더 전체 이동

- **git clone 명령어가 오류 날 경우**

  - powershell을 열고 아래 명령어 입력
  ```bash
  winget upgrade --id Git.Git
  ```
  - 터미널 재시작 후 다시 git clone 명령어 실행

3. **퓨전 ADD-IN 추가**

- 퓨전에서 새 디자인 생성 후 상단 매뉴에서 유틸리티 선택
- "ADD-INS" 클릭 
- 상단에 "+" 누르기
- 클론 한 폴더 찾기(Fusion-360-MCP-Server)
- 폴더 선택
- "MCP-Link"가 추가 됐는지 확인(오른쪽에 핑크 뇌 모양 이미지)
- "Run", "Run on startup" 체크

4. **퓨전에서 TEXT COMMANDS 실행**

- 새 디자인 화면에 "Ctrl + Alt + C" 입력 후 하단에 "TEXT COMMANDS" 생성됨
- "TEXT COMMANDS" 오른쪽에 "+" 버튼 누르기
- 오른쪽 하단에 "Txt", "Py", "Js" 중 "Py" 선택

5. **로컬 API 암호 확인**

- 파일 탐색기에서 C:\AuraFriday\mcp-link-server\bin 여기로 이동 (내PC -> 로컬 디스크C -> AuraFriday -> mcp-link-server -> bin)
- "nativemassaging.json" 파일 VS code로 열기
- 7번째 줄에 "Authorization": "Bearer (로컬 API 암호)"에서 로컬 API 암호 복사(6번에서 사용)

6. **클로드랑 퓨전 MCP로 연결**

- 클로드 대스크톱에서 "설정 -> 개발자 -> Edit config"
- 파일 탐색기가 열리면 "claude_desktop_config.json" 파일 VS Code로 샐행
- 아래 코드를 그대로 붙여넣기, 5번에서 복사한 로컬 API 암호를 "Authorization: Bearer (여기 로컬 API 암호 입력)"에 붙여넣기
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
        "Authorization: Bearer (여기 로컬 API 암호 입력)"
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

## 사용 방법

- AuraFriday MCP-Link Sever 백그라운드에 실행
- 퓨전에서 디자인에 들어간 뒤 ADD-IN에서 MCP-Link가 활성화 되어있는지 확인
- 퓨전에서 TEXT COMMANDS에 아래 텍스트가 나오면 MCP 서버 연결 성공!
```python
 [MCP] [SUCCESS] fusion360 registered successfully!
 [MCP] Listening for reverse tool calls...
 [MCP] ============================================================
 [MCP] Listening for reverse tool calls...
```
- 클로드 데스크톱 실행
- 새 채팅에서 왼쪽에 "+" 버튼 누르기
- 커넥터에 "mypc"라고 뜨면 연결 성공!
- 이제 마음껏 모델링 하세요~^-^

## 자료 정리

AuraFriday Fusion-360-MCP-Server. [https://github.com/AuraFriday/Fusion-360-MCP-Server](https://github.com/AuraFriday/Fusion-360-MCP-Server)
AuraFriday MCP link server. [https://github.com/AuraFriday/mcp-link-server/releases/tag/latest](https://github.com/AuraFriday/mcp-link-server/releases/tag/latest)