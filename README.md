# 💻 클라이언트 프로그래머 포트폴리오

> **"DirectX부터 서버까지, 바닥부터 단단하게 다져온 프로그래머"**

안녕하세요, 기본기의 힘을 믿는 클라이언트 개발자 류성민입니다. 
게임이 화면에 그려지는 원리를 이해하기 위해 DirectX와 자체 엔진을 연구했고, 데이터의 흐름을 알기 위해 AWS 서버까지 직접 구축했습니다. 
이러한 폭넓은 기술적 베이스를 바탕으로 언리얼 엔진 5를 깊이 있게 활용하며, 화려한 연출 뒤에 숨겨진 복잡한 로직들을 안정적으로 구현해내는 역할을 수행하고 있습니다.

</br>

## 📜 목차
### 1. 📄 프로젝트 개요
- 🔗 1. [[UE5] 액션 게임 프로젝트 (25.10 ~ 25. 11)](https://github.com/kabu0330/UE_Soul2) 
- 🔗 2. [[UE5, AWS] Dedicated Server 프로젝트 (25.05 ~ 25.08)](https://github.com/kabu0330/FPS_with_DedicatedServer) 
- 🔗 3. [[UE5 팀 프로젝트] 시뮬레이션 게임 (Overcooked! 2 모작) (25.02 ~ 25.05)](https://github.com/kabu0330/UE_Overcooked2) 
- 🔗 4. [[DirectX 11] 2D 액션 게임 프로젝트 (Hollow Knight 모작) (24.11 ~ 25.02)](https://github.com/kabu0330/DX_HollowKnight2) 
- 🔗 5. [[Win API] 슈팅 게임 프로젝트(The Binding of Isaac 모작) (24.07 ~ 24.11)](https://github.com/kabu0330/WinAPI) 

</br>

### 2. 📑 주요 구현 내용 
### 🚀 대표 주제

제가 프로젝트들을 진행하며 문제 해결을 깊이 고민했던 여섯가지 주제입니다. ✅

1.  **[컨텐츠]** 타격감과 반응성을 극대화한 전투 시스템 구현
    * 🔗 [유연한 콤보 시스템: 이벤트 기반 Perfect/Mercy 구간을 통한 공격 후딜레이 캔슬 및 콤보 연계](#ue5-액션-유연한-콤보-시스템-이벤트-기반-perfectmercy-구간-설정) 
    * 🔗 [루트 모션 기반 자연스러운 대시 구현](#ue5-액션-루트-모션-기반-자연스러운-대시-구현--motion-warping)
2.  **[안정성]** 애니메이션 중단 시에도 꼬이지 않는 견고한 상태 동기화
    * 🔗 [애니메이션 라이프 사이클 기반 비동기 상태 관리](#ue5-액션-애니메이션-라이프-사이클-기반-비동기-상태-관리)
3.  **[확장성]** 코드 수정 없는 데이터 관리 및 UI 결합도 최소화
    * 🔗 [데이터 에셋 기반 무기별 전투 스타일 관리](#ue5-액션-데이터-에셋-기반-무기별-전투-스타일-관리)
    * 🔗 [델리게이트(Delegate)를 활용한 유연한 인벤토리 시스템](#ue5-액션-델리게이트delegate를-활용한-유연한-인벤토리-시스템)
4.  **[리팩토링]** 강한 결합도(Tight Coupling) 해소를 위한 리팩토링
    * 🔗 [[리팩토링] OCP(개방 폐쇄 원칙) 기반 설계: 상속에서 인터페이스로 전환](#리팩토링-ocp개방-폐쇄-원칙-기반-설계-상속에서-인터페이스로-전환)
    
### 2-1. 상태 관리 시스템
- 🔗 [```Enum```의 한계 → ```FSM Component```](#directx-11-enum의-한계--fsm-component)
- 🔗 [상태 관리: StateComponent와 ```GameplayTag```](#ue5-액션-상태-관리-statecomponent와-gameplaytag)
- 🔗 [애니메이션 라이프 사이클 기반 비동기 상태 관리](#ue5-액션-애니메이션-라이프-사이클-기반-비동기-상태-관리) ✅
### 2-2. 컨텐츠 구현
- 🔗 [다중좌표계 간 위치 동기화](#directx-11-다중-좌표계-간-위치-동기화)
- 🔗 [유연한 콤보 시스템: 이벤트 기반 Perfect/Mercy 구간을 통한 공격 후딜레이 캔슬 및 콤보 연계](#ue5-액션-유연한-콤보-시스템-이벤트-기반-perfectmercy-구간을-통한-공격-후딜레이-캔슬-및-콤보-연계) ✅
- 🔗 [루트 모션 기반 자연스러운 대시 구현](#ue5-액션-루트-모션-기반-자연스러운-대시-구현--motion-warping) ✅
- 🔗 [데이터 에셋 기반 무기별 전투 스타일 관리](#ue5-액션-데이터-에셋-기반-무기별-전투-스타일-관리) ✅
- 🔗 [델리게이트(Delegate)를 활용한 유연한 인벤토리 시스템](#ue5-액션-델리게이트delegate를-활용한-유연한-인벤토리-시스템) ✅
- 🔗 [다이나믹 머티리얼로 강조 효과 구현하기](#ue5-팀-프로젝트-다이나믹-머티리얼로-강조-효과-구현하기) 
### 2-3. 네트워크
- 🔗 [지연 초기화: 런타임 액터 스폰, BeginPlay 호출 전 DataTable 데이터 무결성 확보](#ue5-팀-프로젝트-지연-초기화-런타임-액터-스폰-beginplay-호출-전-datatable-데이터-무결성-확보) 
- 🔗 [비동기 폴링 기반 서버 접속 시도](#dedicated-server-비동기-폴링-기반-서버-접속-시도)
- 🔗 [```SeamlessTravel```: 레벨 전환 시 데이터 유실 방지](#dedicated-server-seamlesstravel-레벨-전환-시-데이터-유실-방지) 
- 🔗 [콜백(Callback) 체인을 활용한 데이터 무결성 확보](#dedicated-server-콜백callback-체인을-활용한-데이터-무결성-확보) 
### 2-4. 협업 및 버전 관리
- 🔗 [Pull-Request 시행착오와 교훈](#ue5-팀-프로젝트-pull-request-시행착오와-교훈)
### 2-5. 최적화 전략 
- 🔗 [Unity 리소스 메타데이터 파싱을 통한 스프라이트 시트 관리](#directx-11-unity-메타데이터-파싱을-통한-스프라이트-시트-관리)
- 🔗 [[리팩토링] CPU 성능 최적화: ```Tick``` 의존성 해소, 이벤트 기반(Event-Driven Architecture)으로의 전환](#ue5-액션-리팩토링-cpu-성능-최적화-tick-의존성-해소-이벤트-기반event-driven-architecture으로의-전환) 
- 🔗 [네트워크 복제 대역폭 최적화: ```Fast Array Serializer```를 활용한 배열 요소 단위 델타 복제(Delta Replication)](#dedicated-server-네트워크-복제-대역폭-최적화-fast-array-serializer를-활용한-배열-요소-단위-델타-복제delta-replication) 
### 2-6. 회고
- 🔗 [```PlayerController```가 입력을 처리하는게 적절한가?](#playercontroller가-입력을-처리하는게-적절한가) 
- 🔗 [[리팩토링] OCP(개방 폐쇄 원칙) 기반 설계: 상속에서 인터페이스로 전환](#리팩토링-ocp개방-폐쇄-원칙-기반-설계-상속에서-인터페이스로-전환) ✅

</br>

## 📄 1. 프로젝트 개요
### 🔭 [UE5] 액션 게임 프로젝트
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\SoulPlay.webp">
</p>

* 🔗 [Youtube](https://youtu.be/8U4345QKBfc)
* 🔗 [Github](https://github.com/kabu0330/UE_Soul2)

### 📋 프로젝트 정보

<details>
<summary><b>📖 상세 정보 펼치기</b></summary>

| 항목 | 내용 | 항목 | 내용 |
|:------|:-----|:-----|:-----|
| 🖥️ **플랫폼** | PC (Windows) | 🎮 **장르** | 액션 |
| 👤 **개발 인원** | 1인 | 📅 **개발 기간** | 2025.10 ~ 2025.11 |
| 🛠️ **개발 도구** | C++, Unreal Engine 5 | | |
| 📝 **게임 소개** | 스태미나 기반 전투 액션 게임 | | |

### 💻 작업 내용

| 분류 | 상세 내용 |
|:-----|:----------|
| **컨텐츠** | 캐릭터, 몬스터, 전투 시스템, 인벤토리 시스템, UI |
| **애니메이션** | 스테이트 머신, 블렌드 포즈, 리타게팅, 모션 워핑 |
| **상태 관리** | 게임플레이 태그 컨테이너 |
| **AI** | Behavior Tree, Patrol, Perception|
| **기타** | 메타 휴먼, 포스트 프로세싱 |

</details>

### 🎯 작업 목표
**이벤트 기반 설계 및 타격감 있는 전투 시스템 구현**
- Tick 기반 → 이벤트 기반(Input, Timer, Delegate, AnimNotify) 전환
- 섬세한 타격감을 위한 애니메이션 타이밍 설계
- 언리얼 기능 적극 활용 (Motion Warping, BT, 블루프린트 테스트)

### 📊 핵심 성과
- ✅ ```Tick``` 사용 최소화
  - AI 기능 외 ```Tick``` 미사용
  -  ```UWeaponCollisionComponent``` 및 ```UTargetingComponent```에서 제한적 사용
- ✅ GameplayTag Container로 복잡한 상태 관리 간소화
- ✅ OnMontageEnded Delegate로 애니메이션 중단 시에도 안정적인 상태 처리

> 💡 **배운 점**: Tick 기반에서 이벤트 기반으로 전환하면서 코드가 훨씬 명확해졌습니다. "언제 실행되는지"를 Timer와 Delegate로 명시하니 디버깅도 쉬워지고, AnimNotify로 애니메이션과 로직을 분리하니 전투 시스템 확장이 보다 쉬워졌습니다. 

</br>

___

### 🔭 [UE5, AWS] Dedicated Server 프로젝트
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\DedicatedServer.webp">
</p>

* 🔗 [Youtube](https://youtu.be/8tyiK_7egvI?si=MP7l8gBIcKs95v6U)
* 🔗 [Github](https://github.com/kabu0330/FPS_with_DedicatedServer)

### 📋 프로젝트 정보
<details>
<summary><b>📖 상세 정보 펼치기</b></summary>

| 항목 | 내용 | 항목 | 내용 |
|:------|:-----|:-----|:-----|
| 🖥️ **플랫폼** | PC (Windows) | 🎮 **장르** | FPS |
| 👤 **개발 인원** | 1인 | 📅 **개발 기간** | 2025.05 ~ 2025.08 |
| 🛠️ **개발 도구** | C++, Node.js, Unreal Engine 5, AWS |
| 📝 **게임 소개** | 최대 10인의 플레이어가 경쟁하는 1인칭 슈팅게임 |

### 💻 작업 내용

| 분류 | 상세 내용 |
|:-----|:----------|
| **모듈** | 서버 전용 모듈 구현, 컨텐츠 모듈과 분리 |
| **사용자 관리** | 회원가입, 본인 인증(e-mail), 로그인 |
| **세션 관리** | 게임 세션 및 게임 플레이어 세션, 토큰 생성 및 관리 |
| **Seamless Travel** | 레벨 전환 및 플레이어 데이터 동기화 |
| **DB** | 플레이 개인 기록 및 랭킹 시스템 |
| **UMG** | UI제작 |

</details>

### 🎯 작업 목표
**서버-클라이언트 아키텍처 및 AWS 클라우드 인프라 실전 경험**
- Dedicated Server 구조 이해 (Authority 기반 설계)
- AWS SDK 활용 (EC2, Lambda, DynamoDB, GameLift)
- 네트워크 동기화 문제 해결 (RPC/Replication, SeamlessTravel)

### 📊 핵심 성과
- ✅ AWS SDK C++ 빌드 및 UE 프로젝트 연동
- ✅ SeamlessTravel 시 PlayerState 동기화 문제 해결 (```CopyProperties```, ```OverrideWith```)
- ✅ 컨텐츠/서버 전용 모듈 분리
- ✅ FFastArraySerializer 적용 네트워크 복제 비용 최적화

> 💡 **배운 점**: Dedicated Server를 직접 구축하며 **서버의 역할**을 보다 잘 이해하게 되었습니다. 클라이언트에서 보이는 것과 서버에서 계산하는 것을 분리하고, Replication 타이밍을 제어하는 과정에서 네트워크 게임의 기본 구조를 이해하게 되었습니다. "중단점 없이 로그만 보고 디버깅"하는 경험이 처음엔 어려웠지만, 덕분에 로그를 활용한 디버깅 능력을 기를 수 있었습니다.

</br>

___

### 🔭 [UE5 팀 프로젝트] 시뮬레이션 게임 (Overcooked! 2 모작)
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\Overcooked!2.gif">
</p>

* 🔗 [Youtube](https://youtu.be/zs3aQ8tSZ3E?si=R2VaHZ-xt10g0D2M)
* 🔗 [Github](https://github.com/kabu0330/UE_Overcooked2)

### 📋 프로젝트 정보
<details>
<summary><b>📖 상세 정보 펼치기</b></summary>

| 항목 | 내용 | 항목 | 내용 |
|:------|:-----|:-----|:-----|
| 🖥️ **플랫폼** | PC (Windows) | 🎮 **장르** | 시뮬레이션 |
| 👤 **개발 인원** | 6인 | 📅 **개발 기간** | 2025.02 ~ 2025.05 |
| 🛠️ **개발 도구** | C++, Unreal Engine 5 |
| 📝 **게임 소개** | 최대 4인의 플레이어가 함께 재료를 전달/손질/조합하여 </br> 제한 시간 내에 최대한 많은 요리를 제출하는 협동 게임|

### 💻 작업 내용

| 분류 | 상세 내용 |
|:-----|:----------|
| **컨텐츠** | 데이터 기반 요리 컨텐츠 개발 |
| **네트워크** | RPC, Replication |
| **레벨 디자인** | 타이틀/스테이지 레벨 디자인 |
| **기타** | Dynamic Material Instance |
	
</details>

### 🎯 작업 목표
**멀티플레이어 협업 게임 개발 및 팀 협업 경험**
- 네트워크 동기화 문제 해결 (재료 스폰, 상호작용 시스템, 머티리얼 동기화)
- Git 버전 관리 실전 경험 (Fork-PR 전략)
- 독립적인 기능 테스트 환경 구축

### 📊 핵심 성과
- ✅ SpawnActorDeferred로 Replicate 타이밍 문제 해결
- ✅ 테스트 레벨로 독립적 기능 검증 가능
- ✅ DataTable 기반 요리 시스템
- ⚠️ Fork-PR 방식의 시행착오 경험 → Stash 활용법을 나중에 알게 됨

> 💡 **배운 점**: 팀 프로젝트에서는 "**항상 내가 통제 가능한 상태에서 테스트할 수 없다**"는 현실을 체감했습니다. 테스트 레벨을 만들어 캐릭터 없이도 기능을 검증하고, Git 전략을 개선하며, 네트워크 동기화를 "필요한 것만" 하는 선택 기준을 익혔습니다

</br>

___

### 🔭 [DirectX 11] 2D 액션 게임 프로젝트 (Hollow Knight 모작)
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\HollowKnight.gif">
</p>

* 🔗 [Youtube](https://youtu.be/vi6KnUeedrs?si=nJsI59Pi36cGy-Rn)
* 🔗 [Github](https://github.com/kabu0330/DX_HollowKnight2)

### 📋 프로젝트 정보
<details>
<summary><b>📖 상세 정보 펼치기</b></summary>

| 항목 | 내용 | 항목 | 내용 |
|:------|:-----|:-----|:-----|
| 🖥️ **플랫폼** | PC (Windows) | 🎮 **장르** | 액션, 메트로베니아 |
| 👤 **개발 인원** | 1인 | 📅 **개발 기간** | 2024.11 ~ 2025.02 |
| 🛠️ **개발 도구** | C++|
| 📝 **게임 소개** | 액션 기반 전투 게임|

### 💻 작업 내용

| 분류 | 상세 내용 |
|:-----|:----------|
| **컨텐츠** | 캐릭터, 몬스터, 맵, 이펙트 및 스킬, UI |
| **기타** | FSM, 멀티 스레드 로딩 |

</details>

### 🎯 작업 목표
**상용 엔진 프레임워크 이해 및 그래픽 프로그래밍 기초 습득**
- 게임 엔진의 구조 분석 및 활용
- Actor-Component 패턴 기반 게임 제작
- 이벤트 기반 상태 관리(FSM Component)

### 📊 핵심 성과
- ✅ UE5 프레임워크 구조 이해 (Engine Core, Level, GameMode, Actor, Component)
- ✅ DirectX 11 렌더링 파이프라인 흐름 이해
- ✅ 상속 기반 기능 구현(AEffect, ASkill, AParticle, AKnightSkill, AMonsterSkill)
- ✅ 컴포넌트 기반 기능 구현(UFSMStateComponent, UTimeEventComponent, UCollision, USpriteRenderer)
- ✅ 멀티스레드 비동기 리소스 로딩 구현 (초기 실행 시간 단축)

> 💡 **배운 점**: 엔진을 분석하며 **UE5의 설계 철학**을 이해하게 되었습니다. "왜 Actor와 Component를 분리하는가", "왜 Tick이 필요한가" 같은 질문에 답하며, UE5로 돌아왔을 때 단순히 "사용"하는 것이 아니라 "이해하고 활용"할 수 있게 되었습니다.

</br>

___

### 🔭 [Win API] 슈팅 게임 프로젝트(The Binding of Isaac 모작)
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\Isaac.webp">
</p>

* 🔗 [Youtube](https://youtu.be/Uf7M80sdum0?si=vpmTN5Q4YahdKVrY)
* 🔗 [Github](https://github.com/kabu0330/WinAPI)

### 📋 프로젝트 정보
<details>
<summary><b>📖 상세 정보 펼치기</b></summary>

| 항목 | 내용 | 항목 | 내용 |
|:------|:-----|:-----|:-----|
| 🖥️ **플랫폼** | PC (Windows) | 🎮 **장르** | 슈팅 |
| 👤 **개발 인원** | 1인 | 📅 **개발 기간** | 2024.07 ~ 2024.11 |
| 🛠️ **개발 도구** | C++|
| 📝 **게임 소개** | 아이템을 수집하고 조합하며 슈팅 게임 |

### 💻 작업 내용

| 분류 | 상세 내용 |
|:-----|:----------|
| **컨텐츠** | 캐릭터, 몬스터, 맵, 이펙트 및 스킬, UI |

</details>

### 🎯 작업 목표
**게임을 제작하는 기본 구조 학습**
- 상속 구조를 활용한 메모리 관리
- Vector, Sin, Cos 등 게임 제작에 필요한 수학 활용


### 📊 핵심 성과
- ✅ Windows에서 게임 엔진을 구동하는 원리 이해(WinProc, PeekMessage, HDC, Bitmap 등)
- ✅ 상속 구조와 RTTI의 활용을 통한 기능 구현
- ✅ 자료구조(vector, list, map)를 활용한 게임 제작 기초 이해

> 💡 **배운 점**: 어떻게 프로그램이 운영체제에서 동작하는지에 대한 밑그림을 그릴 수 있었습니다. 게임을 직접 제작해보며 물리 세계를 구현하는데 수학이 어떻게 쓰이는지 이해할 수 있게 되었습니다.

</br>

___

### 2. 📑 주요 구현 내용 
### 2-1. 상태 관리 시스템

### [DirectX 11] ```Enum```의 한계 → ```FSM Component```
### 🎮 구현 목표 
**복잡해지는 상태 관리를 체계적으로 개선하고, 유지보수성과 확장성을 높이기**

WinAPI 프로젝트에서 ```Enum``` 기반 상태 관리의 한계를 직접 겪으며, DirectX 프로젝트에서는 FSM을 독립적인 Component로 분리하여 상태 전환 로직을 체계화하고자 했습니다.

</br>

### 🚨 문제 상황
**WinAPI 프로젝트: Enum + Switch 문의 한계**

**핵심 문제점:**
1. **복합 상태 표현 불가**: 
   "공격+무적" 같은 상태는 bool 변수 추가 필요
2. **조건문 과다**: 
   매 함수마다 `if (IsHit) if (Invincibility) if (IsDead)` 반복
3. **상태 전환 분산**: 
   여러 곳에서 `BodyState = LowerState::IDLE` 직접 변경
4. **디버깅 어려움**: 
   어디서 상태를 바꿨는지 추적 힘듦

상태를 추가하기도 어려울 뿐만 아니라 관리도 어려웠고, 애니메이션이 종료되는 시점 또는 입력이 끝나는 시점을 맞춰가며 동작 실행 중 다른 동작이 실행하거나 애니메이션이 재생되지 않도록 일일이 신경 써야 했습니다.

</br>

### 💭 해결 방안 고민  
**상태만 처리하는 별도의 클래스가 있다면 어떨까?**

핵심 아이디어:
- 상태가 바뀌면 애니메이션도 자동 변경
- 각 상태별로 독립적인 함수에서 로직 관리
- Tick에서 모든 상태 검사 → FSM이 현재 상태만 실행

이렇게 되면 Tick에서 모든 상태를 검사하던 방식에서 벗어나, **상태에 맞는 함수에서 변경 가능한 상태를 제한**할 수 있게 되므로 훨씬 효율적일 것이라고 생각했습니다.

```cpp
class UFSMStateManager
{
public:
	class FSMState
	{
	public:
        /** 최초 1회 실행 */
		std::function<void()> StartFunction = nullptr;

        /** 매 프레임 실행 */
		std::function<void(float)> UpdateFunction = nullptr;

        /** 상태 종료 시 실행 */
		std::function<void()> EndFunction = nullptr;
	};

    //...
private:
	FSMState* CurState = nullptr;
	FSMState* PrevState = nullptr;
	std::map<int, FSMState> States;
}
```
</br>

FSM을 아래와 같이 활용했습니다. 

```cpp
void AKnight::SetFSM()
{
	//            상태                Update          애니메이션
	CreateState(EKnightState::IDLE, &AKnight::SetIdle, "Idle");
	CreateState(EKnightState::RUN, &AKnight::SetRun, "Run");
}

void AKnight::CreateState(EKnightState _State, StateCallback _Callback, std::string_view _AnimationName)
{
	FSM.CreateState(_State, std::bind(_Callback, this, std::placeholders::_1),
		[this, _AnimationName]()
		{
			std::string AnimationName = _AnimationName.data();
			BodyRenderer->ChangeAnimation(AnimationName);
		});
}
```

```cpp
// 각 상태는 독립적인 함수
void AKnight::SetIdle(float _DeltaTime)
{
    ActivateGravity(); // 중력 체크
    RecoveryIdle(); // Idle 상태 초기화 함수
    
    // 입력에 따른 상태 전환
    if (UEngineInput::IsPress(VK_LEFT) || 
        UEngineInput::IsPress(VK_RIGHT))
    {
        FSM.ChangeState(EKnightState::IDLE_TO_RUN);
        return;
    }
   // ...
}
```
**장점**
- Switch 문 없이 상태 등록 가능
- 애니메이션 자동 연결
- 각 상태가 독립적인 함수로 분리됨

</br>

### 🔧 한계
**StartFunction 활용의 한계**

```StartFunction```이 단일 함수만 받아서 애니메이션 재생에만 사용하게 되었습니다. </br>
프로젝트 종료 후 복기하며 ```StartFunction```을 vector로 만들었으면 "상태가 바뀌면 초기화 되어야 할 변수들도 ```StartFunction```에서 처리했더라면 초기화 로직과 Tick 로직을 분리하고 더 간결했을 텐데"하는 생각이 들었습니다.

```cpp
// 실제 구현 - StartFunction 1개만
void AKnight::SetFocus(float _DeltaTime)
{
    // ❌ 매 프레임 체크해야 함
    bIsFocusEffect = false;      // 초기화
    bIsFocusEndEffect = false;   // 초기화
    
    // 실제 로직
    if (UEngineInput::IsUp('A'))
    {
        ChangeNextState(EKnightState::IDLE);
    }
}
```

**이렇게 했다면:**
- 애니메이션 재생
- 플래그 초기화
- 사운드 재생
- 이펙트 스폰

```cpp
// 이상적인 방식 (구현 못함)
CreateState(EKnightState::FOCUS)
    .AddStart([]() { 
        BodyRenderer->ChangeAnimation("Focus"); 
    })
    .AddStart([]() { 
        bIsFocusEffect = false;      // 최초 1회만
        bIsFocusEndEffect = false;   // 최초 1회만
    })
    .AddStart([]() { 
        Sound.Play("focus.wav"); 
    })
    .SetUpdate(&AKnight::SetFocus);  // 로직만 집중
```


</br>

### ✅ 결과 
**개선 효과:**

| 항목 | WinAPI (Before) | DirectX (After) |
|:-----|:---------------|:---------------|
| **상태 관리** | Switch 문 직접 | FSM Component |
| **상태 추가** | 어려움 | 쉬움 (`CreateState` 1줄) |
| **디버깅** | 전체 검색 필요 | `FSM.ChangeState` 검색 |
| **가독성** | ⭐ | ⭐⭐⭐ |

</br>

___

### [UE5 액션] 상태 관리: StateComponent와 ```GameplayTag```

### 🎮 구현 목표 
**복합 상태를 bool 변수 없이 직관적으로 표현하고, 상태 검사를 체계적으로 관리하기**

UE5 프로젝트에서는 GameplayTag로 간결하게 로직을 구현하고자 했습니다.

</br>

### 🚨 문제 상황
**단일 태그로는 복잡한 전투 로직을 표현하는데 한계가 있다**

처음에는 ```GameplayTag``` 단일로 상태 관리(```CurrentState```)를 시도했습니다. </br>
그러나 전투 로직의 복잡도가 증가하면서 "공격 중 피격"과 같은 상황이 문제가 되었습니다.

**예를 들어:**
| 상태 | 대미지 | 일반 공격 | 상태이상 공격 | 잡기 공격 |
|:---:|:---:|:---:|:---:|:---:|
| **일반** | O | 공격 중단<br>+ 피격 재생 | 공격 중단<br>+ 피격 재생 | 공격 중단<br>+ 피격 재생 |
| **경직 면역** | O | **공격 유지** | 공격 중단<br>+ 피격 재생 | 공격 중단<br>+ 피격 재생 |
| **슈퍼 아머** | O | **공격 유지** | **공격 유지** | **공격 유지** |
| **무적** | X | **공격 유지** | **공격 유지** | **공격 유지** |


이런 복합적인 상황을 `CurrentState` 하나로 처리하는데 한계가 있었습니다.

**예를 들어**
- 태그를 여러 개 사용할 수 있으면
  * Character.State.Attacking
  * Character.State.SuperArmour
  * Character.State.Hit
  * "캐릭터가 공격 중이고, 슈퍼아머 상태인데 피격됐구나!"

  </br>

- 태그를 하나만 써야 한다면
  * Charater.State.Attacking.Condition.HitIgnore
  * "캐릭터가 공격 중일 때, 피격은 무시한다." ← 덜 직관적이고 조건이 늘어날수록 태그 수도 급격히 증가

</br>

### 💭 해결 방안 고민  
**"상태를 여러 개 동시에 가질 수 있다면?"**

게임플레이 태그의 계층 구조를 활용하는 방법도 고민했으나, **GameplayTag Container**로 
여러 상태(`ActiveGameplayTags`)를 가지고 이를 검사하는 방식이 더 유연할 것이라고 판단했습니다.

**핵심 아이디어:**
- 상태를 **태그(문자열)**로 표현
- Container에 **여러 태그를 동시에 보관**
- "이 태그를 포함하고 있는가?" 쿼리로 상태 검사

```cpp
// StateComponent.h - Container로 관리
class UStateComponent
{
    FGameplayTagContainer ActiveGameplayTags; // 현재 활성 상태들
    
    void AddGameplayTag(const FGameplayTag& Tag);
    bool IsActiveGameplayTag(const FGameplayTag& Tag);
    bool IsAnyActiveGameplayTags(const FGameplayTagContainer& Tags);
};
```

</br>

### 🔧 활용
특정 동작을 실행하기 위한 상태 검사
```cpp
bool ASoulCharacterBase::CanPerformAttack(FGameplayTag& AttackTypeTag, const bool bHitCanceled, const bool bPairedAnimation)
{
	// 공격을 수행할 수 없는 상태를 정의
	FGameplayTagContainer CheckTags;
	CheckTags.AddTag(SoulGameplayTag::Character_State_Rolling);
	CheckTags.AddTag(SoulGameplayTag::Character_State_GeneralAction);
	CheckTags.AddTag(SoulGameplayTag::Character_State_Blocking);
	CheckTags.AddTag(SoulGameplayTag::Character_State_Stunned);
	CheckTags.AddTag(SoulGameplayTag::Character_State_DrinkingPotion);
	CheckTags.AddTag(SoulGameplayTag::Character_State_Down);
	CheckTags.AddTag(SoulGameplayTag::Character_State_Interaction);
	CheckTags.AddTag(SoulGameplayTag::Character_State_Attacking_Recovery);

    return StateComponent->IsAnyActiveGameplayTags(CheckTags) == false && // 태그 검사
		CombatComponent->IsCombatEnabled() == true &&
		AttributeComponent->CheckHasEnoughStamina(StaminaCost) == true;
}
```

**이렇게 하면:**
- "공격 중 + 경직 면역" = `Attacking` + `Poise` 두 태그 동시 보유
- "피격 시 경직 면역인가?" = Container에 `Poise` 태그 있는지 검사
- 복잡한 조합 = 필요한 태그들만 추가/제거

</br>

디버깅
```cpp
// StateComponent.cpp - Tick에서 실시간 확인
void UStateComponent::TickComponent(float DeltaTime, ...)
{
    if (GetOwner() != GetWorld()->GetFirstPlayerController()->GetPawn()) 
        return;
    
    uint64 Index = 1000;
    GEngine->AddOnScreenDebugMessage(
        Index++, 10.f, FColor::Cyan, 
        TEXT("Active Gameplay Tags : ")
    );
    
    // 현재 활성화된 모든 태그 출력
    for (const FGameplayTag& GameplayTag : ActiveGameplayTags)
    {
        GEngine->AddOnScreenDebugMessage(
            Index++, 0.03f, FColor::Cyan, 
            GameplayTag.ToString()
        );
    }
}
```
**효과:**
- 플레이 중 현재 상태 실시간 확인 가능
- "왜 공격이 안 나가지?" → 화면 보고 `Character.State.Attacking` 태그 발견 → 태그 제거 로직 검사
- 복합 상태 디버깅이 직관적으로 변함

</br>

### ✅ 결과 
**개선 효과:**

| 항목 | DirectX (Before) | UE5 (After) |
|:-----|:----------------|:------------|
| **복합 상태** | bool 변수 여러 개 사용 | ```AddTag()``` |
| **상태 검사** | `if (!A && !B && C)` | `HasTagExact()` |
| **디버깅** | 변수 일일이 확인 | Container 출력 |
| **확장성** | bool 계속 추가 | 태그만 정의 |
| **가독성** | ⭐⭐ | ⭐⭐⭐⭐ |


</br>

___

### [UE5 액션] 애니메이션 라이프 사이클 기반 비동기 상태 관리

### 🎮 구현 목표 

전투 중 **입력으로 스킬을 캔슬**하거나 **피격으로 몽타주가 중단**되는 등, 몽타주가 끝까지 재생되지 않는 상황에서도 캐릭터 상태가 정상적으로 복구되는 전투 시스템을 구현하고자 했습니다.

</br>

### 🚨 문제 상황
**몽타주가 중단되면 Gameplay Tag가 제거되지 않는 현상 발생**

기존 구조에서는 공격/피격 시작 시 상태 태그를 추가하지만, 종료 시 태그 제거는 ```AnimNotify```에 의존했습니다.

**AnimNotify의 치명적인 한계:**
- ❌ **몽타주가 중단되면** 해당 프레임의 Notify가 **호출되지 않음**
- ❌ **블렌드 아웃** 발생 시 몽타주 끝부분 Notify가 **누락될 위험**

즉, 몽타주가 **끝까지 재생되고 블렌드 없이 종료**된다는 보장이 있어야만 AnimNotify로 상태 관리가 가능합니다. 

**실제 발생한 문제:**
- 공격 중 회피 → `TAG_Character_State_Attacking` 미제거 → 캐릭터 영구 이동 불가, 공격 입력 무시
- 피격으로 공격 중단 → `TAG_Character_State_Attacking` 미제거 → 캐릭터 영구 이동 불가, 공격 입력 무시

</br>

### 💭 해결 방법
**"태그 추가를 호출 로직에서 했으면, 제거도 호출 로직에서 하면 되지 않을까?"**

핵심은 **몽타주 종료 시점에 무조건 호출되는 콜백**을 찾는 것이었습니다.

이 때 알게된 것이 ```AnimInstance```에 있는 ```FOnMontageEndedDelegate```였습니다. 몽타주가 재생되고나면 어떤 이유에서든 몽타주가 종료될 때 호출을 보장해줍니다. 심지어 두 번째 매개변수로 중단 여부까지 확인할 수 있으니 정상적으로 재생이 끝났을 때와 중단되었을 때의 로직 처리를 구분하여 로직을 처리하기도 수월했습니다.

**고려한 방법들:**
1. **Timer 사용** → 몽타주 길이만큼 타이머 설정 후 태그 제거
   - 리스크: 몽타주가 일찍 중단되어도 타이머는 계속 진행
   - 판단: 근본적 해결 아님 ❌

2. **FOnMontageEnded Delegate 활용** ✅
   - 몽타주가 **어떤 이유로든 종료**되면 무조건 호출
   - `bInterrupted` 파라미터로 정상 종료/중단 여부 구분 가능
   - UE5가 제공하는 안전한 방법

</br>

### 🔧 구현

피격 시스템에 먼저 적용하여 검증:
```cpp
void ASoulCharacterBase::HitReaction(AActor* Attacker, UDamageType* DamageType, 
            const FVector& HitDirection)
{
    // ...
    FOnMontageEnded OnMontageEnded;
	OnMontageEnded.BindUObject(this, &ThisClass::RecoveryHitReaction);
    AnimInstance->Montage_Play(HitReactAnimation);
	AnimInstance->Montage_SetEndDelegate(OnMontageEnded, HitReactAnimation);
}
```

```cpp
void ASoulCharacterBase::RecoveryHitReaction(UAnimMontage* AnimMontage, bool bInterrupted)
{
	check(StateComponent);

	RemoveState(SoulGameplayTag::Character_State_Hit);
	RemoveState(SoulGameplayTag::Character_State_Down);
	RemoveState(SoulGameplayTag::Character_State_Attacking);
	RemoveState(SoulGameplayTag::Character_State_Attacking_Recovery);
    
	StateComponent->ToggleMovementInput(true);
	AttributeComponent->ToggleStaminaRegeneration(true, 0.5f);
}
```

**검증 결과:**
- ✅ 피격 모션 중 공격받아 중단 → 상태 정상 복구
- ✅ 피격 모션 정상 종료 → 상태 정상 복구
- ✅ 블렌드 아웃 발생 → Delegate 정상 호출

모든 태그 제거 로직을 ```FOnMontageEndedDelegate```를 통하도록 변경했습니다.

</br>

### ✅ 결과 
**안정적인 상태 관리 시스템 구축**

✅ **모든 종료 케이스 대응**
- 정상 종료, 입력 캔슬, 피격 중단, 블렌드 아웃 모두 처리

✅ **상태 불일치 문제 완전 해결**
- 공격 캔슬 후 이동 불가 버그 소멸
- 스태미나 재생 미복구 현상 해결

✅ **확장 가능한 구조**
- `bInterrupted`로 종료 상황별 로직 분기 가능
- 새로운 몽타주 추가 시 동일 패턴 적용

`AnimNotify`는 **특정 타이밍의 이벤트**(이펙트 재생, 사운드 등)에 적합하지만, **상태 초기화**처럼 반드시 실행되어야 하는 로직은 **Delegate로 보장**해야 합니다. 

</br>

___

### 2-2. 컨탠츠 구현

### [DirectX 11] 다중 좌표계 간 위치 동기화
### 🎮 구현 목표

게임 엔진에서 BMP 픽셀 충돌 맵(윈도우 계층)과 액터 Transform(엔진 계층) 간의 좌표계 불일치 문제를 해결하여 정확한 픽셀 기반 지형 충돌을 구현합니다.

</br>

### 🚨 문제 상황

#### 엔진 계층 구조로 인한 좌표계 불일치

게임 엔진을 Windows에 종속된 Platform 계층과 게임 컨텐츠 제작에 필요한 기능을 지원하는 Core 계층으로 분리한 것이 문제의 시작이었습니다.

```
[윈도우 계층 - EnginePlatform]  
- BMP 이미지 (픽셀 충돌용)
- UEngineWinImage (Transform 없음)
- 스크린 좌표 시스템

[엔진 계층 - EngineCore]
- PNG 텍스처 (렌더링용)
- Transform (월드 좌표)
- 데카르트 좌표 시스템
```

**문제의 핵심:**
- BMP 파일은 윈도우 계층에 속하며 Transform 정보를 가질 수 없음
- 액터는 엔진 계층의 월드 좌표로 움직이지만, 픽셀 충돌은 윈도우 계층의 BMP를 참조
- 두 계층의 좌표 기준점이 다름

<br>

#### 대안

**방법 1: 엔진 구조 변경**
```cpp
// UEngineWinImage에 Transform 추가?
class UEngineWinImage
{
    FTransform Transform; // ❌ 계층 규칙 위반
};
```
- 계층 분리 원칙 위반 (Platform 계층이 Core 계층 의존)
- 엔진 전체 구조 수정 필요

**방법 2: WinImage를 엔진 계층으로 이동**
```cpp
// UEngineWinImage를 EngineCore로?
#include <EngineCore/EngineWinImage.h> // ❌ 의존성 역전
```

</br>

### 💭 해결 방안

#### 핵심 아이디어: 픽셀 충돌 검사는 데카르트 좌표계에서 윈도우 좌표계로 변환

현재 배경 이미지(png) 파일의 좌상단(Left Top) 좌표를 스크린 좌표의 원점(0, 0)으로 변환하고, y축을 반전시켜 액터의 픽셀 충돌 검사는 스크린 좌표계 기준으로 변환합니다.

플레이어가 속하지 않은 맵 리소스는 모두 비활성화시켜 항상 플레이어가 입장한 맵에서만 좌표계를 변환한 충돌 검사를 수행합니다.

```
월드 좌표 (액터) → BMP 로컬 좌표 → 픽셀 색상 검사
```

**설계 원칙:**
1. BMP 파일은 변경하지 않는다 (윈도우 계층 유지)
2. 액터 좌표를 BMP의 좌표계로 변환한다
3. 맵이 바뀌면 변환 기준점만 갱신한다

#### Room 기반 좌표 변환 시스템

```cpp
// Room.h - 좌표 변환의 중심
class ARoom : public AActor
{
private:
    UEngineWinImage PixelCollisionImage;  // BMP 충돌 맵
    FVector LeftTopPos;                    // BMP의 좌표 기준점 (월드 좌표)
    FVector Size;                          // 방 크기
};
```

**Room이 좌표 변환을 담당하는 이유:**
- Room은 엔진 계층에 속하므로 Transform 사용 가능
- 각 Room은 독립적인 BMP 충돌 맵 보유
- Room 전환 시 자동으로 좌표계 변환 기준점 갱신

#### 좌표 변환 구현

```cpp
// Room.cpp
FVector ARoom::GetPixelCollisionPoint(AActor* _Actor, FVector _Offset)
{
    float DeltaTime = UEngineCore::GetDeltaTime();
    
    // 액터의 월드 좌표 획득
    FVector CollisionPos = Knight->GetPixelCollision()->GetWorldLocation();
    FVector GravityForce = Knight->GetGravityForce();
    
    // 1단계: 월드 좌표 → Room 로컬 좌표
    CollisionPos -= LeftTopPos;
    
    // 2단계: 다음 프레임 예측 위치 계산
    FVector NextPos = GravityForce * DeltaTime;
    FVector CollisionPoint = { 
        CollisionPos.X + NextPos.X + _Offset.X, 
        CollisionPos.Y + NextPos.Y + _Offset.Y 
    };
    
    return CollisionPoint;
}
```

**변환 과정:**

```
[월드 좌표]
Knight: (9000, -6000)
Room LeftTopPos: (6150, -3550)

[1단계] 월드 → Room 로컬
CollisionPos = (9000, -6000) - (6150, -3550)
             = (2850, -2450)

[2단계] BMP 좌표 (Y축 반전)
BMP GetColor({ 2850, 2450 })  // Y축 부호 반전
```

</br>

#### Y축 좌표계 통일

```cpp
// Room.cpp
bool ARoom::IsOnGround(FVector _Pos)
{
    FVector CollisionPoint = _Pos;
    CollisionPoint.RoundVector();
    
    // Y축 반전: 엔진(Y Down) → BMP(Y Up)
    UColor CollisionColor = PixelCollisionImage.GetColor(
        { CollisionPoint.X, -CollisionPoint.Y }
    );
    
    return (CollisionColor == UColor::BLACK);
}
```

**좌표계 차이:**

| 시스템 | 원점 | Y축 방향 |
|--------|------|----------|
| 엔진 월드 좌표 | 임의 | 아래가 음수 |
| BMP 좌표 | 좌상단 | 아래가 양수 |

</br>

### 🔧 구현 세부사항

#### Room 초기화 시 좌표 기준점 설정

```cpp
// RoomManager.cpp - 맵 생성
Crossroads1->SetRoomLocation({ 6150, -3550 });
```

```cpp
// Room.cpp
void ARoom::SetRoomLocation(FVector _Pos)
{
    float ZOrder = static_cast<float>(EZOrder::BACKGROUND);
    SetActorLocation({ GetActorLocation().X + _Pos.X, 
                       GetActorLocation().Y + _Pos.Y, 
                       ZOrder });
    LeftTopPos = _Pos;  // BMP 좌표 변환 기준점 저장
}
```

#### 픽셀 충돌 검사 - 중력

```cpp
// Room.cpp
void ARoom::CheckPixelCollisionWithGravity(AActor* _Actor, FVector _Offset)
{
    float DeltaTime = UEngineCore::GetDeltaTime();
    FVector TwoPixelUp = FVector::UP * 2.0f;
    
    // 현재 위치의 픽셀 색상 검사
    FVector CollisionPoint = GetPixelCollisionPoint(_Actor, _Offset);
    FVector CollisionPoint2PixelUp = GetPixelCollisionPoint(_Actor, _Offset + TwoPixelUp);
    
    if (true == IsOnGround(CollisionPoint))
    {
        Knight->SetOnGround(true);
        
        // 지면에 박히지 않도록 위로 조정
        while (true == IsOnGround(CollisionPoint2PixelUp))
        {
            Knight->AddRelativeLocation(TwoPixelUp);
            CollisionPoint2PixelUp = GetPixelCollisionPoint(_Actor, _Offset + TwoPixelUp);
        }
    }
    else
    {
        Knight->SetOnGround(false);
    }
    
    Force(_Actor, DeltaTime);
}
```

**동작 원리:**
1. 액터의 월드 좌표를 BMP 로컬 좌표로 변환
2. 해당 좌표의 픽셀 색상을 `GetColor()`로 검사
3. 검은색(지면)이면 중력 중단, 아니면 중력 적용

</br>

#### 픽셀 충돌 검사 - 벽

```cpp
// Room.cpp
void ARoom::CheckPixelCollisionWithWall(AActor* _Actor, float _Speed, bool _Left, FVector _Offset)
{
    FVector CollisionPos = Knight->GetPixelCollision()->GetWorldLocation();
    FVector CollisionHalfScale = Knight->GetPixelCollision()->GetWorldScale3D().Half();
    
    float DeltaTime = UEngineCore::GetDeltaTime();
    float NextPos = _Speed * DeltaTime;
    
    // 월드 좌표 → Room 로컬 좌표
    CollisionPos -= LeftTopPos;
    
    FVector CollisionPoint = { CollisionPos.X + NextPos, CollisionPos.Y + 10.0f };
    
    // 좌우 방향에 따라 충돌 체크 위치 조정
    if (true == _Left)
    {
        CollisionPoint.X -= CollisionHalfScale.X;
    }
    else
    {
        CollisionPoint.X += CollisionHalfScale.X;
    }
    
    CollisionPoint.RoundVector();
    
    // Y축 반전하여 BMP 좌표로 검사
    UColor CollisionColor = PixelCollisionImage.GetColor(
        { CollisionPoint.X, -CollisionPoint.Y }
    );
    
    // 노란색(벽) 또는 검은색(지면)이면 벽으로 인식
    if (CollisionColor == UColor::YELLOW || CollisionColor == UColor::BLACK)
    {
        Knight->SetWallHere(true);
    }
    else
    {
        Knight->SetWallHere(false);
    }
}
```

**색상 기반 충돌 판정:**

| 픽셀 색상 | 의미 | 충돌 처리 |
|----------|------|----------|
| BLACK | 지면 | 중력 중단, 벽 충돌 |
| YELLOW | 벽 | 벽 충돌 |
| RED | 천장 | 천장 충돌 |
| WHITE | 빈 공간 | 통과 가능 |

</br>

#### Actor에서 픽셀 충돌 활성화

```cpp
// Knight.cpp 
void AKnight::ActivatePixelCollsion()
{
    if (true == NoneGravity)  // 디버그 모드
    {
        return;
    }
    
    ARoom* Room = ARoom::GetCurRoom();
    if (nullptr != Room)
    {
        // Room에게 좌표 변환 및 충돌 검사 위임
        Room->CheckPixelCollisionWithWall(this, Stat.GetVelocity(), bIsLeft, FVector::ZERO);
        Room->CheckPixelCollisionWithCeil(this, BodyRenderer.get(), Stat.GetVelocity(), bIsLeft, FVector::ZERO);
    }
}
```

```cpp
// Knight.cpp
void AKnight::Tick(float _DeltaTime)
{
    AActor::Tick(_DeltaTime);
    
    ActivatePixelCollsion();  // 매 프레임 픽셀 충돌 검사
    
    // ...
}
```

</br>

### ✅ 결과

#### 계층 분리 원칙 준수

```
[EnginePlatform]
└─ UEngineWinImage
   └─ GetColor() 만 제공

[EngineCore]  
└─ ARoom (좌표 변환 담당)
   ├─ LeftTopPos (기준점)
   └─ GetPixelCollisionPoint() (좌표 변환)
```

- UEngineWinImage는 순수하게 픽셀 색상만 반환
- ARoom이 모든 좌표 변환 로직 관리
- 계층 간 의존성 규칙 유지

</br>

#### 맵 전환 시 자동 좌표계 갱신

```cpp
// Door를 통한 Room 전환
void ADoor::WarpRoom()
{
    ARoom::SetCurRoom(TargetRoom);  // 현재 Room 변경
    Knight->SetActorLocation(TargetPos);
    
    // 새로운 Room의 LeftTopPos를 기준으로 자동 변환
    // 추가 코드 불필요 - Room이 알아서 처리
}
```

- Room이 바뀌면 해당 Room의 LeftTopPos 자동 적용
- 개발자는 월드 좌표만 신경 쓰면 됨
- 좌표 변환은 Room이 투명하게 처리

</br>

#### 정확한 지형 충돌 구현

**변환 전 (좌표 불일치):**
```
액터 월드 좌표: (9000, -6000)
BMP 검사 좌표: (9000, 6000) ❌ 엉뚱한 위치
```

**변환 후 (정확한 매핑):**
```
액터 월드 좌표: (9000, -6000)
Room LeftTopPos: (6150, -3550)
BMP 검사 좌표: (2850, 2450) ✅ 정확한 위치
```

</br>

#### 확장성 확보

```cpp
// 새로운 Room 추가 시
std::shared_ptr<ARoom> NewRoom = CreateRoom("NewRoom", "NewRoom_back.png", "NewRoom_pixel.bmp", { 5000, 3000 });
NewRoom->SetRoomLocation({ 20000, -10000 });

// 좌표 변환 로직은 자동으로 동작
// 추가 코드 작성 불필요
```

</br>

### [UE5 액션] 유연한 콤보 시스템: 이벤트 기반 Perfect/Mercy 구간을 통한 공격 후딜레이 캔슬 및 콤보 연계
### 🎮 구현 목표 
**자연스러운 콤보 시스템 구현**
- 공격 중 입력이 들어오면 **후딜레이를 캔슬**하고 즉시 다음 콤보로 연계
- 공격 종료 후에도 **일정 시간 내 입력** 시 다음 콤보 진행
- 입력 타이밍에 따라 **정확한 프레임에서 콤보 전환**

</br>

### 🚨 기존 방식
**Timer 기반 콤보의 한계: 뚝뚝 끊기는 연계**

기존 시스템은 공격 몽타주 재생 시간을 기준으로 Timer를 설정하고, Timer 종료 시점에 입력 여부를 확인하여 다음 콤보를 재생했습니다.
```cpp
void ACharacter::Attack()
{
    // 몽타주 전체 길이로 타이머 설정
    float MontageLength = AttackMontage->GetPlayLength();
    GetWorldTimerManager().SetTimer(ComboCheckTimer, this, 
        &ThisClass::CheckComboInput, MontageLength, false);
    
    PlayAnimMontage(AttackMontage);
}

void ACharacter::CheckComboInput()
{
    if (bInputPressed)
    {
        PlayNextCombo();  // 타이머 종료 시점에만 체크
    }
}
```

**발생한 문제:**
- ❌ 콤보 전환 타이밍이 **몽타주 끝**으로 고정되어 부자연스러움
- ❌ 공격 **모션이 끝나기 전** 입력해도 타이머가 끝날 때까지 대기
- ❌ 후딜레이 캔슬이 불가능해 **액션감 저하**

**핵심 문제:** "입력을 언제 받았는가"와 "언제 다음 콤보로 넘어갈 수 있는가"를 분리할 수 없었습니다.

</br>

### 💭 해결 방안
**"입력 체크 타이밍을 구간으로 나눠 관리하고 싶다."**

Timer는 시간 기반이므로 애니메이션의 특정 구간을 정밀하게 제어하기 어렵습니다. 필요한 것은:

1. **입력 받을 수 있는 구간 정의** (공격 시작 ~ 후딜레이 전)
2. **해당 구간 내에서만 입력 체크**
3. **입력이 들어온 순간 바로 다음 콤보 전환 가능**

</br>

**AnimNotifyState의 발견:**

AnimNotify가 **단일 시점**에서만 호출되는 반면, **AnimNotifyState**는:
- `NotifyBegin`: 구간 시작 시점
- `NotifyTick`: 구간 내 매 프레임
- `NotifyEnd`: 구간 종료 시점

이 세 가지 콜백을 제공하여 **시간 구간을 정밀하게 제어**할 수 있습니다.

</br>

### 🔧 시행착오 
#### 1차 시도: AnimNotifyState로 입력 윈도우 구현

**핵심 아이디어:** 공격 모션이 절반 이상 진행된 시점부터 입력을 받을 수 있는 "콤보 윈도우"를 정의
```cpp
void UAnimNotifyState_ComboWindow::NotifyBegin(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation,
                                          float TotalDuration, const FAnimNotifyEventReference& EventReference)
{
	if (UCombatComponent* CombatComp = Character->GetCombatComponent())
	{
		CombatComp->EnableComboWindow();
	}
}

void UAnimNotifyState_ComboWindow::NotifyEnd(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation,
	const FAnimNotifyEventReference& EventReference)
{
	if (UCombatComponent* CombatComp = Character->GetCombatComponent())
	{
		CombatComp->DisableComboWindow();
	}
}
```

**좋은 점:**
- ✅ ComboWindow 내 입력 → 후딜레이 캔슬하고 즉시 다음 콤보
- ✅ 정확한 타이밍에 입력한 플레이어에게 빠른 전투감 제공


```cpp
void UCombatComponent::DisableComboWindow()
{
	bCanComboInput = false;
 
	// 애니메이션 재생 중에 다음 공격 입력이 들어왔다면 다음 애니메이션 재생 준비
	if (bSavedComboInput)
	{
		bSavedComboInput = false; 
		++ComboCounter;
		LOG_WARNING("Combo Window Closed : 입력 확인, 다음 콤보 실행");

        // 다음 콤보 재생
		DoAttack(LastAttackType); 
	}
}
```

**딜레마**

ComboWindow를 벗어나면 입력이 모두 무시되어 **콤보가 첫 번째로 초기화**됩니다.
```
플레이어 경험:
1. 1타 공격 → 2타 입력 (살짝 늦음) 
2. ComboWindow 놓침 → 후딜레이 진입
3. 후딜 중 다시 입력 
4. 콤보 초기화 → 1타부터 다시 시작 😡
```

**"타이밍 놓쳤으니 다시 처음부터" = 매우 불쾌한 경험**

조작감을 높이겠다는 의도로 후딜레이 캔슬이라는 혜택을 제공한 것은 좋았으나, 패널티(후딜레이 간 입력 불가/ 이동 불가)가 너무 강력했습니다.

</br>

#### 2차 시도: ComboWindow 범위 확장
**시도:** NotifyState의 범위를 후딜레이 구간까지 늘려보자

✅ 장점:
- 입력 허용 시간이 넉넉해져 콤보 성공률 ↑

❌ 치명적 단점:
```
플레이어 경험:
1. 1타 완료 → 후딜레이 진입
2. 후딜 중 2타 입력 (입력은 받아짐)
3. 그러나 NotifyEnd() 도달 전까지 대기 😤
4. 콤보 공격 진행이 느릿하게 느껴짐
```

**후딜레이를 경험하는 건 매한가지**입니다. Timer만 사용했을 때에 비해 두드러지는 개선감이 잘 느껴지지 않습니다.

**핵심 문제 인식:**
```
앞쪽으로 여유 주기 (공격 중) ✅ → 후딜 캔슬 = 쾌적함
뒤쪽으로 여유 주기 (후딜레이 중) ❌ → 후딜 대기 = 불쾌감
```
```AnimNotifyState```는 **구간의 끝에서 일괄 처리**하는 구조이므로, 후딜레이 구간까지 포함하면 결국 후딜을 다 봐야 합니다. 

</br>

#### 3차 개선: 이중 입력 체크
**구현 목표:**
1. **Perfect Timing 보상**: ComboWindow 내 입력 → 후딜 캔슬, 부드러운 연계
2. **패널티 부여**: ComboWindow 놓침 → 후딜레이 재생 (시간적 불이익)
3. **2차 기회 제공**: 그래도 후딜 중 입력 들어오면 → 콤보는 이어짐

<p align="center">
 <img alt="이미지" src="readme\ComboWindow.png">
</p>

**핵심 아이디어:** 
- **1차 윈도우 (ComboWindow)**: 후딜 캔슬 가능한 "Perfect 구간"
- **2차 윈도우 (Timer)**: 후딜은 보지만 콤보는 이어지는 "Mercy 구간"

```cpp
void UAnimNotify_AttackFinished::Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation,
                                        const FAnimNotifyEventReference& EventReference)
{
	if (UCombatComponent* CombatComp = Character->GetCombatComponent())
	{
		CombatComp->AttackFinished(ComboResetDelay);
	}
}
```
```cpp
void UCombatComponent::AttackFinished(const float ComboResetDelay)
{
	// ComboResetDelay 간 추가 콤보 입력 시간을 준 뒤 콤보 시퀀스 종료
    // 입력이 들어오면 ExecuteComboAttack에서 콤보 공격을 자동으로 처리. 타이머는 콤보 초기화만 지연
	GetWorld()->GetTimerManager().SetTimer(ComboResetTimerHandle, this, &UCombatComponent::ResetCombo, ComboResetDelay);
}
```
```cpp
void UCombatComponent::ExecuteComboAttack(const FGameplayTag& AttackTypeTag)
{
	if (false == CharacterBase->IsCurrentState(SoulGameplayTag::Character_State_Attacking))
	{
		// 애니메이션은 끝났지만, 콤보시퀀스 변수가 true인 시간에는 추가 입력 기회를 준다.
		if (bComboSequenceRunning == true && bCanComboInput == false)
		{
			++ComboCounter;
			LOG_WARNING("추가 공격 입력 기회 : Combo counter : %d", ComboCounter);
		}
		else // 첫 번째 공격
		{
			LOG(">>> 콤보 시퀀스 시작 <<<");
			ResetCombo();
			bComboSequenceRunning = true;
		}
		
        // 진짜 공격 로직 처리 함수
		DoAttack(AttackTypeTag);

		GetWorld()->GetTimerManager().ClearTimer(ComboResetTimerHandle);
	}
	// 아직 공격 애니메이션이 끝나지 않았는데 콤보 입력이 추가로 들어온 경우 : 최적의 타이밍
	else if (bCanComboInput) 
	{
		LOG_WARNING("Combo Hit!!!!");
		bSavedComboInput = true;
	}
}
```

**플레이어 경험 개선:**

| 시나리오 | 기존 (Timer만) | 개선 (이중 윈도우) |
|---------|---------------------|-------------------|
| Perfect 입력 |  후딜 재생 → 다음 콤보 😡  | 공격 끝 → **즉시 다음 콤보** ✅ |
| ComboWindow 놓침 | - | 후딜 재생 😡|
| 후딜 중 입력 | 후딜 재생 → 다음 콤보 😡 |**즉시 다음 콤보** ✅ |
| Timer 종료 후 | 1타로 되돌아감 | 1타로 되돌아감 |
```
개선된 플레이어 경험:
1. 콤보 공격 재생(1타)
2. ComboWindow 놓침 → 후딜 재생 (패널티)
3. 후딜 중 다시 입력
4. 후딜레이 중단 → 즉시 2타 공격 진행! ✅
```

</br>

### ✅ 결과 
**조작감을 챙긴 콤보 시스템**

✅ **Perfect Timing 보상 (ComboWindow)**
- 공격 모션 30% 이후 입력 → 후딜 캔슬
- 숙련된 플레이어에게 빠른 전투감 제공

✅ **Mercy Window (Extra Combo Input)**
- ComboWindow 놓쳐도 0.N초 추가 기회
- 후딜레이 패널티는 있지만 **콤보는 끊기지 않음** (핵심 개선!)

✅ **입력 타이밍별 차등 보상**
| 타이밍 | 조작감 | 전투 속도 | 콤보 유지 |
|--------|--------|----------|----------|
| Perfect | 후딜 없음 | 빠름 ⭐ | ✅ |
| Late | 후딜 재생 | 보통 ✅ | ✅ |
| Too Late | 콤보 끊김 | 느림 ❌ | ❌ |

</br>

___

### [UE5 액션] 루트 모션 기반 자연스러운 대시 구현  ```Motion Warping```

### 🎮 구현 목표 
액션 게임의 핵심인 **빠르고 역동적인 이동**을 구현하되, 애니메이션과 자연스럽게 어우러지는 대시 시스템을 만들고자 했습니다. 특히 적에게 빠르게 접근하는 "돌진형 스킬"의 자연스러운 연출이 목표였습니다.

</br>

### 🚨 문제 상황
대시를 구현하기 위해 세 가지 방법을 테스트했습니다.
- ```AddMovementInput()```의 Scale을 높이는 방법
- ```LaunchCharater()```를 사용하는 방법
- ```Tick()```에서 ```MaxWalkSpeed```를 조작하는 방법 

결국 세 가지 방법 다 제가 느끼는 결과물은 아래 이미지와 같습니다.

<p align="center">
 <img alt="이미지" src="readme\DNFDash.webp">
</p>

<p align="center">
 <img alt="이미지" src="readme\Howl.png">
</p>


세 가지 방법 모두 결과적으로:
- ❌ 캐릭터가 **순간이동하는 듯한 부자연스러운 느낌**
- ❌ **캐릭터가 미끄러지는 현상**
- ❌ 이동 거리와 애니메이션 거리의 **불일치로 인한 이질감**

'이동'과 '애니메이션'이 완전히 분리된 것이 문제의 핵심이었습니다.

</br>

### 💭 해결 방법
Youtube로 다른 사람들이 어떻게 대시를 구현했는지 보기 위해 자료조사를 하다가 우연히 언리얼 서밋을 보게 되었는데, 여기서 모션 워핑의 존재를 알게되었습니다.
<p align="center">
 <img alt="이미지" src="readme\Unreal.png">
</p>

[Youtube](https://youtu.be/nxzfJcwyj1Y?si=FSiQD8UPRUGWqXio)

영상을 보다 대시 시연 과정이 나오는 것을 보고 "아! 이거다!"


**Motion Warping의 핵심 개념:**

애니메이션을 **런타임에 동적으로 변형**하여 목표 지점까지 도달하게 만드는 기술입니다.
- 애니메이션이 원래 100cm 이동한다면 → 목표가 200cm 떨어져 있으면 애니메이션을 2배 늘림
- Root Motion을 유지하면서 거리를 조정하므로 **발이 땅에서 미끄러지지 않음**
- 이동 거리와 애니메이션이 **완벽하게 일치**

즉, 제가 찾던 **애니메이션과 이동을 하나로 묶는 방법**이었습니다.

</br>

### 🔧 구현

#### 1차 시도: Blueprint로 프로토타입 검증

본격적인 C++ 작업 전에 Motion Warping 플러그인을 활성화하고, 블루프린트로 빠르게 프로토타입을 만들어 개념을 검증했습니다.
영상을 참고하여 저에게 필요한 부분만 자료조사를 하며 블루프린트로 로직을 먼저 완성시켜나갔습니다.

<p align="center">
 <img alt="이미지" src="readme\BlueprintTest.png">
</p>

**검증 항목:**
- ✅ Motion Warping Component 동작 확인
- ✅ Warp Target 설정 방식 이해
- ✅ 애니메이션 에디터에서 Warp Point 설정 방법 습득

**결과:** "실제로 작동한다!"는 확신을 얻고 C++ 구현으로 전환


#### 2차 시도: C++ 구현

```cpp
void ASoulPlayerCharacter::MotionWarpingDashSlash()
{
	Super::MotionWarpingDashSlash();

	check(MotionWarpingComponent);
	LOG(">>> Motion Warping Dash Slash <<<")
	GetCharacterMovement()->SetMovementMode(EMovementMode::MOVE_Flying);
	FVector Start = MotionWarpArrowComponent->GetComponentLocation();
	FVector Forward = MotionWarpArrowComponent->GetForwardVector();
	FVector End = Start + (Forward * 2000.0f);

	FHitResult OutHit;
	TArray<AActor*> ActorToIgnore;
	ActorToIgnore.Add(this);
	
	EDrawDebugTrace::Type TraceType = EDrawDebugTrace::None;

	const bool bHit = UKismetSystemLibrary::LineTraceSingle(
		GetWorld(),
		Start,
		End,
		UEngineTypes::ConvertToTraceType(ECC_Visibility),
		false,
		ActorToIgnore,
		TraceType,
		OutHit,
		true
	);

	if (bHit)
	{
		MotionWarpingComponent->AddOrUpdateWarpTargetFromLocation(TEXT("DashSlash"), OutHit.Location);
	}
}
```

**구현 핵심:**
1. **Flying Mode**: 대시 중 지형의 영향을 받지 않도록 설정
2. **동적 목표 설정**: 레이캐스트로 탐지한 지점을 실시간으로 Warp Target에 적용
3. **Warp Point 이름 매칭**: 애니메이션 에디터에서 설정한 "DashSlash"와 코드의 이름 일치


대시 애니메이션의 **특정 구간**에 Motion Warping NotifyState를 추가:
- Warp Target Name: "DashSlash"
- Warp Translation: Forward 축 활성화
- Warp Rotation: 목표 방향으로 캐릭터 회전

이렇게 하면 **애니메이션 재생 중 실시간으로** Root Motion이 목표 지점까지 늘어납니다.

</br>

### ✅ 결과 

**애니메이션과 완벽하게 동기화된 역동적인 대시 완성**

**Launch Character(Before)**
<p align="center">
 <img alt="이미지" src="readme\DashBefore.webp">
</p>

미끄러짐이 있음

**Motion Warping(After)**
<p align="center">
 <img alt="이미지" src="readme\DashAfter.webp">
</p>

이동이 깔끔하게 떨어짐

</br>

___

### [UE5 액션] 데이터 에셋 기반 무기별 전투 스타일 관리

### 🎮 구현 목표 

**무기마다 다른 전투 경험**을 제공하되, **코드 수정 없이** 새로운 무기를 추가할 수 있는 확장 가능한 구조를 구축하고자 했습니다. </br>
특히 무기마다 다른 **콤보 체계, 스킬 구성, 공격력, 요구 스태미나** 등을 데이터로 분리하여, 언리얼 에디터에서 수정할 수 있는 환경을 목표로 했습니다.

</br>

### 🚨 문제 상황
**하드코딩의 한계: 무기 추가가 곧 코드 수정**

초기에는 무기 데이터를 캐릭터 클래스에 직접 하드코딩했습니다.
```cpp
// 초기 구조 - 모든 무기 정보를 캐릭터가 보유
void ACharacter::Attack()
{
    if (CurrentWeapon == EWeaponType::Sword)
    {
        PlayAnimMontage(SwordCombo[ComboIndex]);
    }
    else if (CurrentWeapon == EWeaponType::Axe)
    {
        PlayAnimMontage(AxeCombo[ComboIndex]);
    }
    // 무기가 추가될 때마다 else if 증가...
}
```

❌ **무기 추가 시 개발 사이클 증가**
```
새 무기 추가 프로세스:
1. C++ 코드에 무기 타입 Enum 추가
2. 애니메이션 배열 선언
3. 조건문 분기 추가
4. C++ 컴파일
5. 에디터 재시작
6. 테스트 → 수정 시 1번부터 반복
```

❌ **무기 간 차별화된 로직 구현 어려움**
- 검은 빠른 3타 콤보, 도끼는 느린 2타 강공격 같은 차이를 조건문으로만 구현
- 코드가 무기별 특수 케이스로 가득 차서 가독성 저하

❌ **기획자 의존도 증가**
- 밸런싱, 콤보 수 조정 같은 단순 작업도 프로그래머 필요

이와 관련한 작업을 C++ 코드가 아닌 **에디터에서 유연하게 처리**하고 싶었습니다.

</br>

### 💭 해결 방안 고민  
**"무기를 데이터로 분리하되, 단순 수치뿐만 아니라 행동까지 정의할 수는 없을까?"**

**Data Asset** ✅
   - Blueprint에서 무기별 **고유 로직 구현** 가능
   - 애니메이션, 수치, 조건을 **하나의 Asset에 캡슐화**
   - Primary Data Asset 사용 시 **비동기 로딩**으로 메모리 최적화


**고려사항:**
```
무기 = 데이터 집합체
- 무슨 공격인가? (AttackTypeTag)
- 어떤 애니메이션을 재생하는가? (Montages)
- 언제 재생하는가? (ConditionTags)
```

</br>

### 🔧 구현
#### 정말 필요한 데이터만 남기기

무기를 정의하기 위해 **최소한으로 필요한 데이터**만 추려내는 데 집중했습니다.

처음엔 "혹시 필요할까봐" 이것저것 넣다가, 실제 사용하지 않는 데이터가 쌓이는 걸 발견했습니다. 여러 시행착오 끝에 **정말 사용하는 다섯 가지**로 압축했습니다:

1. **공격/동작 타입** (AttackTypeTag)
2. **몽타주 배열** (Animations)
3. **실행 조건 태그** (ConditionTags)
4. **실행 조건 검사 범위** (ConditionCheckDistance)
5. **루트모션 스케일** (RootMotionScales)


```cpp
USTRUCT(BlueprintType)
struct FMontageGroup
{
	GENERATED_BODY()
public:
    // 이 그룹이 재생되기 위한 조건 태그
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	TArray<FGameplayTagContainer> ConditionTags;

    // 조건 체크 거리(예: 잡기 검사 최대 거리)
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	float ConditionCheckDistance = 300.f;

    // 무기마다 다른 이동 거리 보정
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	TArray<float> RootMotionScales;
	
    // 실제 재생할 애니메이션 배열
	UPROPERTY(EditAnywhere, BlueprintReadWrite)
	TArray<TObjectPtr<UAnimMontage>> Animations;
};
```

```cpp
UCLASS()
class SOUL_API UMontageActionData : public UPrimaryDataAsset
{
	GENERATED_BODY()

public:
    // Tag와 인덱스로 특정 몽타주 가져오기
	UAnimMontage* GetMontageForTag(const FGameplayTag& GroupTag, const int32 Index = 0) const;

    // 그룹 내 랜덤 선택 (몬스터)
	UAnimMontage* GetRandomMontageForTag(const FGameplayTag& GroupTag) const;
	
protected:
	UPROPERTY(EditAnywhere, BlueprintReadWrite, meta = (DisplayName = "Montage Groups"))
	TMap<FGameplayTag, FMontageGroup> MontageGroups;
};
```

</br>

#### 데이터 소유권 고민: 누가 이 데이터를 가져야 하나?

처음엔 "캐릭터가 데이터를 가지고, 무기 교체 시 참조만 바꾸면 되지 않을까?"라고 생각했습니다.

하지만 다음 이유로 **무기가 데이터를 소유**하도록 결정했습니다:

- ✅ 같은 종류의 무기는 동일한 전투 스타일 (한손검끼리, 폴암끼리 일관성)
- ✅ 무기의 정보는 무기 자체가 가지고 있는 게 **객체지향 원칙**에 부합
- ✅ 새 무기 추가 시 **무기 Blueprint만 만들면 끝** (캐릭터 수정 불필요)


**무기 클래스에 Data Asset 적용:**
```cpp
// 무기 header
class SOUL_API ASoulWeapon : public ASoulEquipment
{
protected:
	UPROPERTY(EditDefaultsOnly, Category = "Setting|Animation")
	TObjectPtr<UMontageActionData> MontageActionData;

    UPROPERTY(EditAnywhere, BlueprintReadWrite, Category = "Setting")
	ECombatType CombatType = ECombatType::SwordShield;
}
```

</br>

#### 무기 장착 시 전투 모드 자동 전환

무기를 장착하면 AnimInstance의 **전투 자세가 자동으로 변경**됩니다.

```cpp
void ASoulWeapon::EquipItem(int32 SlotIndex)
{
	if (UCombatComponent* CombatComp = CharacterBase->GetCombatComponent())
	{
        // 장착한 무기의 CombatType으로 AnimInstance 업데이트
        // → Idle/Walk/Run 애니메이션이 무기 타입에 맞게 자동 전환
		if (USoulAnimInstance* AnimInstance = Cast<USoulAnimInstance>(CharacterBase->GetMesh()->GetAnimInstance()))
		{
			AnimInstance->UpdateCombatMode(CombatType);
		}
	}
}
```

</br>

#### 공격 실행: 무기에서 데이터 조회

공격 시점에 **현재 무기에서 적절한 몽타주를 가져와 재생**합니다.

```cpp
void ASoulCharacterBase::DoAttack(const FGameplayTag& AttackTypeTag)
{
   // 1. 현재 장착한 무기에서 Tag + ComboCounter로 몽타주 검색
	UAnimMontage* Montage = Weapon->GetMontageForTag(NewAttackTypeTag, ComboCounter);

    // 2. 콤보 끝에 도달했다면 (더 이상 몽타주가 없음)
	if (false == IsValid(Montage)) {/*...*/}

    // 3. 몽타주 재생
    AnimInstance->Montage_Play(Montage);
	AnimInstance->Montage_SetEndDelegate(OnMontageEnded, Montage);
}
```

**데이터 흐름:**
```
무기 장착
  ↓
Data Asset 로드 + CombatType 전달
  ↓
AnimInstance 전투 모드 변경
  ↓
공격 입력 (Tag: Character.Attack.Light)
  ↓
무기의 Data Asset에서 Tag + Index로 몽타주 검색
  ↓
애니메이션 재생
```

</br>

### ✅ 결과 

**코드 수정 없이 확장 가능한 무기 시스템 완성**
- 새 무기 추가: Data Asset 생성 + 애니메이션 할당만으로 완료
- 밸런싱: 에디터에서 수치 조정 → 즉시 테스트 (컴파일 불필요)
- 각 무기가 Data Asset을 통해 **독립적으로 정의**됨
- 무기 타입 추가 시 **코드 수정 0줄**

**Before vs After:**

| 항목 | 하드코딩 | Data Asset 기반 |
|------|---------|----------------|
| 무기 추가 시간 | C++ 수정 + 컴파일 | Data Asset 생성 |
| 밸런스 조정 | 프로그래머 필요 | 에디터에서 즉시 가능 |
| 콤보 체계 변경 | 조건문 수정 | Asset에서 배열 조정 |
| 빌드 크기 | 모든 무기 포함 | 필요 시 로딩 |
| 코드 복잡도 | 무기마다 분기문 | Tag 기반 통합 로직 |

</br>

___

### [UE5 액션] 델리게이트(Delegate)를 활용한 유연한 인벤토리 시스템

### 🎮 구현 목표 

단순히 아이템을 줍고 장비를 착용하는 것을 넘어, **인벤토리-장비창 간 드래그 앤 드롭으로 아이템을 자유롭게 이동**하고, **상태 변화가 즉시 모든 UI에 반영**되는 시스템을 구현하고자 했습니다.

</br>

### 🚨 문제 상황

**복잡한 의존성: UI가 모든 컴포넌트를 알아야 하는 구조**

초기 설계에선 편의상 UI 위젯(예: `ItemSlotWidget`)이 `InventoryComponent`나 `CombatComponent`를 직접 참조해 기능을 호출했습니다.

- (문제 1) 복잡성: `ItemSlotWidget`이 아이템 사용을 위해 `InventoryComponent`를, 장착을 위해 `CombatComponent`를, 갱신을 위해 `EquipmentWidget`을 모두 알아야 했습니다.

- (문제 2) 양방향 의존: `InventoryComponent`도 장비가 해제되면 `EquipmentWidget`을 업데이트해야 했습니다. UI와 로직이 서로 거미줄처럼 얽혀, 기능 하나를 수정하면 관련된 모든 위젯을 수정해야 하는 '스파게티 코드'가 되었습니다.

핵심 문제 인식: UI가 데이터 로직을 너무 많이 알고 있다. "**UI는 데이터가 변경되었음을 알기만 하면 된다**"는 원칙이 필요했습니다.


</br>

### 💭 해결 원칙 
**"관심사 분리" (Separation of Concerns)**

복잡한 의존성을 끊어내기 위해 데이터 흐름을 단방향으로 강제했습니다.

- 데이터는 Component가 소유: `InventoryComponent`, `CombatComponent`가 모든 데이터(아이템 목록, 장착 정보)를 '소유'하고 변경 로직을 독점합니다.

- UI는 Manager와 소통: UI 위젯은 `WidgetManagerComponent`라는 **'중앙 관리자'**를 통해서만 Component에 "기능을 요청"합니다. (GetComponentByClass 난사 방지)

- 갱신은 Delegate로: Component는 데이터가 변경되면, 자신을 참조하는 UI를 찾는 대신 **Delegate(이벤트)`를 방송(Broadcast)**합니다.

- UI는 Delegate를 구독: 모든 UI(인벤토리, 장비창)는 이 Delegate를 **'구독(Subscribe)'**하고 있다가, 알림이 오면 스스로 갱신합니다.

개선된 흐름: UI 입력 → WidgetManager → Component (데이터 변경) → Delegate 방송 → 모든 구독 UI가 스스로 갱신


**아키텍처 다이어그램:**
```
[UI Layer]
 ItemSlotWidget ──┐
 EquipmentSlotWidget ─┤
                      ├─→ WidgetManager ─→ [Data Layer]
 InventoryWidget ──┤                       InventoryComponent
 EquipmentWidget ─┘                        CombatComponent
                                                   ↓
                      Delegate ←───────────────────┘
                         ↓
                    [UI 자동 갱신]
```


</br>

### 🔧 핵심 구현

**데이터 흐름:**
```
1. 플레이어가 새 무기 드래그 앤 드롭
   ↓
2. EquipmentSlotWidget::NativeOnDrop()
   ↓
3. InventoryComponent->RemoveItem(원본 슬롯)
   → OnInventoryUpdated Delegate 발행
   → InventoryWidget 자동 갱신
   ↓
4. Equipment->EquipItem()
   ↓
5. CombatComponent->SetWeapon(새 무기, 슬롯 인덱스)
   → 기존 무기를 InventoryComponent->AddItem(슬롯 인덱스)
   → OnInventoryUpdated Delegate 발행
   → InventoryWidget 다시 갱신 (기존 무기 표시)
   → OnChangedWeapon Delegate 발행
   → EquipmentWidget 자동 갱신
```


**1. Delegate를 이용한 자동 갱신**

InventoryComponent에 "인벤토리가 갱신되었다"는 신호(Delegate)를 만듭니다.

```cpp
DECLARE_DYNAMIC_MULTICAST_DELEGATE(FOnInventoryUpdated);

UCLASS()
class SOUL_API UInventoryComponent : public UActorComponent
{
public:
    UPROPERTY(BlueprintAssignable)
    FOnInventoryUpdated OnInventoryUpdated;  // UI가 구독할 Delegate

    bool AddItem(FName ItemID, int32 Amount)
    {
        // ... 데이터 변경 로직
        
        BroadcastInventoryUpdated();  // 변경 알림
        return true;
    }

    void BroadcastInventoryUpdated() const
    {
        if (OnInventoryUpdated.IsBound())
        {
            OnInventoryUpdated.Broadcast();
        }
    }
};
```

위젯은 Delegate 구독만 합니다.
```cpp
void UInventoryWidget::SetInventoryComponent(UInventoryComponent* NewInventoryComp)
{
    if (InventoryComponent)
    {
        // 기존 구독 해제
        InventoryComponent->OnInventoryUpdated.RemoveDynamic(this, &UInventoryWidget::RefreshInventory);
    }
    
    InventoryComponent = NewInventoryComp;
    if (InventoryComponent)
    {
        // 새로운 구독
        InventoryComponent->OnInventoryUpdated.AddDynamic(this, &UInventoryWidget::RefreshInventory);
        RefreshInventory();  // 초기 상태 반영
    }
}
```

</br>

**2. DragDropOperation으로 드래그 정보 관리

```cpp
// ItemDragDropOperation.h
UCLASS()
class UItemDragDropOperation : public UDragDropOperation
{
    GENERATED_BODY()
public:
    // 드래그 중인 아이템 정보
    UPROPERTY()
    FItemData ItemData;

    // 드래그 시작한 원본 슬롯
    UPROPERTY()
    USlotWidget* SourceSlotWidget;

	// swap시 바꿀 위치를 기록
    UPROPERTY()
    int32 SourceSlotIndex;
};
```

슬롯 위젯은 드롭이 감지되면, Operation 객체에 담긴 SourceSlotWidget을 확인하여 "아, 인벤토리에서 장비창으로 이동했구나" 혹은 "장비창에서 인벤토리로 이동했구나"를 판단하고, WidgetManager에 적절한 기능(장착/해제)을 요청합니다.

**드롭 처리 (EquipmentSlotWidget):**
```cpp
bool UEquipmentSlotWidget::NativeOnDrop(...)
{
    // 2. 드래그 출처 확인
    if (UItemSlotWidget* ItemSlot = Cast(Operation->SourceSlotWidget))
    {
        // 인벤토리 → 장비창: 장착
        if (ASoulItemBase* Item = Operation->ItemData.Item->GetDefaultObject())
        {
            FActorSpawnParameters SpawnParams;
            SpawnParams.Owner = GetOwningPlayerPawn();
            
            ASoulEquipment* Equipment = GetWorld()->SpawnActor(
                Operation->ItemData.Item, 
                GetOwningPlayerPawn()->GetActorTransform(), 
                SpawnParams
            );
            
            if (Equipment)
            {
                // 인벤토리에서 제거
                UWidgetManagerComponent::GetInventoryComponent()->RemoveItem(Operation->SourceSlotIndex);
                
                // 장비 장착 (내부에서 CombatComponent 업데이트)
                Equipment->EquipItem(Operation->SourceSlotIndex);
                
                // UI 갱신은 Delegate가 자동 처리!
            }
        }
    }
    else if (UEquipmentSlotWidget* EquipSlot = Cast(Operation->SourceSlotWidget))
    {
        // 장비창 → 인벤토리: 장착 해제
        // (별도 처리)
    }
}
```

**핵심:** UI는 단 한 줄(`Equipment->EquipItem()`)만 호출하지만, 나머지는 **Delegate 체인으로 자동 동기화**

</br>

### ✅ 결과 

이 아키텍처를 통해 UI와 데이터 로직을 성공적으로 분리했습니다.

- 단방향 데이터 흐름: 데이터 흐름이 명확해져 버그 추적이 쉬워졌습니다.
- 자유로운 드래그 앤 드롭: 인벤토리 ↔ 장비창 간 아이템 교체(Swap), 장착, 해제 로직이 Delegate를 통해 자동으로 동기화됩니다.
- 높은 확장성: '퀵슬롯'이나 '상점' UI를 새로 추가하더라도, WidgetManager에 접근하고 Delegate를 구독하기만 하면 기존 코드 수정 없이 즉시 시스템에 연동됩니다.

</br>

___


### [UE5 팀 프로젝트] 다이나믹 머티리얼로 강조 효과 구현하기

### 🎮 구현 목표 

팀원 요청사항으로, 캐릭터가 상호작용 가능한 오브젝트(재료, 조리대 등)에 **강조 효과(밝기 증가)**를 적용하여 플레이어가 "지금 이걸 집을 수 있구나"를 직관적으로 알 수 있도록 기능을 추가합니다.

</br>

### 🚨 문제 상황

**머티리얼을 2개씩 준비해야 하나?**

강조 효과를 구현하려면 머티리얼의 밝기를 조절해야 하는데, 리소스 작업이 이미 완료된 상태였습니다.

고민한 방법:
- 모든 오브젝트의 머티리얼을 복제 → 강조용/일반용 각각 준비
- 문제점: **리소스 2배 증가** + 관리 복잡도 상승

다행히 프로젝트 초기에 "베이스 머티리얼을 만들고 인스턴스로 작업하는 게 좋다"는 조언을 듣고 모두가 Material Instance로 작업했습니다. 이 구조 덕분에 **베이스 머티리얼에 밝기 파라미터만 추가**하면 모든 인스턴스에 자동 적용 가능했습니다.

</br>

### 💭 해결 방법

**Dynamic Material Instance로 런타임 파라미터 제어**

1. BeginPlay에서 모든 메시의 머티리얼을 Dynamic Material Instance로 변환
2. 원본 밝기값 저장 (복원용)
3. 강조 On → 밝기 증가 / 강조 Off → 원본 밝기 복원
```cpp
void AOC2Actor::BeginPlay()
{
    TArray MeshComponents;
    GetComponents(MeshComponents);

    for (UMeshComponent* Mesh : MeshComponents)
    {
        for (int i = 0; i < Mesh->GetNumMaterials(); i++)
        {
            UMaterialInterface* Material = Mesh->GetMaterials()[i];
            UMaterialInstanceDynamic* DynamicMaterial = 
                UMaterialInstanceDynamic::Create(Material, this);
            
            // 원본 밝기값 저장
            float OriginalValue;
            Material->GetScalarParameterValue(FName("DiffuseAdd"), OriginalValue);
            DiffuseColorMapWeights.Add(OriginalValue);
            
            Mesh->SetMaterial(i, DynamicMaterial);
        }
    }
}

void AOC2Actor::ApplyMaterialHighlight()
{
    // 런타임에 밝기 파라미터만 증가
    DynamicMaterial->SetScalarParameterValue(FName("DiffuseAdd"), HighlightValue);
}

void AOC2Actor::RestoreMaterial()
{
    // 저장해둔 원본 밝기로 복원
    DynamicMaterial->SetScalarParameterValue(FName("DiffuseAdd"), 
        DiffuseColorMapWeights[Index]);
}
```

약간의 성능 저하(Dynamic Material 생성 비용)가 우려되지만, 머티리얼을 2개씩 관리하는 것보다 합리적이라고 판단했습니다.

</br>

### 🔧 시행착오 

**간헐적 머티리얼 소실 버그**

테스트 중 **강조 해제 후 머티리얼이 날아가는 현상** 발견:
- 증상: 강조 효과 중 또는 강조효과가 끝난 이후 오브젝트의 머티리얼이 사라짐
- 재현: 간헐적 발생 (특정 조건 불명확)

시도 1: 원본 밝기값을 BeginPlay에서 저장
- 결과: 여전히 간헐적 발생

시도 2: 네트워크 동기화 문제로 추정 → RPC로 서버-클라 동기화
```cpp
UFUNCTION(Server, Reliable)
void Server_SetHighlight(bool Value);

UPROPERTY(ReplicatedUsing=OnRep_Highlight)
bool bIsHighlighted;
```
- 결과: **여전히 간헐적 발생**

</br>

**다시 생각해보면 동기화가 필요없는 작업인데**

캐릭터 개발자와 함께 디버깅하다가 설계 자체의 문제를 발견:

> "상호작용 강조는 **각 플레이어 화면에만 보이면 되는데**, 왜 서버에 RPC로 요청하고 모든 클라이언트에 복제하고 있지?"

문제의 흐름:
```
1. 클라이언트 A가 오브젝트에 접근
2. Server_SetHighlight() RPC 호출
3. 서버에서 bIsHighlighted = true로 변경
4. 모든 클라이언트에 OnRep_Highlight() 호출 ← 불필요!
5. 네트워크 타이밍 꼬임 → 복원 순서 문제
```

강조 효과는:
- 게임플레이에 영향 없는 **순수 시각 효과**
- 각 클라이언트가 **자신의 화면에서만** 보면 됨
- 다른 플레이어가 볼 필요 없음

**해결: 클라이언트 전용 처리**
```cpp
// RPC 제거, 로컬 함수로 변경
void AOC2Actor::SetHighlight(bool Value)
{
    if (Value)
        ApplyMaterialHighlight();
    else
        RestoreMaterial();
}
```

</br>

### ✅ 결과 

✅ **팀 부담 최소화**: 리소스 작업자 추가 작업 없이 C++ 코드로 기능 추가  
✅ **네트워크 최적화**: 불필요한 RPC/Replication 제거

</br>

___

### 2-3. 네트워크
### [UE5 팀 프로젝트] 지연 초기화: 런타임 액터 스폰, BeginPlay 호출 전 DataTable 데이터 무결성 확보

### 🎮 구현 목표 
플레이어가 스폰 테이블과 상호작용하면 **재료 액터를 동적으로 생성**합니다. 재료는 타입(토마토, 양파 등)에 따라 다른 메시와 데이터를 가지며, 모든 플레이어에게 동일하게 보여야 합니다.


### 💭 구현 방법
**재료 시스템을 어떻게 설계할 것인가?**

재료마다 고유한 메시, 아이콘, 조리 상태가 필요한데, 이를 어떻게 관리할지 두 가지 방안을 고민했습니다.

**A안: BP 클래스를 여러 개 만들기**
```
BP_Tomato (메시, 아이콘, 상태 모두 내장)
BP_Onion (메시, 아이콘, 상태 모두 내장)
BP_Lettuce (메시, 아이콘, 상태 모두 내장)
...
```

장점:
- 구현 간단: BP에서 모든 값 설정
- 에디터에서 바로 확인 가능

단점:
- ❌ 재료마다 BP 클래스 추가 (30종 → 30개 BP)
- ❌ 공통 로직 수정 시 모든 BP 수정 필요
- ❌ 스폰 테이블도 재료 수만큼 매칭 필요
```cpp
// 스폰 테이블마다 하드코딩
if (TableType == ESpawnTableType::Tomato)
    SpawnActor(BP_Tomato);
else if (TableType == ESpawnTableType::Onion)
    SpawnActor(BP_Onion);
// 30개 분기문...
```

**B안: 데이터 기반 설계**
```
재료 클래스: 1개 (껍데기, Type과 State만 가짐)
DataTable: 재료 정보 모두 등록 (메시, 아이콘, 조리 데이터)
```

장점:
- ✅ 재료 추가 시 DataTable에 Row 추가만
- ✅ 밸런싱/수정이 엑셀 작업처럼 간편
- ✅ 코드 수정 없이 기획 변경 대응

단점:
- 초기 구현 복잡도 높음
- 런타임에 DataTable 조회 필요

**선택: B안 (데이터 기반)**

</br>

### 🚨 문제 상황

**데이터 기반 설계의 함정**

```cpp
// 설계: 재료는 Type만 가지고, 나머지는 DataTable에서 조회
class AIngredient
{
    UPROPERTY(Replicated)
    EIngredientType IngredientType;  // Enum만 복제
};

// BeginPlay에서 DataTable 조회
void AIngredient::BeginPlay()
{
    FIngredientData* Data = DataTable->FindRow(IngredientType);
    SetMesh(Data->Mesh);
    SetTexture(Data->Icon);
}
```

**스폰 흐름:**
```
1. 스폰 테이블 상호작용 (클라이언트)
2. Server RPC 호출
3. 서버가 재료 스폰 (SpawnActor)
4. 재료의 Type 설정
5. BeginPlay 호출 → DataTable 조회
```

**발생한 버그:**  
스폰을 요청한 클라이언트 화면에만 재료가 보이고, **다른 플레이어들은 안 보임**.

디버깅 결과, 다른 클라이언트에서는 `IngredientType == None`으로 조회되어 메시가 설정되지 않았습니다.


</br>

### 🔧 구현

**네트워크 복제 타이밍 문제**

원인:
```
서버: SpawnActor → Type 설정 → BeginPlay → DataTable 조회 ✅
클라: SpawnActor → BeginPlay → Type 복제 (아직 안 됨!) ❌
```

클라이언트는 **BeginPlay가 먼저 호출**되고, Type은 **그 이후에 복제**되므로 DataTable 조회가 `None`으로 실패합니다.

**해결: SpawnActorDeferred**

"BeginPlay 전에 프로퍼티를 먼저 설정"할 수 있는 지연 스폰을 사용:
```cpp
AIngredient* USpawnManageComponent::SpawnIngredientActor(
    TSubclassOf IngredientClass, 
    EIngredientType Type)
{
    // 1. 메모리만 할당 (BeginPlay 호출 안 함)
    FTransform SpawnTransform;
    AIngredient* Ingredient = GetWorld()->SpawnActorDeferred(
        IngredientClass, 
        SpawnTransform
    );

    // 2. BeginPlay 전에 Type 설정 (Replicated 변수)
    Ingredient->SetType(Type);

    // 3. 이제 BeginPlay 호출 → 모든 클라에 Type이 이미 복제됨
    Ingredient->FinishSpawning(SpawnTransform);

    return Ingredient;
}
```

**실행 흐름:**
```
서버: SpawnDeferred → SetType → FinishSpawning → BeginPlay ✅
클라: (복제 대기) → Type 복제 완료 → BeginPlay ✅
```

`FinishSpawning` 호출 전에 `SetType`으로 Replicated 변수를 설정하면, BeginPlay가 호출될 때 **이미 모든 클라이언트에 Type이 복제된 상태**입니다.
```cpp
// Ingredient.cpp
void AIngredient::SetType_Implementation(EIngredientType Type)
{
    // Replicated 변수 설정 (BeginPlay 전)
    IngredientType = Type;
}

void AIngredient::BeginPlay()
{
    // 이제 모든 클라에서 IngredientType이 올바르게 설정됨
    FIngredientData* Data = DataTable->FindRow(IngredientType);
    SetMesh(Data->Mesh);
    SetTexture(Data->Icon);
}
```

</br>

### ✅ 결과 
✅ **모든 클라이언트에 재료 정상 표시**  
✅ **데이터 기반 설계 유지**: 재료 BP 클래스 1개 + DataTable로 모든 재료 타입 관리  
✅ **네트워크 복제 타이밍 이해**: BeginPlay 전후의 실행 순서 파악

일반 `SpawnActor`는 즉시 BeginPlay를 호출하므로, Replicated 변수 설정이 복제보다 늦을 수 있습니다. **SpawnActorDeferred**를 사용하면:
1. 메모리 할당
2. 프로퍼티 설정 (복제 준비)
3. `FinishSpawning` → BeginPlay 호출

이 순서로 실행되어 **BeginPlay 시점에 이미 모든 데이터가 복제된 상태**를 보장할 수 있습니다. 동적 스폰이 필요한 멀티플레이어 게임에서 필수 패턴입니다.

</br>

___

### [Dedicated Server] 비동기 폴링 기반 서버 접속 시도
### 🎮 구현 목표 
플레이어가 "게임 참가" 버튼을 클릭하면 **게임 세션 상태와 무관하게 자동으로 접속**되도록 합니다. 게임 세션이 없으면 생성하고, 활성화 중이면 대기했다가 자동으로 접속하는 것이 목표입니다.

### 🚨 문제 상황
**게임 세션 생성 타이밍 문제**

AWS GameLift에서 게임 세션 생성 요청을 보내면 **즉시 활성화되지 않습니다**:
```
1. Lambda에 게임 세션 생성 요청 (CreateGameSession)
2. GameLift가 EC2 인스턴스에 게임 세션 할당
3. 게임 서버 프로세스 초기화
4. 상태: ACTIVATING (약 3~10초 소요)
5. 상태: ACTIVE (플레이어 접속 가능)
```

**기존 흐름의 문제:**
```cpp
// 클라이언트: 버튼 클릭
void UGamePage::JoinGameButtonClicked()
{
    GameSessionsManager->JoinGameSession();  // 게임 세션 찾기/생성
}

void UGameSessionsManager::FindOrCreateGameSession_Response(...)
{
    // Lambda 응답: 새 게임 세션 생성됨
    FDSGameSession GameSession;
    
    if (GameSession.Status == "ACTIVATING")
    {
        // 아직 활성화 안 됨 → 플레이어 세션 생성 실패
        TryCreatePlayerSession(...);  // ❌ 실패!
    }
}
```
</br>

**플레이어 경험:**
```
1. "게임 참가" 버튼 클릭
2. 게임 세션 생성 및 활성화 시작
3. "게임 세션을 찾을 수 없습니다" 메시지 ❌
4. 다시 버튼 클릭
5. 게임 세션 상태 검사 : 만약 (ACTIVATING)이면 실패
6. "게임 세션을 찾을 수 없습니다" 메시지 ❌
7. 게임 세션이 ACTIVE 상태가 될 때 까지 실패 반환
```
플레이어는 게임 세션이 어떤 상태인지 중요하지 않습니다. 입력에 따른 피드백(결과)만 중요합니다. </br>

플레이어가 **수동으로 재시도**해야 하는 것은 매우 불편한 경험입니다. "왜 안 되지?" 하며 여러 번 클릭하는 것은 피로감을 줍니다.

따라서 내부적으로 어떻게 동작하는지 플레이어가 몰라도 의도한 결과를 받을 수 있도록 내부에서 타이머를 이용해 일정 시간 순환하는 방법을 고려했습니다.


</br>

### 💭 해결 방법
**Timer 기반 자동 재시도 (폴링)**

로직을 두 단계로 분리했습니다.
- ACTIVE 게임 세션이 존재하면 : 즉시 접속
- 게임 세션이 없다면 : 세션 생성을 요청하고 타이머 예약

핵심 아이디어: 게임 세션 상태를 확인하고, `ACTIVATING` 상태면 **자동으로 재시도**
```cpp
void UGameSessionsManager::HandleGameSessionStatus(const FString& Status, const FString& SessionId)
{
    // 플레이어 접속 처리
    if (Status.Equals(TEXT("ACTIVE")))
    {
        // 활성화 완료 → 플레이어 세션 생성
        BroadcastJoinGameSessionMessage.Broadcast(
            TEXT("Found activate Game Session. Creating a Player Session..."), false);

        if (UDS_LocalPlayerSubsystem* LocalPlayerSubsystem = GetDSLocalPlayerSubsystem())
        {
            TryCreatePlayerSession(LocalPlayerSubsystem->GetUsername(), SessionId);
        }
    }
    else if (Status.Equals(TEXT("ACTIVATING")))
    {
        // 활성화 중 → 0.5초 후 자동 재시도
        FTimerDelegate CreateSessionDelegate;
        CreateSessionDelegate.BindUObject(this, &ThisClass::JoinGameSession);
        
        APlayerController* LocalPlayerController = GEngine->GetFirstLocalPlayerController(GetWorld());
        if (IsValid(LocalPlayerController))
        {
            LocalPlayerController->GetWorldTimerManager().SetTimer(
                CreateSessionTimer, 
                CreateSessionDelegate, 
                0.5f,  // 0.5초 간격
                false  // 1회만 실행 (재귀적으로 반복)
            );
        }
    }
    else
    {
        // 예외 상태
        BroadcastJoinGameSessionMessage.Broadcast(
            TEXT("GameSessionStatus is Not ACTIVE or ACTIVATING"), true);
    }
}
```

**실행 흐름:**
```
1. 플레이어: "게임 참가" 버튼 클릭
2. JoinGameSession() 호출 → Lambda에 게임 세션 요청
3. Lambda 응답: Status = "ACTIVATING"
4. HandleGameSessionStatus() → Timer 설정 (0.5초 후)
5. 0.5초 후 JoinGameSession() 자동 재호출
6. Lambda 응답: 여전히 "ACTIVATING" → Timer 재설정
7. 0.5초 후 JoinGameSession() 자동 재호출
8. Lambda 응답: Status = "ACTIVE" → 플레이어 세션 생성
9. 서버 접속 성공 ✅
```

**개선된 플레이어 경험:**
```
1. "게임 참가" 버튼 클릭
2. "게임 세션을 찾는 중..." 메시지
3. (내부적으로 자동 재시도 중)
4. "플레이어 세션 생성 중..." 메시지
5. 로비 레벨로 자동 전환 ✅
```

플레이어는 **한 번만 클릭**하고, 내부적으로 알아서 처리됩니다.

</br>

**Delegate로 UI 피드백**

재시도 중에도 플레이어가 "멈춘 게 아니구나"를 알 수 있도록 ```BroadcastJoinGameSessionMessage``` Delegate로 상태 메시지를 전달:
```cpp
// GameSessionsManager.h
UPROPERTY(BlueprintAssignable)
FAPIStatusMessgae BroadcastJoinGameSessionMessage;

// GamePage.cpp - UI가 Delegate 구독
void UGamePage::NativeConstruct()
{
    GameSessionsManager->BroadcastJoinGameSessionMessage.AddDynamic(
        JoinGameWidget, &UJoinGame::SetStatusMessage);
}

// 상태 변화마다 메시지 업데이트
BroadcastJoinGameSessionMessage.Broadcast(TEXT("Searching for Game Session..."), false);
BroadcastJoinGameSessionMessage.Broadcast(TEXT("Creating Player Session..."), false);
```

</br>

### ✅ 결과 

✅ **원클릭 접속**: 플레이어는 버튼 한 번만 클릭  
✅ **자동 재시도**: `ACTIVATING` 상태일 때 0.5초 간격으로 폴링  
✅ **UX 개선**: "연결 중..." 메시지로 진행 상황 피드백

</br>

___
### [Dedicated Server] ```SeamlessTravel```: 레벨 전환 시 데이터 유실 방지
### 🎮 구현 목표 
서버에 접속한 플레이어들은 로비 레벨에서 모인 뒤, 게임 시작 시 **SeamlessTravel**로 플레이 레벨로 이동합니다. 이 과정에서 플레이어의 `Username`이 유지되어야 DB에 플레이 기록을 정상적으로 저장할 수 있습니다.

</br>

### 🚨 문제 상황
**SeamlessTravel 후 닉네임이 공백으로 표시**

플레이어 정보 저장 전략:
- ```PlayerState```: 닉네임(Username), PlayerSessionId (게임 내 공유 데이터)
- ```LocalPlayerSubsystem```: AccessToken, Email (로컬 전용 데이터)
````cpp
// 로비 입장 시 (GameSessionsManager.cpp)
const FString Options = "PlayerSessionId=" + PlayerSession.PlayerSessionId 
                      + "?Username=" + PlayerSession.PlayerId;
UGameplayStatics::OpenLevel(this, Address, true, Options);
````

로비 레벨에서는 정상적으로 닉네임이 표시되지만, **SeamlessTravel로 플레이 레벨 전환 후 닉네임이 초기화**되는 문제 발생:
````
로비 레벨: 닉네임 "Kabu" ✅
   ↓ (SeamlessTravel)
플레이 레벨: 닉네임 "" (공백) ❌
````

연쇄 문제:
- 킬 로그에 닉네임 공백 표기 ❌
- DB에 플레이어 기록 저장 실패 (Username이 공백) ❌

</br>

### 💭 해결 방법
**"왜 SeamlessTravel 후 데이터가 날아가지?"**

처음엔 "레벨 전환은 자동으로 데이터를 유지해주는 거 아닌가?" 생각했지만, 테스트 결과 **PlayerState의 커스텀 변수는 자동으로 복사되지 않음**을 확인.

**첫 번째 시도: PlayerState 클래스 통일**

의심: "로비 레벨과 플레이 레벨의 PlayerState 클래스가 달라서 그런가?"
````cpp
// Before
로비 레벨: DS_DefaultPlayerState (서버 모듈)
플레이 레벨: BP_MatchPlayerState (컨텐츠 모듈, DS_DefaultPlayerState 상속)

// After: 통일 시도
로비 레벨: BP_MatchPlayerState
플레이 레벨: BP_MatchPlayerState
````

결과: **여전히 초기화됨** ❌

상속받았어도 문제가 해결되지 않는 이유를 찾아야 했습니다.

</br>

**두 번째 시도: SeamlessTravel 동작 원리 조사**

UE5 공식 문서와 코드를 찾아보니, SeamlessTravel 시 PlayerState는:
````
1. 구 레벨에서 PlayerState 복사본 생성 (CopyProperties 호출)
2. 신 레벨로 PlayerState 이동
3. 신 레벨의 기존 PlayerState와 병합 (OverrideWith 호출)
````

핵심 발견: **```CopyProperties()```와 ```OverrideWith()```를 오버라이드하지 않으면 커스텀 변수는 복사 안 됨!**

**해결: 수동 복사 구현**
````cpp
// DS_DefaultPlayerState.cpp
void ADS_DefaultPlayerState::CopyProperties(APlayerState* PlayerState)
{
    Super::CopyProperties(PlayerState);

    // 구 PlayerState → 신 PlayerState로 복사
    if (ADS_DefaultPlayerState* NewPlayerState = Cast(PlayerState))
    {
        NewPlayerState->DefaultUsername = DefaultUsername;
        NewPlayerState->DefaultPlayerSessionId = DefaultPlayerSessionId;
    }
}

void ADS_DefaultPlayerState::OverrideWith(APlayerState* PlayerState)
{
    Super::OverrideWith(PlayerState);

    // 신 레벨의 임시 PlayerState → 실제 PlayerState로 덮어쓰기
    if (ADS_DefaultPlayerState* OldPlayerState = Cast(PlayerState))
    {
        DefaultUsername = OldPlayerState->DefaultUsername;
        DefaultPlayerSessionId = OldPlayerState->DefaultPlayerSessionId;
    }
}
````

**동작 흐름:**
````
[로비 레벨]
PlayerState A (닉네임: "Kabu")
   ↓
1. CopyProperties() 호출
   → 임시 PlayerState B 생성 (닉네임: "Kabu" 복사)
   ↓
2. SeamlessTravel 시작
   ↓
[플레이 레벨]
PlayerState C (새로 생성, 닉네임: "")
   ↓
3. OverrideWith() 호출
   → PlayerState B의 데이터를 C에 덮어쓰기
   → 최종: PlayerState C (닉네임: "Kabu") ✅
````
</br>

### 🔧 시행착오 
**왜 PlayerState에 저장했는가?**

처음엔 ```PlayerController```에 닉네임을 저장했습니다. `PlayerController`는 `SeamlessTravel` 시 자동으로 데이터가 유지되므로 편했습니다.
````cpp
// 초기 구조 (잘 작동함)
class ADS_PlayerController
{
    UPROPERTY(Replicated)
    FString Username;  // SeamlessTravel 후에도 유지됨 ✅
};
````

**그런데 왜 PlayerState로 옮겼나?**

설계 원칙상 "**플레이어 게임 데이터는 PlayerState가 소유**"하는 것이 맞다고 판단:
- PlayerController: 입력 처리, 카메라 제어 (제어 관련)
- PlayerState: 점수, 닉네임, 팀 정보 (게임 데이터)

실제 사용 케이스:
````cpp
void UEliminationComponent::ProcessElimination(bool bHeadShot, AMatchPlayerState* AttackerPS, AMatchPlayerState* VictimPS)
{
    AMatchGameState* GameState = Cast<AMatchGameState>(UGameplayStatics::GetGameState(AttackerPS));
    if (IsValid(GameState))
    {
        HandleFirstBlood(GameState, SpecialElimType, AttackerPS);
        UpdateLeaderStatus(GameState, SpecialElimType, AttackerPS, VictimPS);
        
        // GameState->Multicast Deleaget Broadcast -> Widget Kill Feed Update
        FKillInfo KillInfo;
        KillInfo.KillerName = AttackerPS->GetUsername();
        KillInfo.VictimName = VictimPS->GetUsername();
        
        GameState->AnnounceKill(KillInfo);
    }
}
````

</br>

**Replicated 변수인데 왜 복사가 필요한가?**

처음엔 "```UPROPERTY(Replicated)```로 선언했으니 자동 동기화 아닌가?" 생각했지만:
````cpp
UPROPERTY(ReplicatedUsing = OnRep_Username)
FString DefaultUsername = "";
````

**Replication ≠ SeamlessTravel 데이터 유지**
- Replication: 서버 → 클라이언트 동기화
- SeamlessTravel: 구 레벨 → 신 레벨 데이터 이동 (별도 메커니즘!)

따라서 Replicated 변수여도 ```CopyProperties()```/```OverrideWith()``` 구현 필수.



</br>

### ✅ 결과 
✅ **닉네임 정상 표시**: SeamlessTravel 후에도 "Kabu" 유지  
✅ **DB 저장 성공**: PlayerId가 공백이 아닌 실제 닉네임으로 저장  

**"SeamlessTravel은 PlayerState를 자동으로 복사하지 않는다"**
언리얼의 ```PlayerState```는 기본 프로퍼티(PlayerName, Score 등)만 자동 복사하고, **커스텀 변수는 개발자가 직접 ```CopyProperties()```와 ```OverrideWith()```를 구현**해야 합니다.
- ```CopyProperties()```: 구 레벨에서 신 레벨로 데이터 복사
- ```OverrideWith()```: 신 레벨의 임시 PlayerState를 실제 PlayerState에 병합

</br>

___

### [Dedicated Server] 콜백(Callback) 체인을 활용한 데이터 무결성 확보
### 🎮 구현 목표

경기 종료 후 **Player Table → Leaderboard Table** 순서로 DB 업데이트가 진행되어, 랭킹이 정확하게 반영되도록 합니다. 
Player Table에 최신 승수가 저장된 후에야 Leaderboard가 올바르게 갱신될 수 있습니다.

</br>

### 🚨 문제 상황

**1등이 2등으로 표시되는 버그**

경기 종료 후 순위 계산 흐름:
```
1. Player Table에 승수 기록 (matchWins += 1)
2. Leaderboard Table에서 상위 10명 갱신
```

그런데 실제로는:
```
플레이어 A: 5승 → 6승 (우승!)
   ↓
[동시에 발생]
Lambda 1: Player Table에 6승 기록 중... (느림)
Lambda 2: Leaderboard 갱신 (Player Table 조회) → 아직 5승! ❌
   ↓
결과: Leaderboard에 5승으로 기록됨
```

**문제의 핵심: 비동기 작업의 순서 미보장**

AWS Lambda는 비동기로 실행되므로, 두 Lambda를 동시에 호출하면:
```cpp
// 게임 종료 시 (잘못된 구현)
void ADS_MatchGameMode::OnMatchEnded()
{
    // 두 요청이 거의 동시에 발생
    GameStatsManager->RecordMatchStats(...);     // Lambda 1
    GameStatsManager->UpdateLeaderboard(...);    // Lambda 2
    
    // Lambda 2가 Lambda 1보다 먼저 끝날 수 있음!
}
```

실제 테스트 결과:
```
경기 1: 우승 → 랭킹 1위 ✅
경기 2: 우승 → 랭킹 2위 ❌ (Player Table 갱신 전 Leaderboard 조회)
경기 3: 우승 → 랭킹 1위 ✅
```

간헐적으로 발생하는 이유는 **네트워크 지연**에 따라 Lambda 실행 순서가 바뀌기 때문입니다.

</br>

### 💭 해결 방법

**"Player Table 저장이 끝났다는 걸 어떻게 알지?"**

비동기 작업의 순서를 보장하려면 **"첫 번째 작업 완료 → 두 번째 작업 시작"** 구조가 필요했습니다.

**초기 고민: Timer로 지연?**
```cpp
GameStatsManager->RecordMatchStats(...);
GetWorldTimerManager().SetTimer(TimerHandle, [this]() {
    GameStatsManager->UpdateLeaderboard(...);
}, 2.0f, false);  // 2초 후 실행
```

문제:
- 2초면 충분한가? 3초는? → 정답 없음
- Lambda가 느려지면 여전히 실패
- 불필요한 대기 시간

**해결: Delegate 체인**

"Player Table 저장 성공 시 Delegate 발행 → Leaderboard 갱신" 구조로 변경
```cpp
// GameStatsManager.h
DECLARE_DYNAMIC_MULTICAST_DELEGATE(FOnAPIRequestSucceeded);

class UGameStatsManager : public UHTTPRequestManager
{
public:
    void RecordMatchStats(const FDSRecordMatchStatsInput& Input);
    void UpdateLeaderboard(const TArray<FString>& PlayerNames);
    
    UPROPERTY(BlueprintAssignable)
    FOnAPIRequestSucceeded OnUpdatedGameStatsSucceeded;  // 핵심!
};
```

**Lambda 응답 처리:**
```cpp
// GameStatsManager.cpp
void UGameStatsManager::RecordMatchStats_Response(
    FHttpRequestPtr Request, 
    FHttpResponsePtr Response, 
    bool bWasSuccessful)
{
    if (!bWasSuccessful) return;
    
    TSharedPtr<FJsonObject> JsonObject;
    TSharedRef<TJsonReader<>> JsonReader = 
        TJsonReaderFactory<>::Create(Response->GetContentAsString());
    
    if (FJsonSerializer::Deserialize(JsonReader, JsonObject))
    {
        if (ContainsErrors(JsonObject, true)) return;
        
        // Player Table 저장 성공!
        UE_LOG(LogDedicatedServers, Warning, 
            TEXT("RecordMatchStats_Response Succeeded!"));
        
        OnUpdatedGameStatsSucceeded.Broadcast();  // Delegate 전파
    }
}
```

**GameMode에서 Delegate 구독:**
```cpp
// DS_MatchGameMode.cpp
void ADS_MatchGameMode::CreateGameStatsManager()
{
    GameStatsManager = NewObject<UGameStatsManager>(this, GameStatsManagerClass);
    
    // Delegate 구독 (핵심!)
    GameStatsManager->OnUpdatedGameStatsSucceeded.AddDynamic(
        this, 
        &ADS_MatchGameMode::OnGameStatsUpdated
    );
}

void ADS_MatchGameMode::OnMatchEnded()
{
    // 1. Player Table에 승수 기록만 요청
    EndMatchForPlayerStats();  // RecordMatchStats 호출
    
    // 2. Leaderboard는 여기서 호출 안 함!
    // (Delegate 콜백에서 호출됨)
}

// Delegate 콜백
void ADS_MatchGameMode::OnGameStatsUpdated()
{
    // Player Table 저장 완료 후 자동 호출됨!
    UE_LOG(LogTemp, Warning, TEXT("OnGameStatsUpdated"));
    
    // 2. 이제 Leaderboard 갱신
    TArray<FString> LeaderIds;
    if (AMatchGameState* GS = GetGameState<AMatchGameState>())
    {
        TArray<AMatchPlayerState*> Leaders = GS->GetLeaders();
        for (AMatchPlayerState* Leader : Leaders)
        {
            LeaderIds.Add(Leader->GetUsername());
        }
    }
    
    UpdateLeaderboard(LeaderIds);  // 최신 데이터로 갱신 ✅
}
```

**개선된 흐름:**
```
1. 경기 종료
   ↓
2. RecordMatchStats() 호출 (Player Table 갱신)
   ↓
3. Lambda 실행... (비동기)
   ↓
4. Lambda 성공 응답
   ↓
5. OnUpdatedGameStatsSucceeded.Broadcast()
   ↓
6. OnGameStatsUpdated() 자동 호출
   ↓
7. UpdateLeaderboard() 호출 (최신 데이터 조회) ✅
```

</br>

### 🔧 고려사항
**왜 서버에서 순위를 계산하지 않았나?**

고민: "서버가 직접 순위 계산하면 Lambda 2개 필요 없지 않나?"
```cpp
// 고려했던 방법
void ADS_MatchGameMode::OnMatchEnded()
{
    // 서버가 직접 PlayerState 순회하며 순위 계산
    TArray<AMatchPlayerState*> AllPlayers;
    // ... 정렬 로직
    
    // DB에 한 번에 저장
    GameStatsManager->RecordMatchStatsWithRanking(AllPlayers);
}
```

그러나 **DB는 Single Source of Truth**여야 한다고 판단:
- 서버 크래시 시 데이터 소실 위험
- 여러 게임 세션 간 랭킹 통합 불가
- Lambda 분리 = 관심사 분리 (Player 기록 vs Leaderboard 갱신)

</br>

### ✅ 결과

✅ **순위 정확도 100%**: Player Table 저장 후 Leaderboard 갱신 보장  
✅ **간헐적 버그 해결**: 네트워크 지연과 무관하게 순서 보장  
✅ **확장성**: 새로운 통계 추가 시 Delegate 체인 확장 가능

**핵심 교훈:**

**"비동기 작업의 순서는 코드 순서가 아니라 Delegate로 보장한다"**

HTTP 요청, Lambda 호출 같은 비동기 작업은 **응답 시점을 예측할 수 없습니다**. 

Delegate 패턴:
```
작업 1 호출 → 응답 대기 → Delegate 전파 → 작업 2 자동 시작
```

이 방식은:
- 네트워크 지연과 무관하게 순서 보장
- Lambda 실행 시간이 늘어나도 안전
- 여러 단계의 비동기 작업 체인 가능

AWS Lambda, REST API, GameLift 같은 **외부 서비스와 통신**할 때 필수 패턴입니다.

</br>

___

### 2-4. 협업 및 버전 관리
### [UE5 팀 프로젝트] Pull-Request 시행착오와 교훈
### 🎮 선택 의도

6인 팀 프로젝트의 코드 충돌을 예방하기 위해 '안전한' Fork-PR(Pull-Request) 전략을 채택했습니다.

**선택한 워크플로우: Fork-PR**
```
1. 각자 메인 저장소를 Fork
2. 개인 저장소에서 작업
3. 완료 후 Pull Request 생성
4. 리뷰어(관리자)가 코드 검토 후 Merge
```

### 🚨 문제 상황

1. 관리자 병목 현상 초기 개발 단계에선 빠른 기능 추가가 필요한데, 관리자의 코드 리뷰가 '병목'이 되었습니다.

- Fork-PR: PR 생성 → 리뷰 대기 → Merge → 팀원 Pull

- 문제: 단순 Getter 함수 하나를 Merge하는 데 10분 이상 소요되어, 의존성이 있는 다른 팀원의 작업이 그대로 멈췄습니다.

2. 진짜 문제는 .uasset 충돌 정작 .cpp/.h 코드 충돌은 클래스 단위 작업 분리로 인해 거의 없었습니다. 진짜 문제는 바이너리 파일인 .uasset(블루프린트, 레벨) 충돌이었습니다.

- 치명적 한계: uasset은 텍스트가 아니라 리뷰(Review)가 불가능했습니다.

- 사고 발생: 충돌 시 Git은 자동 병합을 못하고 "내 것" 아니면 "상대 것"을 선택해야만 했습니다. 이 과정에서 **한쪽의 작업물이 그대로 유실(lost)**되는 사고가 발생했습니다.

- 결국, Fork-PR은 잡지도 못할 uasset 충돌을 예방하지도 못하면서, 코드 리뷰로 인한 속도 저하만 유발했습니다.

</br>

### 🔧 해결 및 교훈
1. 긴급 소통 채널 운영
- Discord에 "긴급 PR" 채널 생성
- 급한 PR은 여기 알림
- 관리자가 우선 처리

1. uasset 충돌은 Git 기능이 아닌, 사람 간의 '소통'으로 해결했습니다.
- 사전 공지: BP_Ingredient처럼 공용 블루프린트 수정 전, Discord에 미리 공지.
- 수동 병합: 충돌 시, 양쪽 작업자가 구두로 변경 사항을 확인한 뒤, 한 명이 수동으로 두 변경 사항을 모두 재적용했습니다.

2. 'git stash'의 발견 프로젝트 후반에 git stash라는 더 효율적인 방법을 알게 되었습니다.

```bash
# 현재 작업 임시 저장
git stash

# 최신 코드 가져오기
git pull origin main

# 작업 다시 꺼내기
git stash pop

# 충돌 나면 수동 해결
```

**"이걸 일찍 알았더라면..."**

Stash를 알았다면:
```
A: "기능 완료" → Push
B: 작업 중 → git stash → git pull → git stash pop
   → 충돌 있으면 해결 → 작업 계속
```

</br>

### ✅ 결과
워크플로우는 팀의 규모와 단계에 맞춰야 합니다.

Fork-PR은 코드 품질이 중요하고 리뷰 인력이 충분한 대규모/안정화 프로젝트에 적합합니다.

우리처럼 '빠른 프로토타이핑'이 중요한 소규모/초기 팀은, git stash 활용법을 익히고 '작업 전 소통'을 강화하는 Direct Push 방식이 훨씬 효율적이었을 것이라는 교훈을 얻었습니다.

</br>

___

### 2-5. 최적화 전략 

### [DirectX 11] Unity 리소스 메타데이터 파싱을 통한 스프라이트 시트 관리

### 🎮 구현 목표

Unity에서 제작된 스프라이트 시트의 메타데이터(.smeta) 파일을 파싱하여, DirectX 11 엔진에서 개별 스프라이트의 UV 좌표와 크기 정보를 자동으로 추출하고 관리하는 시스템을 구축합니다.

</br>

### 🚨 문제 상황

1. 반복적인 수작업의 비효율성
- 리소스를 포토샵에서 하나 하나 크기에 맞춰 잘라야하는 수작업
- 리소스를 분석하여 프레임 순서에 맞춰 파일 이름을 정렬
- 스프라이트 시트에서 각 프레임의 픽셀 좌표와 크기를 일일이 계산
- 프로그램에서 렌더링 후 피봇 불일치 시, 다시 포토샵으로 작업 후 업로드하는 불편함

</br>

2. 유지보수의 어려움
- 스프라이트 인덱스를 직접 계산하고 체크 (위험)

사전에 리소스를 준비하고 편집하는 시간이 상당히 오래걸리고, 리소스를 추가할 때마다 수 시간이 소요되는 작업 부하가 발생했습니다. </br>
리스소와 관련된 작업의 부담을 해소하기 위해 파일시스템과 데이터 파싱을 이용하기로 했습니다.


</br>

### 💭 해결 방안

#### 아키텍처

```
UEngineDirectory (파일 탐색)
        ↓
UEngineFile (파일 읽기)
        ↓
UEngineSprite::CreateSpriteToMeta (메타 파싱)
        ↓
FSpriteData (UV 좌표 변환)
        ↓
SpriteRenderer (렌더링)
```

#### 1. 파일 시스템 추상화

```cpp
class UEngineDirectory : public UEnginePath
{
public:
    // 확장자 필터링과 재귀 탐색을 지원하는 파일 검색
    std::vector<UEngineFile> GetAllFile(
        bool _IsRecursive, 
        const std::vector<std::string>& _Exts
    );
    
    std::vector<UEngineDirectory> GetAllDirectory();
};
```

**설계 의도:**
- 디렉토리 구조를 추상화하여 리소스 자동 로딩 시스템 구축
- 확장자 기반 필터링으로 원하는 파일만 선별적으로 처리
- 재귀 탐색으로 서브 디렉토리 리소스까지 일괄 로딩

</br>

#### 2. Unity 메타데이터 포맷 분석

<p align="center">
 <img alt="이미지" src="readme\Parse.png">
</p>

Unity .smeta 파일 구조:
```yaml
rect:
  serializedVersion: 2
  x: 128
  y: 256
  width: 64
  height: 64
alignment: 0
pivot: {x: 0.5, y: 0.5}
outline: []
```

**핵심 정보:**
- `rect`: 스프라이트 시트 내 픽셀 좌표와 크기
- `pivot`: 스프라이트의 중심점 (0~1 정규화 값)

</br>

#### 3. 문자열 파싱 전략

```cpp
//"rect:"와 "outline:" 사이의 텍스트 추출
size_t RectIndex = Text.find("rect:", StartPosition);
size_t AligIndex = Text.find("outline:", RectIndex);

if (RectIndex == std::string::npos || AligIndex == std::string::npos)
{
    break;  // 더 이상 스프라이트 데이터가 없음
}

NewSpirte->SpriteTexture.push_back(Tex.get());
SpriteDataTexts.push_back(Text.substr(RectIndex, AligIndex - RectIndex));
StartPosition = AligIndex;
```

**파싱 로직:**
1. `rect:` 키워드로 스프라이트 데이터 시작 지점 탐색
2. `outline:` 키워드로 종료 지점 확인
3. 두 키워드 사이의 텍스트 블록을 추출하여 개별 스프라이트 데이터로 분리

</br>

#### 4. 수치 데이터 추출

```cpp
FSpriteData SpriteData;

// X 좌표 추출
std::string Number = UEngineString::InterString(Text, "x:", "\n", Start);
SpriteData.CuttingPos.X = static_cast<float>(atof(Number.c_str()));

// Y 좌표 추출
Number = UEngineString::InterString(Text, "y:", "\n", Start);
SpriteData.CuttingPos.Y = static_cast<float>(atof(Number.c_str()));

// Width 추출
Number = UEngineString::InterString(Text, "width:", "\n", Start);
SpriteData.CuttingSize.X = static_cast<float>(atof(Number.c_str()));

// Height 추출
Number = UEngineString::InterString(Text, "height:", "\n", Start);
SpriteData.CuttingSize.Y = static_cast<float>(atof(Number.c_str()));

// Pivot X 추출 (쉼표로 구분)
Number = UEngineString::InterString(Text, "x:", ",", Start);
SpriteData.Pivot.X = static_cast<float>(atof(Number.c_str()));

// Pivot Y 추출 (중괄호로 종료)
Number = UEngineString::InterString(Text, "y:", "}", Start);
SpriteData.Pivot.Y = static_cast<float>(atof(Number.c_str()));
```

**InterString 함수의 역할:**
- 시작 문자열과 종료 문자열 사이의 부분을 추출
- `Start` 변수로 파싱 위치를 추적하여 순차적으로 값을 읽음

</br>

#### 5. 좌표계 변환 및 정규화

```cpp
FVector TexSize = Tex->GetTextureSize();

// Y축 반전 (Unity는 왼쪽 하단 기준, DirectX는 왼쪽 상단 기준)
SpriteData.CuttingPos.Y = TexSize.Y - SpriteData.CuttingPos.Y - SpriteData.CuttingSize.Y;

// 픽셀 좌표를 0~1 UV 좌표로 정규화
SpriteData.CuttingPos.X /= TexSize.X;
SpriteData.CuttingPos.Y /= TexSize.Y;
SpriteData.CuttingSize.X /= TexSize.X;
SpriteData.CuttingSize.Y /= TexSize.Y;
```

**좌표계 차이 해결:**
| 엔진 | 원점 위치 | Y축 방향 |
|------|----------|---------|
| Unity | 왼쪽 하단 | 위쪽이 양수 |
| DirectX | 왼쪽 상단 | 아래쪽이 양수 |

**정규화의 이점:**
- 텍스처 크기와 무관하게 동일한 UV 좌표 사용 가능
- GPU 샘플러가 직접 활용할 수 있는 형식

</br>

## 🔧 시행착오

### 1. 초기 구현: 폴더 기반 스프라이트 로딩

```cpp
std::shared_ptr<UEngineSprite> UEngineSprite::CreateSpriteToFolder(
    std::string_view _Name, 
    std::string_view _Path)
{
    UEngineDirectory Dir = _Path;
    std::vector<UEngineFile> Files = Dir.GetAllFile(false, { ".png"});

    for (size_t i = 0; i < Files.size(); i++)
    {
        // 기본값으로 전체 텍스처 사용 (UV: 0~1)
        FSpriteData SpriteData;
        SpriteData.CuttingPos = { 0.0f, 0.0f };   // 시작점
        SpriteData.CuttingSize = { 1.0f, 1.0f };  // 전체 크기
        SpriteData.Pivot = { 0.5f, 0.5f };        // 중앙 피벗
        NewSpirte->SpriteDatas.push_back(SpriteData);
    }
}
```

**한계점:**
- 스프라이트 시트를 활용할 수 없고, 개별 이미지 파일만 처리 가능
- 애니메이션 프레임마다 별도 파일이 필요해 파일 관리 부담 증가
- 텍스처 전환 오버헤드로 렌더링 성능 저하

</br>

### 2. 문자열 파싱 중 인덱스 관리 문제

**초기 시도:**
```cpp
// 잘못된 예시 - Start 변수를 갱신하지 않음
std::string Number = UEngineString::InterString(Text, "x:", "\n", 0);
SpriteData.CuttingPos.X = atof(Number.c_str());

// 동일한 시작 위치에서 다시 검색하면 첫 번째 "y:"를 찾게 됨
Number = UEngineString::InterString(Text, "y:", "\n", 0);  // 버그!
```

**해결책:**
```cpp
// Start 변수를 참조로 전달하여 파싱 위치 추적
size_t Start = 0;  // 파싱 커서

// InterString 함수가 Start를 자동으로 갱신
std::string Number = UEngineString::InterString(Text, "x:", "\n", Start);
SpriteData.CuttingPos.X = atof(Number.c_str());

// 다음 호출 시 이전 위치 다음부터 검색
Number = UEngineString::InterString(Text, "y:", "\n", Start);
SpriteData.CuttingPos.Y = atof(Number.c_str());
```

</br>

### 3. Y축 좌표계 변환 누락

**문제 상황:**
```cpp
// 변환 없이 그대로 사용 시
SpriteData.CuttingPos.Y = PixelY / TexSize.Y;

// 결과: 스프라이트가 상하 반전되어 렌더링됨
```

**원인 분석:**
- Unity: 원점이 왼쪽 하단, Y축이 위쪽으로 증가
- DirectX: 원점이 왼쪽 상단, Y축이 아래쪽으로 증가

**해결:**
```cpp
// 135 라인: Y축 반전 공식
SpriteData.CuttingPos.Y = TexSize.Y - SpriteData.CuttingPos.Y - SpriteData.CuttingSize.Y;
```

이 공식은 다음과 같이 동작합니다:
1. `TexSize.Y`: 텍스처 전체 높이
2. `CuttingPos.Y`: Unity 좌표계의 Y 위치
3. `CuttingSize.Y`: 스프라이트 높이
4. 결과: DirectX 좌표계로 변환된 Y 위치

</br>

### 4. 멀티 스프라이트 처리

**초기 구조:**
```cpp
// 하나의 메타 파일에 하나의 스프라이트만 처리
std::shared_ptr<UEngineSprite> CreateSpriteToMeta(std::string_view _Name);
```

**개선된 구조:**
```cpp
// 루프를 통한 멀티 스프라이트 처리
while (true)
{
    size_t RectIndex = Text.find("rect:", StartPosition);
    size_t AligIndex = Text.find("outline:", RectIndex);
    
    if (RectIndex == std::string::npos || AligIndex == std::string::npos)
    {
        break;  // 모든 스프라이트 추출 완료
    }
    
    NewSpirte->SpriteTexture.push_back(Tex.get());
    SpriteDataTexts.push_back(Text.substr(RectIndex, AligIndex - RectIndex));
    StartPosition = AligIndex;  // 다음 검색 위치 갱신
}
```

**개선 효과:**
- 하나의 스프라이트 시트에 여러 프레임이 있어도 자동으로 모두 추출
- 애니메이션 시퀀스를 하나의 리소스로 통합 관리 가능

</br>

## ✅ 결과

### 1. 리소스 로딩 자동화

```cpp
// ContentsResource.cpp: 메타데이터 기반 일괄 로딩
void UContentsResource::LoadSpriteMetaData()
{
    UEngineSprite::CreateSpriteToMeta("WanderingHusk.png", ".smeta");
    UEngineSprite::CreateSpriteToMeta("LeapingHusk.png", ".smeta");
    UEngineSprite::CreateSpriteToMeta("FalseKnight.png", ".smeta");
    UEngineSprite::CreateSpriteToMeta("Explode.png", ".smeta");
    // 한 줄로 수십 개의 프레임 자동 로딩
}
```

### 2. 애니메이션 구현 간소화

```cpp
// 사용 예시: 몬스터 애니메이션 설정
std::shared_ptr<UEngineSprite> WanderingHuskSprite = 
    UEngineSprite::Find<UEngineSprite>("WanderingHusk.png");

// 스프라이트 개수 자동 파악
int FrameCount = WanderingHuskSprite->GetSpriteCount();

// 프레임별 UV 좌표 자동 적용
for (int i = 0; i < FrameCount; ++i)
{
    FSpriteData Data = WanderingHuskSprite->GetSpriteData(i);
    // Data.CuttingPos, Data.CuttingSize를 셰이더에 전달
}
```

### 3. 성능 개선 효과

**이전 방식: 개별 파일 방식**
- 텍스처 교체: 프레임당 1회 (비용 높음)
- Draw Call: 프레임 수만큼 증가
- 메모리: 개별 텍스처들의 합

**현재 방식: 스프라이트 시트**
- 텍스처 교체: 0회 (동일 텍스처 재사용)
- Draw Call: 배치 가능
- 메모리: 단일 텍스처 크기

**결과:**
- 16프레임 애니메이션 렌더링 시 Draw Call 16회 → 1회로 감소

</br>

### 4. 유지보수성 향상

**변경 전:**
```cpp
// 스프라이트 시트 수정 시 50줄의 코드를 전부 재작성
SpriteData[0].CuttingPos = { 0.0f, 0.0f };
SpriteData[0].CuttingSize = { 64.0f / 1024.0f, 64.0f / 1024.0f };
SpriteData[1].CuttingPos = { 64.0f / 1024.0f, 0.0f };
// ... 48줄 더
```

**변경 후:**
```cpp
// Unity에서 스프라이트 시트 수정 후 .smeta 파일 덮어쓰기만 하면 끝
UEngineSprite::CreateSpriteToMeta("Character.png", ".smeta");
```

</br>

### 5. 크로스 플랫폼 에셋 공유

```
Unity 프로젝트 (스프라이트 편집)
        ↓
    .smeta 내보내기
        ↓
DirectX 프로젝트 (자동 파싱)
        ↓
   게임에서 사용
```

**이점:**
- Unity의 강력한 스프라이트 편집 도구 활용


</br>

## 📊 핵심 성과 요약

| 항목 | 개선 전 | 개선 후 | 개선율 |
|------|---------|---------|--------|
| 스프라이트 설정 시간 | 수동 입력| 자동 파싱 | 편의성 향상 |
| 좌표 입력 오류율 | 약 5 ~ 10% | 0% | 100% 감소 |
| Draw Call (16프레임) | 16회 | 1회 | 94% 감소 |
| 리소스 파이프라인 | Unity → 수작업 → DX | Unity → DX | 편의성 향상 |

</br>

### [UE5 액션] [리팩토링] CPU 성능 최적화: ```Tick``` 의존성 해소, 이벤트 기반(Event-Driven Architecture)으로의 전환
### 🎮 목표

Tick 사용을 최소화하고 **이벤트 기반**으로 게임 로직 구성하기


### 💭 고민

**"Tick에 익숙해진 습관"**

기존 프로젝트에서 Tick 의존도:
- WinAPI: 거의 모든 로직
- DirectX: FSM의 ```ComponentTick```
- UE5 초기: 여전히 Tick 남용

이면에는 Tick은 직관적이고 "**이벤트 기반은 낯설다**"는 생각이 있었습니다.

**성능 문제 경험:**
```cpp
// WinAPI 시절 실수
void Player::Tick()
{
    UpdateUI();  // 매 프레임 UI 리소스 갱신
    // 결과: 800fps → 150fps ❌
}
```

이번 프로젝트는 철저히 **Timer, Delegate, AnimNotify** 활용을 목표로 했습니다.

</br>

**AnimNotify의 함정**

초기엔 ```AnimNotify```가 너무 편해서 남용:
```cpp
// 공격 종료 시 상태 초기화
AnimNotify_RemoveGameplayTag → RemoveState(Attacking)
```

**문제 발생:**
- 공격 중 회피 → 몽타주 중단 → ```AnimNotify_RemoveGameplayTag``` 미호출 ❌
- 블렌드 아웃 중 끝부분 Notify 누락
- ```Character_State_Attacking``` 영구 유지 → 캐릭터 이동 불가

**깨달음: "AnimNotify는 호출을 보장하지 않는다"**

</br>

### 🔧 해결 방법

**1. 중요 로직은 Delegate로 보장**
```cpp
// Before: AnimNotify (불안정)
AnimNotify_AttackEnd → 상태 초기화

// After: FOnMontageEnded (안전)
void ASoulCharacterBase::DoAttack(...)
{
    FOnMontageEnded OnMontageEnded;
    OnMontageEnded.BindUObject(this, &ThisClass::RecoveryAttack);
    
    AnimInstance->Montage_Play(AttackMontage);
    AnimInstance->Montage_SetEndDelegate(OnMontageEnded, AttackMontage);
}

void ASoulCharacterBase::RecoveryAttack(UAnimMontage* Montage, bool bInterrupted)
{
    // 중단되든 정상 종료든 무조건 호출 ✅
    RemoveState(SoulGameplayTag::Character_State_Attacking);
}
```

**2. UI는 Delegate로 분리**
```cpp
// Before: UI가 Component 직접 참조
void UHealthBarWidget::NativeTick()
{
    AttributeComp = GetOwner()->GetComponent();
    UpdateHealth(AttributeComp->GetHealth());  // 매 프레임 ❌
}
```
```cpp
// After: Delegate 구독
void UAttributeComponent::TakeDamageAmount(float Damage)
{
    BaseHealth -= Damage;
    OnAttributeChanged.Broadcast(EAttributeType::Health, BaseHealth, MaxHealth);
}

void UStatBarWidget::BindDelegate()
{
    AttributeComponent->OnAttributeChanged.AddDynamic(
        this, &UStatBarWidget::SetPercent);
}
```

</br>

**3. 역할별 이벤트 활용**

| 상황 | Tick (Before) | 이벤트 (After) |
|------|---------------|----------------|
| 스태미나 회복 | 매 프레임 체크 | ```Timer``` (회복 주기) |
| 상태 해제 | bool 변수 체크 | ```Delegate``` |
| UI 갱신 | 매 프레임 조회 | ```Delegate``` (변경 시만) |
| 충돌 검사 | 매 프레임 | ```AnimNotifyState``` (구간 지정) |
| 무적 부여 | bool + Tick | ```AnimNotifyState``` (Begin/End) |

</br>

**최종 Tick 사용처:**
```cpp
// WeaponCollisionComponent.cpp - 충돌 검사만
void UWeaponCollisionComponent::TickComponent(float DeltaTime, ...)
{
    if (bIsCollisionEnabled)  // 공격 중에만 활성화
    {
        CollisionTrace();  // 무기 궤적 추적
    }
}

// TargetingComponent.cpp - 락온 유지
void UTargetingComponent::TickComponent(float DeltaTime, ...)
{
    if (bIsLockOn && IsValid(LockedTargetActor))
    {
        FaceLockOnActor();  // 시선 고정
    }
}
```

**온/오프 제어로 최적화:**
```cpp
void ActivateCollision()
{
    WeaponCollisionComponent->SetComponentTickEnabled(true);
}

void DeactivateCollision()
{
    WeaponCollisionComponent->SetComponentTickEnabled(false);
}
```

</br>

### ✅ 결과

✅ **Tick 사용 최소화**: AI 외 거의 미사용  
✅ **명확한 실행 타이밍**: "언제" 호출되는지 코드로 명시  
✅ **디버깅 용이**: Delegate/Timer는 호출 시점 추적 쉬움  
✅ **성능 향상**: 불필요한 매 프레임 체크 제거

Tick의 함정:
- 매 프레임 실행 = 성능 낭비
- "언제" 실행되는지 불명확
- bool 변수 남발

이벤트 기반의 장점:
- **Timer**: "3초 후 실행" 명확
- **Delegate**: "HP 변경 시 UI 갱신" 명확
- **AnimNotify**: "공격 30프레임에 충돌 활성화" 명확

AnimNotify는 "**타이밍 이벤트**"로만 사용하고, "**상태 관리**"는 Delegate로 보장하는 것이 안전합니다. 언리얼의 이벤트 시스템을 적극 활용하면 코드가 더 명확하고 유지보수가 쉬워집니다.

___

### [Dedicated Server] 네트워크 복제 대역폭 최적화: ```Fast Array Serializer```를 활용한 배열 요소 단위 델타 복제(Delta Replication)
### 🎮 구현 목표

로비에서 플레이어 목록을 실시간으로 동기화합니다. 누군가 입장/퇴장하거나 준비 버튼을 누를 때마다 **변경된 플레이어 정보만** 네트워크로 전송하여 대역폭을 절약합니다.

</br>

### 🚨 문제 상황

**배열 전체 복제의 낭비**

일반적인 ```TArray``` Replication:
````cpp
UPROPERTY(Replicated)
TArray<FLobbyPlayerInfo> PlayerList;  // 10명 전체 복제
````

문제:
````
상황: 10명 접속 중, 1명이 준비 버튼 클릭
   ↓
Replicated Array 감지: "배열이 변경됨!"
   ↓
네트워크 전송: 10명 전체 정보 복제 ❌
   ↓
실제 필요: 1명 정보만 업데이트하면 충분
````

**실제 측정 결과:**
````
상황: 플레이어 10명, 각 정보 100바이트
- 일반 복제: 1,000바이트 전송 (10명 × 100바이트)
- 필요한 양: 100바이트 (1명만)
→ 900바이트 낭비 (90%) ❌
````

로비에서 준비 버튼을 연타하거나, 플레이어가 빈번하게 입/퇴장하면 **불필요한 전송이 급격히 증가**합니다.

</br>

### 💭 해결 방법

**Fast Array Serializer: "변경된 것만 보낸다"**

핵심 아이디어:
- 배열 원소마다 "변경 여부" 추적
- 변경된 원소만 ```MarkItemDirty()```로 표시
- 언리얼이 자동으로 변경된 것만 복제

**1. 구조체에 FastArraySerializer 상속**
````cpp
// LobbyPlayerInfo.h
USTRUCT(BlueprintType)
struct FLobbyPlayerInfo : public FFastArraySerializerItem
{
    GENERATED_BODY()

    UPROPERTY()
    FString Username{};

    UPROPERTY()
    bool bIsReady = false;

    // 변경 콜백
    void PostReplicatedAdd(const FLobbyPlayerInfoArray& InArraySerializer);
    void PreReplicatedRemove(const FLobbyPlayerInfoArray& InArraySerializer);
    void PostReplicatedChange(const FLobbyPlayerInfoArray& InArraySerializer);
};
````
```cpp
USTRUCT()
struct FLobbyPlayerInfoArray : public FFastArraySerializer
{
    GENERATED_BODY()

    UPROPERTY()
    TArray<FLobbyPlayerInfo> Items;

    UPROPERTY()
    AGameState* GameState;

    // 필수 함수
    bool NetDeltaSerialize(FNetDeltaSerializeInfo& DeltaParams)
    {
        return FastArrayDeltaSerialize<FLobbyPlayerInfo, FLobbyPlayerInfoArray>(
            Items, DeltaParams, *this);
    }

    void AddPlayer(const FLobbyPlayerInfo& NewPlayerInfo);
    void RemovePlayer(const FString& Username);
    void SetPlayerReady(const FString& Username, bool IsReady);
};

// 필수 템플릿 특수화
template<>
struct TStructOpsTypeTraits<FLobbyPlayerInfoArray> 
    : public TStructOpsTypeTraitsBase2<FLobbyPlayerInfoArray>
{
    enum { WithNetDeltaSerializer = true };
};
```

**2. GameState에서 사용**
````cpp
// DS_GameState.h
UCLASS()
class ADS_GameState : public AGameState
{
    GENERATED_BODY()

public:
    UPROPERTY(ReplicatedUsing = OnRep_PlayerList)
    FLobbyPlayerInfoArray PlayerList;

    UPROPERTY(BlueprintAssignable)
    FOnPlayerListUpdated OnPlayerListUpdated;
````
```cpp
void ADS_GameState::OnRep_PlayerList()
{
	PlayerList.SetOwner(this);
	OnPlayerListUpdated.Broadcast(); // UI 갱신
}
};
```

**3. 플레이어 추가/제거/수정**
````cpp
// LobbyPlayerInfo.cpp
void FLobbyPlayerInfoArray::AddPlayer(const FLobbyPlayerInfo& NewPlayerInfo)
{
    int32 Index = Items.Add(NewPlayerInfo);
    
    // 핵심: 추가된 원소만 Dirty 표시
    MarkItemDirty(Items[Index]);
    
    // 서버에서도 콜백 호출 (UI 갱신용)
    Items[Index].PostReplicatedAdd(*this);
}

void FLobbyPlayerInfoArray::SetPlayerReady(const FString& Username, bool IsReady)
{
    for (FLobbyPlayerInfo& PlayerInfo : Items)
    {
        if (PlayerInfo.Username == Username)
        {
            PlayerInfo.bIsReady = IsReady;
            
            // 핵심: 변경된 원소만 Dirty 표시
            MarkItemDirty(PlayerInfo);
            break;
        }
    }
}

void FLobbyPlayerInfoArray::RemovePlayer(const FString& Username)
{
    for (int32 PlayerIndex = 0; PlayerIndex < Items.Num(); ++PlayerIndex)
    {
        FLobbyPlayerInfo& PlayerInfo = Items[PlayerIndex];
        if (PlayerInfo.Username == Username)
        {
            PlayerInfo.PreReplicatedRemove(*this);
            Items.RemoveAtSwap(PlayerIndex);
            
            // 삭제는 배열 구조 변경이므로 전체 Dirty
            MarkArrayDirty();
            break;
        }
    }
}
````

**4. 클라이언트에서 변경 감지 (UI 갱신)**
````cpp
// LobbyPlayerInfo.cpp
void FLobbyPlayerInfo::TriggerUpdate(const FLobbyPlayerInfoArray& InArraySerializer)
{
    if (ADS_GameState* GameState = Cast<ADS_GameState>(InArraySerializer.GetOwner()))
    {
        // Delegate 발행 → UI 자동 갱신
        GameState->OnPlayerListUpdated.Broadcast();
    }
}

void FLobbyPlayerInfo::PostReplicatedAdd(const FLobbyPlayerInfoArray& InArraySerializer)
{
    // 새 플레이어 추가됨
    UE_LOG(LogTemp, Log, TEXT("Player joined: %s"), *Username);
    TriggerUpdate(InArraySerializer);
}

void FLobbyPlayerInfo::PostReplicatedChange(const FLobbyPlayerInfoArray& InArraySerializer)
{
    // 플레이어 정보 변경됨 (준비 상태 등)
    UE_LOG(LogTemp, Log, TEXT("Player ready changed: %s = %d"), *Username, bIsReady);
    TriggerUpdate(InArraySerializer);
}

void FLobbyPlayerInfo::PreReplicatedRemove(const FLobbyPlayerInfoArray& InArraySerializer)
{
    // 플레이어 퇴장
    UE_LOG(LogTemp, Log, TEXT("Player left: %s"), *Username);
    TriggerUpdate(InArraySerializer);
}
````

**동작 흐름:**
````
[서버]
1. Player A 준비 버튼 클릭
2. PlayerList.SetPlayerReady("PlayerA", true)
3. Items[0].bIsReady = true
4. MarkItemDirty(Items[0])  ← 0번만 Dirty 표시
   ↓
[네트워크]
5. Items[0] 정보만 전송 (100바이트) ✅
   ↓
[클라이언트]
6. PostReplicatedChange() 호출
7. OnPlayerListUpdated.Broadcast()
8. UI 위젯: "PlayerA [준비 완료]" 표시
````

</br>

### 🔧 시행착오

**Owner 설정 누락**
```PostReplicatedAdd()``` 콜백에서 GameState에 접근하려 했지만 ```nullptr``` 크래시:
```cpp
void FLobbyPlayerInfo::PostReplicatedAdd(...)
{
    // ❌ InArraySerializer.GameState가 nullptr
    ADS_GameState* GS = Cast<ADS_GameState>(InArraySerializer.GameState);
}
```

**해결:** ```BeginPlay()```와 ```OnRep_PlayerList()```에서 Owner 설정:
```cpp
void ADS_GameState::BeginPlay()
{
    if (HasAuthority())
    {
        PlayerList.SetOwner(this);  // 서버
    }
}

void ADS_GameState::OnRep_PlayerList()
{
    PlayerList.SetOwner(this);  // 클라이언트
}
```

</br>

### ✅ 결과

✅ **네트워크 대역폭 90% 절감**: 10명 중 1명만 변경 시 100바이트만 전송  
✅ **자동 UI 동기화**: ```PostReplicatedChange()``` 콜백으로 UI 자동 갱신  
✅ **확장성**: 준비 상태뿐 아니라 팀 선택, 캐릭터 선택 등 추가 가능

**"배열 복제는 Fast Array Serializer로"**

일반 ```TArray``` Replication:
- 배열 변경 시 전체 전송
- 10명 중 1명 변경 = 10명 전송
- 대역폭 낭비

Fast Array Serializer:
- 변경된 원소만 전송
- 10명 중 1명 변경 = 1명 전송
- ```MarkItemDirty()```만 추가하면 끝

___

### 2-6. 회고
### ```PlayerController```가 입력을 처리하는게 적절한가?

### 🤔 초기 설계 의도

**"Controller의 역할은 입력을 처리하는 것이 아닌가?"**

`PlayerController`의 본연 기능이 입력 처리라고 생각했기에, 모든 입력을 Controller에서 받도록 설계했습니다:
```cpp
// SoulPlayerControllerBase.cpp
void ASoulPlayerControllerBase::SetupInputComponent()
{
    // 모든 입력을 Controller에 바인딩
    EnhancedInputComp->BindAction(MoveAction, ETriggerEvent::Triggered, this, &ThisClass::Move);
    EnhancedInputComp->BindAction(AttackAction, ETriggerEvent::Started, this, &ThisClass::Attack);
    EnhancedInputComp->BindAction(RollingAction, ETriggerEvent::Started, this, &ThisClass::Rolling);
    // ... 30개 이상의 입력
}
```

**책임 소재가 명확해 보였습니다:**
- Controller: 입력 받기
- Character: 행동 실행

</br>

### 🚨 문제 인식

**Controller는 단순 중계자일 뿐**

그러나 실제 코드를 보면 **Controller는 아무것도 하지 않습니다:**
```cpp
// SoulPlayerControllerBase.cpp - 반복되는 패턴
void ASoulPlayerControllerBase::Attack()
{
    if (ASoulPlayerCharacter* SoulCharacter = Cast<ASoulPlayerCharacter>(GetCharacter()))
    {
        SoulCharacter->Attack();  // 그냥 전달만
    }
}

void ASoulPlayerControllerBase::Rolling()
{
    if (ASoulPlayerCharacter* SoulCharacter = Cast<ASoulPlayerCharacter>(GetCharacter()))
    {
        SoulCharacter->Rolling();  // 그냥 전달만
    }
}

void ASoulPlayerControllerBase::HeavyAttack()
{
    if (ASoulPlayerCharacter* SoulCharacter = Cast<ASoulPlayerCharacter>(GetCharacter()))
    {
        SoulCharacter->HeavyAttack();  // 그냥 전달만
    }
}

// ... 30개 함수가 모두 동일한 패턴 ❌
```

**실제 입력 흐름:**
```
입력 → Controller::Attack() 
       ↓ (캐스팅 + 전달)
     Character::Attack()
       ↓ (다시 전달)
     CombatComponent::Attack()
       ↓ (실제 로직)
     DoAttack()
```

**3단계를 거쳐야 실제 로직 도달** ❌

**관찰한 문제점:**

1. **Controller는 입력 토스하기 바쁨**
   - 이동 → CharacterMovementComponent
   - 공격 → CombatComponent
   - 인벤토리 → InventoryUI
   - UI 모드 전환 → WidgetManager

2. **Controller가 모든 클래스를 알아야 함**
```cpp
// Controller가 알아야 하는 것들
ASoulPlayerCharacter* Character;
UCombatComponent* CombatComp;
UAttributeComponent* AttributeComp;
UStateComponent* StateComp;
UInventoryComponent* InventoryComp;
UWidgetManagerComponent* WidgetManager;
// ... 계속 증가
```

3. **결합도 폭발**
   - CombatComponent 수정 → Controller도 수정 필요
   - 새 기능 추가 → Controller에 함수 추가
   - "책임 소재 명확"하지만 실제론 **God Class** ❌

</br>

### 💭 고민의 흐름

**고민 1: "Controller의 결합도를 낮추려면?"**

Character로 위임했지만, **Character도 같은 고민**:
```cpp
// SoulPlayerCharacter.cpp
void ASoulPlayerCharacter::Attack()
{
    if (CombatComponent)
    {
        CombatComponent->Attack();  // 또 전달
    }
}
```

**결국 "입력 → Controller → Character → Component" 3단계 불필요한 중계**

</br>

**고민 2: "무기별로 다른 입력을 어떻게 처리할까?"**

Q키를 눌렀을 때:
- 한손검: 즉발 특수 공격
- 대검: 차징 공격
- 폴암: 원거리 투척

**시도했던 방법들:**

**A안: Character에서 Switch 문**
```cpp
void ASoulPlayerCharacter::SpecialAttack()
{
    ECombatType CombatType = CombatComponent->GetWeapon()->GetCombatType();
    
    switch (CombatType)
    {
    case ECombatType::Sword:
        CombatComponent->SpecialAttack();
        break;
    case ECombatType::GreatSword:
        CombatComponent->ChargeAttack();
        break;
    case ECombatType::Polearm:
        CombatComponent->ThrowWeapon();
        break;
    }
}
```
❌ Character가 모든 무기 타입을 알아야 함  
❌ 무기 추가 시마다 Switch 문 수정

**B안: Delegate로 태그만 전달?**
```cpp
// Controller
void ASoulPlayerControllerBase::SpecialAttack()
{
    OnInputReceived.Broadcast(SoulGameplayTag::Input_SpecialAttack);
}

// Character
void ASoulPlayerCharacter::OnInputReceived(FGameplayTag InputTag)
{
    switch (InputTag)
    {
    case Input_SpecialAttack:
        // 무기 타입에 따라 분기
        break;
    }
}
```
❌ 결국 Character의 Switch 문은 동일  
❌ 추상화했지만 근본적 해결 아님

**C안: 무기가 IMC를 가지고 장착 시 전달?**
```cpp
// 상상 속 코드
void ASoulWeapon::EquipItem()
{
    Character->AddMappingContext(WeaponSpecificIMC);  
    // Q키 → 차징 공격으로 자동 매핑
}
```
✅ 무기마다 다른 입력 가능  
❌ 구현 복잡도 높음, Enhanced Input 이해 필요  
❓ **"이게 과연 올바른 방법일까?"** → 막막함

</br>

### 💡 깨달음: "입력의 소비자에게 책임을"

**왜 ```ACharacter::SetupPlayerInputComponent()```가 존재하는가?**

언리얼 공식 문서와 커뮤니티를 찾아보며 알게 된 사실:

> **"PlayerController는 '플레이어의 의지'를 대변하고,  
> Pawn은 '그 의지를 수행하는 육체'다."**

**빙의(Possess)의 의미:**
- Controller가 Pawn에 빙의한다 = 의지(Controller)와 육체(Pawn) 분리
- 입력을 **'받는' 곳**과 **'소비하는' 곳**을 분리하는 설계 철학

**핵심 인사이트:**
```
❌ Controller: "공격 입력 → 공격 실행"
✅ Controller: "공격 입력 수신" / Pawn: "공격 실행"
```

</br>

### 🔧 접근 방법

**1. Enhanced Input + IMC**

**무기가 IMC를 소유하는 방식:**
```cpp
// SoulWeapon.h
UCLASS()
class ASoulWeapon
{
    UPROPERTY(EditDefaultsOnly)
    UInputMappingContext* WeaponInputContext;  // 무기별 IMC
};

// SoulWeapon.cpp - 장착 시
void ASoulWeapon::EquipItem()
{
    if (APlayerController* PC = Character->GetController<APlayerController>())
    {
        if (UEnhancedInputLocalPlayerSubsystem* Subsystem = 
            ULocalPlayer::GetSubsystem<UEnhancedInputLocalPlayerSubsystem>(PC->GetLocalPlayer()))
        {
            // 무기 전용 입력 추가
            Subsystem->AddMappingContext(WeaponInputContext, 1);
        }
    }
}

// IMC_Sword.asset
// Q키 → IA_ChargeAttack

// IMC_Axe.asset  
// Q키 → IA_QuickAttack
```

**흐름:**
```
1. 검 장착 → IMC_Sword 추가
   Q키 = IA_ChargeAttack 매핑
   
2. 도끼 장착 → IMC_Sword 제거 + IMC_Axe 추가
   Q키 = IA_QuickAttack 매핑
   
3. Controller는 "Q가 눌렸다"만 알 뿐, 
   차징인지 즉발인지는 무기의 IMC가 결정
```

**장점:**
- ✅ Controller는 무기 타입을 몰라도 됨
- ✅ 무기 추가 시 코드 수정 0줄
- ✅ IMC Asset만 만들면 끝
- ✅ 결합도 완전 분리

</br>

**2. GameplayTag + Delegate**

**입력을 '의도'로 추상화:**
```cpp
// PlayerController
DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnInputIntent, FGameplayTag, IntentTag);

void ASoulPlayerController::SpecialAttack()
{
    // 무기/캐릭터를 모름, 태그만 방송
    OnInputIntent.Broadcast(GameplayTag::Input_SpecialAttack);
}

// CombatComponent
void UCombatComponent::BeginPlay()
{
    // 태그 구독
    PlayerController->OnInputIntent.AddDynamic(this, &ThisClass::OnInputReceived);
}

void UCombatComponent::OnInputReceived(FGameplayTag IntentTag)
{
    if (IntentTag == GameplayTag::Input_SpecialAttack)
    {
        // 현재 무기에 맞는 행동 실행
        Weapon->ExecuteSpecialAttack();
    }
}
```

**장점:**
- ✅ Controller는 의도만 전달
- ✅ 여러 시스템이 동시에 구독 가능

</br>

**3. Character에서 직접 입력 처리 (가장 단순)**
```cpp
// SoulPlayerCharacter.cpp
void ASoulPlayerCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    UEnhancedInputComponent* EnhancedInput = Cast<UEnhancedInputComponent>(PlayerInputComponent);
    
    // Controller 거치지 않고 직접 바인딩
    EnhancedInput->BindAction(AttackAction, ETriggerEvent::Started, this, &ThisClass::Attack);
    EnhancedInput->BindAction(RollingAction, ETriggerEvent::Started, this, &ThisClass::Rolling);
}
```

**Controller는 시스템 입력만:**
```cpp
// SoulPlayerController.cpp
void ASoulPlayerController::SetupInputComponent()
{
    // UI/시스템만
    EnhancedInput->BindAction(PauseAction, ETriggerEvent::Started, this, &ThisClass::Pause);
    EnhancedInput->BindAction(InventoryAction, ETriggerEvent::Started, this, &ThisClass::OpenInventory);
}
```

**장점:**
- ✅ 불필요한 중계 함수 제거
- ✅ 디버깅 용이 (Character만 확인)
- ✅ AI도 Character 함수 직접 호출

</br>

### ✅ 결론: PlayerController의 진짜 역할

**현재 구조의 문제:**
```
❌ PlayerController = "입력 처리자" (God Class)
   → 모든 시스템을 알아야 함
   → 결합도 폭발
   → 중계 함수 30개
```

**올바른 구조:**
```
✅ PlayerController = "입력 관리자" (Input Manager)
   → IMC 추가/제거 관리
   → 의도(Tag)로 변환하여 방송
   → UI/시스템 기능만 직접 처리
```

**책임 분리:**
- **Controller**: 누가 조종하는가 (Possess/Unpossess), 입력 컨텍스트 관리
- **Character**: 무엇을 할 수 있는가 (Move/Attack/Roll), 입력 직접 처리
- **Component**: 어떻게 하는가 (로직 구현)

"**입력을 '처리'하는 것과 '관리'하는 것은 다르다**"

Controller가 모든 입력을 처리하는 것은:
- ❌ 교과서적이지만 확장성 낮음
- ❌ 중계 함수만 늘어남
- ❌ 결합도 문제

Enhanced Input의 IMC나 GameplayTag를 활용하면:
- ✅ Controller는 "입력 컨텍스트 관리자"
- ✅ Character/Component는 "입력 소비자"
- ✅ 무기/스킬 추가 시 코드 수정 불필요

**다음 프로젝트에서는:**
1. Character에서 직접 입력 처리 (기본)
2. 무기별 IMC로 동적 매핑 (확장)
3. Controller는 UI/시스템만 담당
```ACharacter::SetupPlayerInputComponent()```가 존재하는 이유는 "**행동의 주체가 직접 입력을 받는 게 자연스럽다**"

</br>

___

### [리팩토링] OCP(개방 폐쇄 원칙) 기반 설계: 상속에서 인터페이스로 전환

### 🤔 초기 설계: "공통점이 많으니 Base로 관리하자."

프로젝트 초기, `ASoulCharacterBase`를 설계할 때 저는 확신에 차 있었습니다.

`Player`와 `Enemy`는 공격, 피격, 사망 등 공통 로직이 80% 이상이었기 때문입니다.

- 공통 시스템: 공격, 피격, 방어, 사망
- 공통 컴포넌트: Attribute, Combat, State
- 공통 로직: 데미지 계산, 히트 리액션

```cpp
// 공통 로직은 Base에!
class ASoulCharacterBase : public ACharacter, public ISoulCombat
{
protected:
    // 공통 컴포넌트
    UAttributeComponent* AttributeComponent;
    UCombatComponent* CombatComponent;
    UStateComponent* StateComponent;
    
public:
    // 공통 함수
    virtual float TakeDamage(...);
    void HitReaction(...);
    void DoAttack(...);
};

// 상속 구조
ASoulPlayerCharacter : public ASoulCharacterBase
ASoulEnemy : public ASoulCharacterBase
```

기대했던 장점
- ✅ 코드 중복 제거
- ✅ 유지보수 용이 (Base만 수정하면 모두에게 적용)
- ✅ 상속의 이점 극대화 (코드 재사용성)

"Base 클래스에서 한 번만 정의하면 모든 자식이 공짜로 기능을 쓴다." 이 강력한 코드 재사용성(Code Reusability) 덕분에 개발 속도는 빨랐고, 유지보수도 쉬워 보였습니다.

하지만 개발이 진행될수록, 이 '편리함'에 점점 의구심을 갖기 시작했습니다.
</br>

### 🚨 문제 인식
문제는 `Player`와 `Enemy`의 로직이 미세하게 갈라지기 시작한 시점부터였습니다.

#### 딜레마 1: 버려지는 프로퍼티 (Bloated Base Class)
```cpp
class ASoulCharacterBase
{
    // ❓ Enemy는 평생 쓰지도 않을 메모리 낭비
    UCameraComponent* Camera; 
    UInventoryComponent* Inventory;
    TSubclassOf<UCameraShake> HitShake; 
};
```
`Enemy` 인스턴스가 생성될 때마다 사용하지도 않는 카메라와 인벤토리 포인터를 들고 있는 상황. **"Base 클래스가 쓸데없이 비대해지고 있다"**는 신호였습니다.

#### 딜레마 2: 로직의 분기 (Spawn of Spaghetti)
`TakeDamage`는 공통 로직이지만, 세부 동작이 달랐습니다.
- `Player`: 카메라 셰이크 필요
- `Enemy`: AI에게 데미지 알림 필요

```cpp
// ASoulCharacterBase.h
class ASoulCharacterBase
{
protected:
    // 🚨 Player 전용 - Enemy는 빈 구현
    virtual void ClientStartCameraShake(ECameraShakeType ShakeType) {}
    
    // 🚨 Enemy 전용 - Player는 빈 구현
    virtual void TakeDamageForEnemy(float Damage, AController* EventInstigator, 
                                     const FVector& EventLocation, const FVector& HitLocation) {}
    
public:
    virtual float TakeDamage(float Damage, const FDamageEvent& DamageEvent, 
                            AController* EventInstigator, AActor* DamageCauser) override
    {
        // 공통 로직
        float FinalDamage = CalculateDamage(Damage);
        
        // 🚨 누군가는 쓰고 누군가는 안 쓰는 코드
        ClientStartCameraShake(ECameraShakeType::Hit);       // Player만
        TakeDamageForEnemy(Damage, EventInstigator, ...);    // Enemy만
        
        // 공통 로직
        AttributeComponent->TakeDamageAmount(FinalDamage);
        return FinalDamage;
    }
};
```
```cpp
// 시간이 지날수록 점점 늘어나는 분기점들...

void ASoulCharacterBase::HitReaction(...)
{
    PlayHitAnimation();                    // 공통
    
    OnPlayerHitEffect();                   // Player만 (빈 함수)
    OnEnemyHitEffect();                    // Enemy만 (빈 함수)
    
    ApplyKnockback();                      // 공통
    
    OnPlayerCameraShake();                 // Player만 (빈 함수)
    OnEnemyUIUpdate();                     // Enemy만 (빈 함수)
    
    SetState(SoulGameplayTag::Hit);        // 공통
}

공통 로직 (Step 1)
    ↓
빈 가상 함수 호출 (Player 전용)  ← Enemy는 빈 함수 실행
    ↓
공통 로직 (Step 2)
    ↓
빈 가상 함수 호출 (Enemy 전용)   ← Player는 빈 함수 실행
    ↓
공통 로직 (Step 3)
    ↓
빈 가상 함수 호출 (...)
    ↓
   ...
```
갈수록 이러한 늘어나면서 부모 클래스는 점점 관리가 복잡해지는 코드가 되어갔습니다.

</br>

### 💭 고민 : "전방위적인 결합도 증가"

이 불안함은 **시스템 간의 연결(Coupling)**을 다룰 때 폭발했습니다.

#### 의문 1: AnimNotify가 왜 캐릭터를 알아야 하지?

`AnimNotify`에서 충돌 판정을 켤 때, Cast<ASoulCharacterBase>를 사용하고 있었습니다.

만약 나중에 **"공격 가능한 오브젝트(예: 함정, 포탑)"**가 추가된다면? `ASoulCharacterBase`를 상속받지 않은 그들은 이 노티파이를 쓸 수 없습니다. 

**불필요한 결합**이 발생한 것입니다.

```cpp
// Before: 구체적인 타입에 의존
void UAnimNotify_ActivateCollision::Notify(USkeletalMeshComponent* MeshComp, ...)
{
    if (ASoulCharacterBase* Character = Cast<ASoulCharacterBase>(MeshComp->GetOwner()))
    {
        Character->ActivateCollision(CollisionType, DamageType);
    }
}
```

```cpp
// ATrapTower.h - 포탑 추가
class ATrapTower : public AActor  // ❌ ASoulCharacterBase를 상속받지 않음
{
    // 공격 기능이 필요한데...
    // AnimNotify_ActivateCollision을 쓸 수 없다!
};
```
결과:
- 함정, 포탑 같은 "공격 가능한 오브젝트" 추가 시
- `ASoulCharacterBase`를 상속받지 않으면 기존 `AnimNotify` 사용 불가
- 새로운 `AnimNotify`를 또 만들어야 함 → 코드 중복 발생

</br>

#### 의문 2: Manager 클래스는 정답인가?
컴포넌트 간의 참조가 복잡해지자(Inventory ↔ UI ↔ Combat), 저는 `WidgetManager` 같은 관리자 클래스에 의존성을 몰아넣었습니다. 
```cpp
// 복잡한 의존성 그래프
InventoryComponent ↔ InventoryWidget
        ↕
  CombatComponent ↔ StatusWidget
        ↕
 AttributeComponent ↔ StatBarWidget
```

하지만 이것도 미봉책이었습니다. "`AnimNotify`에게 함수를 전달하기 위해 또 Manager를 만들어야 하나?" 

모든 문제를 Manager로 해결하려다 보니, 또 다른 거대 클래스(God Class)를 만들고 있었습니다.

</br>

#### 의문 3: "만약 전투 컨텐츠 이외로 확장이 된다면?"
지금은 전투 게임이지만, 만약 대화만 가능한 NPC가 추가된다면? 

그 NPC가 `ASoulCharacterBase`를 상속받으면 체력, 공격력, 전투 로직까지 억지로 떠안게 됩니다. 

그렇다고 상속을 안 받자니, 상호작용 로직을 또 새로 짜야 합니다.
```cpp
// ANPCCharacter.h - 대화만 가능한 NPC
class ANPCCharacter : public ASoulCharacterBase  // ❌ 강제 상속
{
    // 🚨 억지로 떠안게 되는 것들
    UAttributeComponent* AttributeComponent;  // 체력? 필요 없는데...
    UCombatComponent* CombatComponent;        // 공격? 필요 없는데...
    
    virtual float TakeDamage(...) override { return 0.f; }  // 빈 구현 강제
    virtual void DoAttack(...) override { }                 // 빈 구현 강제
    
    // 실제로 필요한 건 이것뿐
    void StartDialogue();
};
```
"상속은 '정체성(Is-A)'을 강제하지만, 게임 개발에서 필요한 건 '기능(Can-Do)'의 확장이 아닐까?"

</br>

### 🔧 문제 해결 접근 방법 : 인터페이스를 통한 "기능 중심 설계"

저는 이 문제를 해결하기 위해 Base 클래스의 해체가 아닌, 인터페이스와의 공존을 선택했습니다.

#### ✅ 전략 1: "정체성"이 아닌 "능력"으로 대화하라

`AnimNotify`나 외부 시스템은 대상이 `ASoulCharacterBase`인지 알 필요가 없습니다. 그저 **"전투가 가능한가(ISoulCombat)?"**만 알면 됩니다.
```cpp
// ISoulCombat.h - 전투 능력 계약
UINTERFACE(MinimalAPI)
class USoulCombat : public UInterface
{
    GENERATED_BODY()
};

class SOUL_API ISoulCombat
{
    GENERATED_BODY()
    
public:
    // "나는 전투할 수 있다"는 계약
    virtual void ActivateCollision(EWeaponCollisionType CollisionType, TSubclassOf<UDamageType> DamageType) = 0;
    virtual void DeactivateCollision(EWeaponCollisionType CollisionType) = 0;
    virtual void DoAttack(const FGameplayTag& AttackTypeTag) = 0;
    virtual void HitReaction(AActor* Attacker, UDamageType* DamageType, const FVector& HitDirection) = 0;
};
```
```cpp
// Before : 구체적인 타입에 의존
void UAnimNotify_ActivateCollision::Notify(USkeletalMeshComponent* MeshComp, ...)
{
    // ❌ ASoulCharacterBase만 가능
    if (ASoulCharacterBase* Character = Cast<ASoulCharacterBase>(MeshComp->GetOwner()))
    {
        Character->ActivateCollision(CollisionType, DamageType);
    }
}

// After: 인터페이스에 의존
void UAnimNotify_ActivateCollision::Notify(USkeletalMeshComponent* MeshComp, ...)
{
    // 이제 포탑이든, 함정이든, 캐릭터든 ISoulCombat만 구현하면 작동한다.
    if (ISoulCombat* Combat = Cast<ISoulCombat>(Mesh->GetOwner())) 
    {
        Combat->ActivateCollision();
    }
}
```
```cpp
// 이제 포탑도 전투 가능!
class ATrapTower : public AActor, public ISoulCombat  // ✅ 인터페이스만 구현
{
    // ISoulCombat 구현
    virtual void ActivateCollision(...) override
    {
        // 포탑만의 충돌 로직
    }
    
    virtual void DoAttack(...) override
    {
        // 포탑만의 공격 로직
    }
    
    // ASoulCharacterBase의 무거운 로직은 필요 없음!
};
```
```cpp
┌──────────────────┐
│  AnimNotify      │
└────────┬─────────┘
         │ Cast<ISoulCombat>
         ↓
┌──────────────────────┐
│  <<interface>>       │
│  ISoulCombat         │ ← ✅ 추상 계약에 의존
└──────────────────────┘
         △
    ┌────┼────┬────┬────┐
    │    │    │    │    │
  Player Enemy 함정 포탑 Boss (자유로운 확장)
```
이로써 결합도가 획기적으로 낮아졌고, 추후 어떤 오브젝트가 추가되더라도 인터페이스만 구현하면 기존 시스템을 재사용할 수 있게 되었습니다.

</br>

#### ✅ 전략 2: Base 클래스는 "구현의 도우미"로 남겨라
Base 클래스를 버린 것이 아닙니다. 공통 로직(데미지 산출, 상태 관리)은 여전히 유효하기 때문입니다. 

대신, Base 클래스의 역할을 재정의했습니다.
```cpp
┌─────────────────────────────┐
│  1. Interface (계약)        │
│  "이 객체는 전투 가능하다"  │
└──────────────┬──────────────┘
               │
               ↓
┌─────────────────────────────┐
│  2. Base (공통 구현)        │
│  "계약에 대한 기본 구현"    │
└──────────────┬──────────────┘
               │
               ↓
┌─────────────────────────────┐
│  3. Child (특수화)          │
│  "Hook으로 1% 로직만"       │
└─────────────────────────────┘
```

- Interface (ISoulCombat): "이 객체는 공격과 피격이 가능하다"는 계약(Protocol) 정의.
- Base Class (ASoulCharacterBase): 계약에 대한 공통 구현(Default Implementation) 제공.
- Child Class (Player/Enemy): Hook 함수(OnHitReactionEffect)를 통해 자신만의 1% 로직만 오버라이딩.

```cpp
// ISoulCombat.h
class ISoulCombat
{
public:
    virtual void HitReaction(AActor* Attacker, UDamageType* DamageType, const FVector& HitDirection) = 0;
};
```
```cpp
// ASoulCharacterBase.h
class ASoulCharacterBase : public ACharacter, public ISoulCombat
{
protected:
    // 공통 컴포넌트
    UAttributeComponent* AttributeComponent;
    UCombatComponent* CombatComponent;
    
    // 🎯 Hook 함수: 자식이 필요하면 구현
    virtual void OnHitReactionEffect(AActor* Attacker) {}
    
public:
    // 공통 로직 구현
    virtual void HitReaction(AActor* Attacker, UDamageType* DamageType, const FVector& HitDirection) override 
    {
        // ✅ 공통 로직 90%
        PlayHitAnimation();
        ApplyKnockback(HitDirection);
        
        // 🎯 Hook: 자식만의 1% 로직 호출
        OnHitReactionEffect(Attacker);
        
        // ✅ 공통 로직 계속
        SetState(SoulGameplayTag::Character_State_Hit);
    }
};
```
```cpp
// ASoulPlayerCharacter.h
class ASoulPlayerCharacter : public ASoulCharacterBase, public IPlayerCharacter
{
protected:
    // Player만의 프로퍼티
    UCameraComponent* Camera;
    TSubclassOf<UCameraShakeBase> HitCameraShake;
    
    // 🎯 Hook 구현: Player만의 1% 로직
    virtual void OnHitReactionEffect(AActor* Attacker) override
    {
        // 카메라 셰이크 (Player 전용)
        ClientStartCameraShake(HitCameraShake);
    }
};

// ASoulEnemy.h
class ASoulEnemy : public ASoulCharacterBase, public IEnemy
{
protected:
    // Enemy만의 프로퍼티
    UWidgetComponent* HealthBar;
    
    // 🎯 Hook 구현: Enemy만의 1% 로직
    virtual void OnHitReactionEffect(AActor* Attacker) override
    {
        // 체력바 표시 (Enemy 전용)
        ToggleHealthBarVisibility(true);
    }
};
```
```cpp
HitReaction() 호출
    ↓
PlayHitAnimation()     // ✅ 공통 (Base)
    ↓
ApplyKnockback()       // ✅ 공통 (Base)
    ↓
OnHitReactionEffect()  // 🎯 Hook 호출
    ├─ Player: ClientStartCameraShake()  // Player만의 1%
    └─ Enemy: ToggleHealthBarVisibility() // Enemy만의 1%
    ↓
SetState()             // ✅ 공통 (Base)
```
Base 클래스의 공통 로직을 살리되, 더 포괄적인 항목의 가상 함수를 만들어 자식에서 재정의하는 방식을 사용했습니다.

</br>

#### 문제 인식

이제는 전투 관련 함수이지만, `Player`만 또는 `Enemy`만 사용하는 함수에 대한 구현을 올려놓아야 하는 고민이 남았습니다.

```cpp
// ❌ Fat Interface
class ISoulCombat
{
    // 공통
    virtual void DoAttack(...) = 0;
    virtual void HitReaction(...) = 0;
    
    // Player 전용
    virtual void ClientStartCameraShake(...) = 0;  // ❌ Enemy도 구현 강제
    virtual void AddItem(...) = 0;                 // ❌ Enemy도 구현 강제
    
    // Enemy 전용
    virtual void PerformAttack(...) = 0;           // ❌ Player도 구현 강제
    virtual void OnTargeted(...) = 0;              // ❌ Player도 구현 강제
};
```

아예 과감히 인터페이스를 세분화(ISP, Interface Segregation Principle)하기로 결정했습니다.

```cpp
// ISoulCombat.h - 전투 공통
class ISoulCombat
{
    virtual void DoAttack(const FGameplayTag& AttackTypeTag) = 0;
    virtual void HitReaction(AActor* Attacker, UDamageType* DamageType, const FVector& HitDirection) = 0;
    virtual void ActivateCollision(EWeaponCollisionType CollisionType, TSubclassOf<UDamageType> DamageType) = 0;
};

// IPlayerCharacter.h - Player 전용
class IPlayerCharacter
{
    virtual void BroadcastStatusMessage(const FString& Message) const = 0;
    virtual bool AddItem(const FName ItemID, const int32 Amount = 1, const int32 SlotIndex = -1) = 0;
    virtual void ClientStartCameraShake(TSubclassOf<UCameraShakeBase> ShakeClass) const = 0;
};

// IEnemy.h - Enemy 전용
class IEnemy
{
    virtual bool PerformAttack(FGameplayTag& AttackTypeTag, FOnMontageEnded& MontageEndedDelegate) = 0;
};

// ISoulTargeting.h - 타게팅 가능 객체
class ISoulTargeting
{
    virtual void OnTargeted(bool bTarget) = 0;
    virtual bool CanBeTargeted() = 0;
};
```
이제 Derived 클래스는 Base 클래스와 달리 더 많은 인터페이스를 상속받는 구조가 되었습니다.
```cpp
// Player: 필요한 인터페이스만 구현
class ASoulPlayerCharacter : public ASoulCharacterBase,   // 공통 구현
                            public IPlayerCharacter       // Player 전용
{
    // IPlayerCharacter 구현
    virtual void ClientStartCameraShake(...) override;
    virtual bool AddItem(...) override;
};

// Enemy: 필요한 인터페이스만 구현
class ASoulEnemy : public ASoulCharacterBase,   // 공통 구현
                  public IEnemy,                // Enemy 전용
                  public ISoulTargeting         // 타게팅 대상
{
    // IEnemy 구현
    virtual bool PerformAttack(...) override;
    
    // ISoulTargeting 구현
    virtual void OnTargeted(...) override;
    virtual bool CanBeTargeted() override;
};

        <<interface>>           <<interface>>           <<interface>>
        ┌─────────────┐         ┌─────────────┐         ┌─────────────┐
        │ ISoulCombat │         │IPlayerChar  │         │   IEnemy    │
        └──────┬──────┘         └──────┬──────┘         └──────┬──────┘
               │                       │                       │
               │                       │                       │
               └───────┬───────────────┴───────────────┬───────┘
                       │                               │
              ┌────────▽────────┐            ┌────────▽────────┐
              │     Player      │             │     Enemy       │
              │  ─────────────  │             │  ─────────────  │
              │ - Camera        │             │ - HealthBar     │
              │ - Inventory     │             │ - AI            │
              │  ─────────────  │             │  ─────────────  │
              │ + AddItem()     │             │ + PerformAttack │
              │ + CameraShake() │             │ + OnTargeted()  │
              └─────────────────┘             └─────────────────┘
                       △                               △
                       └───────────┬───────────────────┘
                                   │
                          ┌────────▽────────┐
                          │   CharBase      │
                          │  ─────────────  │
                          │ + HitReaction() │
                          │ + DoAttack()    │
                          └─────────────────┘
```

</br>

### ✅ 결론: 복잡성을 제어하는 힘

이번 리팩토링을 통해 얻은 깨달은 것은 다음과 같습니다.

1. 상속의 한계

- "상속은 코드 재사용을 위해 좋지만, 설계를 유연하게 만들지는 못한다"

이유:
- 상속은 부모-자식 간의 결합도가 가장 높은 형태
- 부모의 변경이 자식 전체에 영향
- 자식은 부모의 모든 것을 떠안음 (필요 없어도)

2. 인터페이스는 확장성을 위한 투자

- "당장은 코드가 늘어나는 것 같지만, 새로운 컨텐츠가 추가될 때 기존 코드를 수정하지 않고도 확장할 수 있는 길을 열어준다"

3. Base와 Interface는 양자택일이 아니다

- "Base로 중복을 줄이고, Interface로 결합도를 낮추는 하이브리드 설계가 실무적인 정답에 가깝다"



</br>

___


<h3 align="left">Connect with me:</h3>
<p align="left">
- Email: rjacjs0331@google.com  </p>
- Blog: https://kabu0129.tistory.com  </p>
<a href="https://www.youtube.com/c/kabu-y2u" target="blank"><img align="center" src="https://raw.githubusercontent.com/rahuldkjain/github-profile-readme-generator/master/src/images/icons/Social/youtube.svg" alt="kabu-y2u" height="30" width="40" /></a>
</p>

<h3 align="left">Languages and Tools:</h3>
<p align="left"> <a href="https://www.cprogramming.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/c/c-original.svg" alt="c" width="40" height="40"/> </a> <a href="https://www.w3schools.com/cpp/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/cplusplus/cplusplus-original.svg" alt="cplusplus" width="40" height="40"/> </a> <a href="https://git-scm.com/" target="_blank" rel="noreferrer"> <img src="https://www.vectorlogo.zone/logos/git-scm/git-scm-icon.svg" alt="git" width="40" height="40"/> </a> <a href="https://www.photoshop.com/en" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/devicons/devicon/master/icons/photoshop/photoshop-line.svg" alt="photoshop" width="40" height="40"/> </a> <a href="https://unrealengine.com/" target="_blank" rel="noreferrer"> <img src="https://raw.githubusercontent.com/kenangundogan/fontisto/036b7eca71aab1bef8e6a0518f7329f13ed62f6b/icons/svg/brand/unreal-engine.svg" alt="unreal" width="40" height="40"/> </a> </p>

<p><img align="left" src="https://github-readme-stats.vercel.app/api/top-langs?username=kabu0330&show_icons=true&theme=dark&locale=en&layout=compact" alt="kabu0330" /></p>

<p>&nbsp;<img align="center" src="https://github-readme-stats.vercel.app/api?username=kabu0330&show_icons=true&theme=dark&locale=en" alt="kabu0330" /></p>

<p><img align="center" src="https://github-readme-streak-stats.herokuapp.com/?user=kabu0330&theme=dark" alt="kabu0330" /></p>

<p align="left"> <img src="https://komarev.com/ghpvc/?username=kabu0330&label=Profile%20views&color=0e75b6&style=flat" alt="kabu0330" /> </p>
