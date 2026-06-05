# Daylog

22311889, 강은수, rkddmstnjj@gmail.com
https://github.com/keunsooo/22311889_swproject

---

[ Revision history ]


Revision date Version # Description Author
06/05/2026 0.1 First Draft


---


= Contents =



1. Introduction ..........................................................................................

2. Class diagram ........................................................................................

3. Sequence diagram ..................................................................................

4. State machine diagram ............................................................................ 

5. Implementation requirements ...................................................................

6. Glossary ....................................................................................................

7. References .................................................................................................


---

## 1. Introduction

현대인들은 수많은 정보와 바쁜 일상 속에서 자신만의 일정을 관리하며 삶의 균형을 찾으려 노력한다. 그러나 기존의 캘린더나 다이어리 프로그램들은 일정 관리라는 기능적 측면에만 치우쳐 있거나, 반대로 다이어리 꾸미기와 같은 시각적 감성을 충족하기 위해서는 별도의 그래픽 도구를 병행 사용해야 하는 파편화된 환경을 가지고 있다. "Daylog"는 데스크톱 환경을 기반으로, 현대인들이 하나의 플랫폼 안에서 개인의 시간과 일상, 그리고 이를 개성 있게 꾸미는 예술적 감성을 안전하고 편리하게 결합할 수 있도록 돕고자 고안되었다.

"Daylog"는 개인의 일상 기록과 시간 관리를 하나의 직관적인 사용자 경험(UX)으로 통합한 개인화 캘린더 및 다이어리 데스크톱 애플리케이션이다. 기존의 정형화되고 딱딱한 일정 관리 도구들과 달리, 본 시스템은 사용자가 자신의 감성과 개성을 화면에 투영할 수 있도록 고안되었다. 핵심 기능으로서 체계적인 회원가입, 로그인 및 로그아웃과 같은 인증 시스템을 제공하며, 달력 기반의 정교한 일정 추가 기능, 일 단위의 할 일을 직관적으로 관리하는 투두리스트, 그리고 그날의 감정과 기록을 남길 수 있는 일기 컴포넌트가 유기적으로 상호작용한다. 특히, 애플리케이션 전반의 UI 색상을 자유롭게 변경할 수 있는 테마 커스텀 엔진과 사용자가 로컬 이미지를 직접 업로드하여 다이어리 화면 위에 스티커처럼 자유롭게 배치하고 꾸밀 수 있는 인터랙티브 캔버스 기능을 제공한다.

"Daylog"의 핵심 설계 주안점은 다음과 같다. 첫째, 로컬 우선 보안 인증 및 사용자 격리이다. 로컬 데스크톱 환경 내에서 안전하게 구동되는 사용자 가입, 세션 인증 및 로그아웃 프로세스를 정의하여 개인 정보 노출을 원천 차단한다. 둘째, 뷰 레이어와 비즈니스 로직의 명확한 독립화이다. 일정 및 투두리스트, 일기 데이터를 처리하는 비즈니스 도메인을 독립적인 서비스 레이어로 격리한다. 셋째, 동적 실시간 테마 엔진 디자인이다. 정적 스타일링 구조를 벗어나 사용자가 선택한 테마 색상 메타데이터가 즉각 반영되는 유연한 테마 변환 아키텍처를 설계하였다. 마지막으로, 인터랙티브 데코레이션 레이어 구현이다. 일기 및 달력 뷰 상단에 독립적인 캔버스 오버레이 레이어를 배치하여, 사용자가 첨부한 이미지를 자유롭게 가공하고 스티커 형태로 배치·수정할 수 있도록 하는 확장형 데이터 모델을 정립한다.


---


## 2. Class Diagram

<img width="1890" height="1856" alt="Image" src="https://github.com/user-attachments/assets/2992e5b1-7a02-475c-aa60-22e02f0e72f4" />

| 클래스 | 주요 속성 | 주요 메서드 | 설명 |
| --- | --- | --- | --- |
| **User** | userid, email, passwordHash, username, profileImage, themeColor, createdAt | register(), login(), logout(), updateProfile(), changeTheme() | 등록된 사용자. 모든 콘텐츠를 소유한다. |
| **Event** | eventId, userid, title, description, startDate, endDate, color, stickers[] | create(), update(), delete(), addSticker() | 캘린더 일정. 색상과 스티커를 가질 수 있다. |
| **Todo** | todoId, userid, date, title, isCompleted, priority | create(), toggle(), update(), delete() | 날짜별 할 일 항목. 완료 토글 및 우선순위 지원. |
| **Diary** | diaryId, userid, date, content, mood, images[], stickers[] | create(), update(), delete(), attachImage() | 날짜별 일기. 텍스트, 기분 태그, 이미지, 스티커 지원. |
| **Sticker** | stickerId, imageUrl, posX, posY, scale | place(), move(), resize(), remove() | 캔버스 위 자유 배치. 크기 조정 가능한 이미지 스티커. |
| **Image** | imageId, url, filename, uploadedAt | upload(), delete() | 업로드된 이미지. 클라우드 스토리지에 저장된다. |
| **Theme** | themeId, name, primaryColor, secondaryColor, backgroundColor | apply(), preview() | 전역 색상 팔레트 정의. |
| **AuthService** | jwtSecret | generateToken(), verifyToken(), hashPassword() | 비밀번호 해싱, JWT 생성·검증 담당. |
| **CalendarService**| — | getMonthEvents(), getDayEvents() | 월별·일별 이벤트 조회 서비스. |


