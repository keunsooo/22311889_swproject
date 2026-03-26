1. Conceptualization



To Do Calendar

22311889 강은수 rkddmstnjj@gmail.com



[ Revision history ]


Revision date
Version #
Description
Author
03/26/2026
0.1
First Draft

























= Contents =




1. Business purpose ..................................................................................

2. System context diagram .......................................................................

3. Use case list .........................................................................................

4. Concept of operation ............................................................................ 

5. Problem statement ................................................................................

6. Glossary .................................................................................................

7. References .................................................................................................


1. Business purpose
1.1 project background
 현대 사회에서는 학업, 업무, 개인 일정 등 다양한 활동이 동시에 이루어지면서 효율적인 시간 관리의 중요성이 점점 증가하고 있다. 이에 따라 일정을 관리하는 캘린더나 할 일을 정리할 수 있는 투 두 리스트 애플리케이션은 일상 생활에서 빼 놓을수 없는 도구가 되었다. 기존의 일정 관리 애플리케이션들은 기본적인 기능은 충실히 제공하지만, 사용자의 개별적인 취향이나 라이프스타일을 충분히 반영하지 못하는 한계가 있다. 사용자 인터페이스와 기능 구성에 있어 개인 맞춤형 설정이 부족하여 아쉬운 경우가 많다. 또한 일정 관리와 할 일 관리가 서로 분리된 형태로 제공되는 경우가 많아  
사용자는 여러 애플리케이션을 동시에 사용해야 하는 불편함을 겪는다. 이로 인해 정보가 분산되고 전체적인 관리 효율성이 떨어지는 문제가 발생한다. 

1.2 motivation
 일정 관리와 할 일 관리를 동시에 수행하고자 하는 사용자 요구를 기반으로 ‘To Do Calendar’는 사용자가 자신의 일정과 할 일을 하나의 애플리케이션에서 통합적으로 관리할 수 있도록 한다. 또한 사용자 중심 맞춤형 일정 관리 시스템과 다양한 취향을 반영할 수 있는 유연한 UI에 대한 요구가 늘어남에 따라 개인의 취향에 맞게 인터페이스를 커스터마이징 할 수 있는 환경을 제공을 제공하는 것을 목표로 한다.

1.3 goal
- 일정과 할 일을 통합 관리할 수 있는 시스템 개발한다. 
- 사용자 맞춤형 UI 및 테마 설정 기능을 제공한다.
- 직관적이고 사용하기 쉬운 인터페이스를 구현한다.
- 사용자가 보다 효율적으로 시간을 관리할 수 있도록 한다.

1.4 target market
학생(고등학생, 대학생), 직장인, UI를 자유롭게 커스터마이징 하면서 일정 관리가 필요한 일반 사용자









2. System context diagram



- Register  회원가입
- Login  로그인
- Logout  로그아웃  
- View Calendar  일정 조회  
- Add Schedule  일정 추가  
- Modify Schedule  일정 수정  
- Delete Schedule  일정 삭제  
- Add To-Do  할 일 추가  
- Complete To-Do  할 일 완료 처리  
- Delete To-Do  할 일 삭제  
- Customize UI  UI 커스터마이징  
- Apply UI Settings 테마 적용










3. Use case list

1) Register 

Actor
User
Description
등록되어있지 않은 사용자가 기능을 사용하기 위해 회원으로 등록한다.


2) Login

Actor
User
Description
사용자가 등록한 자신의 아이디로 로그인한다.


3) Logout

Actor
User
Description
사용자가 자신의 아이디를 로그아웃한다.


4) View Calendar

Actor
User
Description
사용자는 자신이 추가, 삭제한 한달 간의 일정을 한 눈에 조회할 수 있다.


5) Add Schedule

Actor
User
Description
사용자는 자신의 일정을 캘린더에 추가할 수 있다.


6) Modify Schedule

Actor
User
Description
사용자는 자신이 추가한 일정 중에 잘못된 내용이 있으면 수정할 수 있다.


7) Delete Schedule

Actor
User
Description
사용자는 자신이 추가한 일정 중에 필요가 없어진 내용이 있으면 일정을 삭제할 수 있다.

8) Add To-Do

Actor
User
Description
사용자는 자신의 할 일을 추가할 수 있다.


9) Complete To-Do

Actor
User
Description
사용자는 자신이 추가한 할 일을 완료했다면 할 일에 완료 표시를 할 수 있다.


10) Delete To-Do

Actor
User
Description
사용자는 자신이 추가한 할 일을 삭제할 수 있다.


11) Costomize UI

Actor
User
Description
사용자는 자신의 개인 취향과 라이프스타일에 맞게 UI를 꾸밀 수 있다.


12) Apply UI Settings 

Actor
System
Description
시스템은 사용자가 커스텀한 UI 설정을 적용시켜 준다.

4. Concept of operation
1) Register 회원가입