---


## 3. Sequence Diagrams

시퀀스 다이어그램은 UML 표준에 따라 액터 헤더, 수직 라이프라인(점선), 활성화 박스, 번호가 붙은 메시지 화살표로 구성됩니다. 실선 화살표는 동기 호출, 점선 화살표는 반환 메시지를 나타낸다.

### 3.1 회원가입 (User Registration)

<img width="1517" height="1232" alt="Image" src="https://github.com/user-attachments/assets/aeedce63-36b7-49cc-b20c-b1a8f179b26a" />

사용자가 회원가입 폼(사용자명, 이메일, 비밀번호)을 작성한다. 프론트엔드는 `POST /auth/register` 요청을 AuthService로 전송합니다. AuthService는 bcrypt로 비밀번호 해시를 생성하고 DB에 신규 사용자를 저장한다. 성공 시 JWT 토큰이 반환되고 캘린더 메인 페이지로 리다이렉트된다.

### 3.2 로그인 (User Login)

<img width="1517" height="1232" alt="Image" src="https://github.com/user-attachments/assets/58e0d6cb-5c4f-4e33-a5fa-47e8240c68a2" />


사용자가 이메일과 비밀번호를 입력힌다. AuthService는 DB에서 해당 이메일의 사용자를 조회하고 bcrypt로 비밀번호 해시를 검증한다. 검증 성공 시 서명된 JWT 토큰이 반환되고 localStorage에 저장된다. 실패 시 오류 메시지가 표시된다.

### 3.3 캘린더 일정 추가 (Add Calendar Event)

<img width="1667" height="1337" alt="Image" src="https://github.com/user-attachments/assets/90716a23-4a24-4524-8844-9be3ed97c27e" />

사용자가 캘린더의 날짜를 클릭하면 EventModal이 열린다. 제목, 시간 범위, 색상 등 이벤트 정보를 입력하고 저장하면 `POST /events`가 JWT와 함께 호출된다. CalendarService는 토큰을 검증하고 DB에 이벤트를 삽입한다. 반환된 데이터로 캘린더 뷰가 즉시 업데이트된다.

### 3.4 투두리스트 관리 (Todo List Management)

<img width="1517" height="1967" alt="Image" src="https://github.com/user-attachments/assets/c6d18cd6-747f-45b8-b47a-6bcd83a8a6ee" />

사용자가 특정 날짜의 투두 패널을 연다. 기존 투두 항목을 불러오고, 새 항목 추가 시 `POST /todos`가 호출되어 DB에 저장된다. 완료 체크박스 클릭 시 `PATCH /todos/{id}`로 isCompleted 상태가 토글된다.

### 3.5 일기 및 이미지 스티커 (Diary Entry with Image Sticker)

<img width="1667" height="1862" alt="Image" src="https://github.com/user-attachments/assets/d7cda5aa-659f-4942-99a3-0bc1253f2f16" />

사용자가 날짜별 일기 페이지를 연다. 텍스트 작성, 이미지 첨부(StorageService 업로드), 스티커 배치(X/Y 좌표 저장)를 모두 수행한 뒤 `PUT /diary/{id}`로 전체 일기를 저장한다.

### 3.6 테마 색상 변경 (Theme Color Change)

<img width="1517" height="1547" alt="Image" src="https://github.com/user-attachments/assets/99cfda3e-9e9a-4eef-a21b-d3263ab8106d" />

사용자가 설정 페이지에서 테마 목록을 불러온다. 원하는 테마를 선택하면 `PUT /user/theme`로 사용자 프로필의 테마 ID가 업데이트된다. 반환된 새 테마 색상이 React의 전역 테마 Context에 즉시 적용된다.

---

## 4. State Machine Diagrams

상태 머신 다이어그램은 UML 표준에 따라 초기 상태(●), 상태(둥근 사각형), 전환(화살표+레이블), 최종 상태(◎)로 구성된다. 점선 테두리 영역은 논리적 그룹을 나타낸다.

### 4.1 클라이언트 상태 머신

<img width="2117" height="2717" alt="Image" src="https://github.com/user-attachments/assets/24d5bfcb-7c91-4f07-b118-ff256f3bd53f" />

클라이언트는 비로그인 상태에서 시작하며 로그인/회원가입 옵션만 표시한다. 인증 성공 후 캘린더 메인(CalendarMain)(중앙 허브)으로 전환된다. 기능 영역(점선 박스)에서 EventModal(일정 생성/편집), TodoPanel(투두 관리), DiaryPage(일기 작성), ThemeSettings(테마 설정) 4가지 기능 상태로 이동할 수 있다. DiaryPage 내에서는 StickerCanvas 서브 상태가 스티커 배치를 처리한다. 로그아웃 시 로그아웃 확인 상태를 거쳐 비로그인 상태로 돌아가거나 앱을 종료한다.

### 4.2 서버 상태 머신

<img width="2117" height="2717" alt="Image" src="https://github.com/user-attachments/assets/a0c5b8da-26c9-413f-b714-0b6acc46260d" />

서버는 Idle(대기) 상태에서 시작한다. 인증 요청 수신 시 Authenticating(인증 중) 상태로 전환된다. 인증 성공 시 Authorized(인가됨)으로, 실패 시 Error 상태(401/400 반환)로 이동 후 Idle 로 복귀한다. Authorized 상태에서는 요청 유형에 따라 ProcessingEvent, ProcessingTodo, ProcessingDiary, UploadingImage 처리 상태로 분기되며, 각 처리 상태는 DB/스토리지 작업 후 결과를 반환하고 Authorized로 복귀합니다. 세션 만료 또는 로그아웃 시 Idle로 돌아간다.

---

## 5. Implementation Requirements

| 분류 | 기술 / 요구사항 | 버전 / 비고 |
| --- | --- | --- |
| **프론트엔드** | React + TypeScript | React 18+, TypeScript 5+ |
| **상태 관리** | Recoil | 0.7+ |
| **스타일링** | SCSS Modules + CSS Variables | Sass 1.x |
| **빌드 도구** | Vite | 5.x |
| **날짜 처리** | date-fns, rrule | date-fns 3.x |
| **백엔드** | Node.js + Express | Node 18+, Express 4.x |
| **인증** | JWT + bcrypt | JWT HS256 |
| **데이터베이스** | PostgreSQL | PostgreSQL 15+ |
| **ORM** | Prisma | Prisma 5.x |
| **이미지 저장소**| AWS S3 또는 Firebase Storage | 멀티파트 업로드 지원 |
| **데스크탑 (선택)**| Electron | Electron 28+ |
| **OS** | Windows 10/11, macOS 12+, Ubuntu 20.04+ | 크로스플랫폼 |
| **브라우저** | Chrome 110+, Firefox 115+, Safari 16+, Edge 110+ | ES2022 지원 필수 |
| **테스트** | Vitest + React Testing Library | 커버리지 ≥ 80% |
| **패키지 관리자**| Yarn | Yarn 4.x (Berry) |

---

## 6. Glossary

| 용어 | 정의 |
| --- | --- |
| **JWT** | 무상태 인증에 사용되는 컴팩트한 토큰 형식. 서명된 페이로드(userId, 만료시간)를 포함한다. |
| **bcrypt** | 연산 비용이 높은 비밀번호 해시 함수. 브루트포스 공격을 어렵게 만든다. |
| **SPA** | 단일 HTML 페이지를 로드하고 이후 콘텐츠를 동적으로 업데이트하는 웹 앱. |
| **REST API** | HTTP 메서드(GET, POST, PUT, DELETE)를 사용하는 네트워크 앱 설계 스타일. |
| **Recoil** | React용 상태 관리 라이브러리. atom과 selector로 반응형 상태를 구현한다. |
| **스티커** | 일기 캔버스 위에 자유롭게 배치, 크기 조정 가능한 이미지 요소. |
| **테마** | 앱 전체 시각 외관을 변경하는 전역 색상 변수 집합. |
| **Todo** | 특정 날짜의 할 일 항목. 완료 상태와 우선순위를 가진다. |
| **Diary** | 날짜별 개인 일기. 텍스트, 기분 태그, 이미지, 스티커를 지원한다. |
| **Event** | 날짜에 활동을 예약하는 캘린더 항목. 제목, 시간 범위, 색상 태그 포함. |
| **ORM** | DB 테이블을 프로그래밍 객체에 매핑하는 도구. |
| **SCSS Modules** | 컴포넌트 범위의 CSS 전처리기 파일. 스타일 충돌을 방지한다. |
| **Electron** | 웹 기술로 크로스플랫폼 데스크탑 앱을 만드는 프레임워크. |
| **상태 머신** | 유한한 상태 집합, 이벤트로 트리거되는 전환, 액션으로 구성된 계산 모델. |
| **라이프라인** | 시퀀스 다이어그램에서 객체의 존재 기간을 나타내는 수직 점선. |
| **활성화 박스** | 시퀀스 다이어그램에서 객체가 메시지를 처리하는 기간을 나타내는 직사각형. |

---

## 7. References

- flaticon https://www.flaticon.com/