Purpose
앱을 사용하기 위해 사용자 등록
Approach
사용자가 회원 정보를 입력하면 서버에 저장하여 새로운 계정을 생성한다.
Dynamics
회원가입 요청 시
Goals
사용자 계정을 생성해 로그인을 할 수 있도록 한다.


2) Login 로그인

Purpose
앱을 사용하기 위해 등록된 사용자인지 인증
Approach
사용자가 ID와 비밀번호를 입력하면 서버에서 회원 정보를 확인하고 로그인 성공 여부를 반환한다.
Dynamics
앱 실행 후 로그인 요청 시
Goals
로그인한 사용자들에게 프로그램의 기능을 제공한다.


3) View Calendar 일정 조회 

Purpose
사용자가 자신의 일정을 조회
Approach
사용자가 캘린더 화면을 요청하면 DB에서 일정 데이터를 불러와 화면에 표시한다.
Dynamics
캘린더 화면 진입 시
Goals
사용자의 한 달간의 일정을 한 눈에 출력 시켜 줌으로써 확인 가능하게 한다.


4) Add Schedule 일정 추가

Purpose
사용자가 자신의 일정을 추가
Approach
사용자가 날짜와 내용을 입력하면 DB에 저장한다.
Dynamics
일정 추가 요청 시
Goals
사용자가 자신의 일정을 추가할 수 있도록 구현한다.
 

5) Modify Schedule 일정 수정

Purpose
사용자가 자신의 일정을 수정
Approach
사용자가 기존 일정 정보를 수정하여 DB에 업데이트 한다.
Dynamics
일정 수정 요청 시
Goals
사용자가 자신의 일정을 수정할 수 있도록 구현한다.

6) Delete Schedule 일정 삭제

Purpose
사용자가 자신의 일정을 삭제
Approach
사용자가 일정을 선택하면 DB에서 삭제한다.
Dynamics
일정 삭제 요청 시
Goals
사용자가 자신의 일정을 삭제할 수 있도록 구현한다.


7) Add To-Do 할 일 추가

Purpose
사용자가 자신의 할 일을 추가
Approach
사용자가 할 일을 이볅하면 리스트에 추가하고 DB에 저장한다.
Dynamics
할 일 추가 시
Goals
사용자가 자신의 할 일을 추가할 수 있도록 구현한다.


8) Complete To-Do 할 일 완료

Purpose
사용자가 자신의 일정을 완료
Approach
사용자가 할 일을 완료 상태로 변경하면 DB에 반영한다.
Dynamics
완료 체크 시
Goals
사용자가 자신의 할 일 상태를 변경할 수 있도록 구현한다.


9) Delete To-Do 할 일 삭제

Purpose
사용자가 자신의 할 일을 삭제
Approach
사용자가 할 일을 선택하면 DB에서 삭제한다.
Dynamics
할 일 삭제 요청 시
Goals
사용자가 자신의 할 일을 삭제할 수 있도록 구현한다.


10) Customize UI UI 설정 변경

Purpose
사용자가 UI를 변경
Approach
사용자가 자신의 취향에 맞게 테마 및 색상을 변경하면 설정이 저장되고 UI에 반영된다.
Dynamics
UI 설정 변경 시
Goals
사용자가 자신의 UI 설정을 변경할 수 있도록 구현한다.






5. Problem statement
데이터 저장 및 동기화 과정에서 발생하는 오류 - 일정 및 할 일 정보는 빈번하게 추가, 수정, 삭제되기 때문에 데이터 처리 과정에서 오류가 발생할 가능성이 있으며, 이를 방지하기 위한 안정적인 데이터 처리 로직이 필요하다.

다양한 사용자 입력에 대한 예외 처리 필요성 - 사용자가 입력하는 일정 정보나 할 일 내용은 형식이 일정하지 않기 때문에 잘못된 입력이나 비정상적인 데이터로 인해 시스템 오류가 발생하지 않도록 검증 과정이 필요하다.

사용자 UI 설계의 복잡성 - 캘린더와 투두리스트 기능을 하나의 화면에서 효율적으로 제공해야 하므로 가독성이 좋은 인터페이스를 설계하는 것이 중요하다.

여러 기능 간의 충돌 및 성능 저하 문제 – 일정 데이터 추가/삭제, UI 저장 등이 동시에 이루어질 경우, 시스템의 응답 속도가 저하될 수 있으므로 효율적인 처리 방식이 요구된다. 

NFRs
-빠른 데이터 처리 속도와 원활한 화면 전환을 제공해야 한다.
-사용자가 직관적으로 사용할 수 있는 UI/UX를 제공해야 한다.
-데이터 손실 없이 안정적으로 동작해야 한다.


















6. Glossary

용어
설명
Calendar
사용자의 일정 정보를 보여준다.
To-Do List
사용자가 해야 할 작업 목록이다.
User
시스템을 사용하는 사용자
Customization
사용자 설정에 따른 UI 변경.


7. References
구글 캘린더 https://calendar.google.com
