<h1 align="left"> 게임 클라이언트 프로그래머 류성민입니다.</h1>

# 프로젝트 소개
* 클릭 시, 해당 깃허브 페이지로 이동합니다.
### 🔗 1. [UE5] 액션 게임 프로젝트 [github.com/kabu0330/UE_Soul2](https://github.com/kabu0330/UE_Soul2)
### 🔗 2. [UE5, AWS] Dedicated Server 프로젝트 [github.com/kabu0330/FPS_with_DedicatedServer](https://github.com/kabu0330/FPS_with_DedicatedServer)
### 🔗 3. [UE5 팀 프로젝트] 시뮬레이션 게임 (Overcooked! 2 모작) [github.com/kabu0330/UE_Overcooked2](https://github.com/kabu0330/UE_Overcooked2)
### 🔗 4. [DirectX 11] 2D 액션 게임 프로젝트 (Hollow Knight 모작) [github.com/kabu0330/DX_HollowKnight2](https://github.com/kabu0330/DX_HollowKnight2)
### 🔗 5. [WinAPI] 슈팅 게임 프로젝트 (The Binding of Isaac 모작) [github.com/kabu0330/WinAPI](https://github.com/kabu0330/WinAPI)
</p>

</br>
</br>

# 📜 목차
### 1. 📄 프로젝트 개요
- 📋 프로젝트 정보
- 💻 작업 내용
- 🎯 작업 목표
- 📊 배운 점 / 회고

</br>

### 2. 📑 주요 구현 내용 
### 2-1. 상태 관리 시스템
- 🔗 [[DirectX 11] ```Enum```의 한계 → ```FSM Component```](#directx-11-enum의-한계--fsm-component)
- 🔗 [[UE5 액션] 복잡한 상태도 심플하게, ```GameplayTag Container```](#ue5-액션-복잡한-상태도-심플하게-gameplaytag-container)
- 🔗 [UE5 액션] 공격이 캔슬된 후 캐릭터가 안 움직여요. ```FOnMontageEnded Delegate```

### 2-2. 컨탠츠 구현
- 🔗 [UE5 액션] 부드러운 콤보 연계는 어떻게 구현할까? ```AnimNotify State```
- 🔗 [UE5 액션] 타격감의 핵심은 타이밍이다. ```AnimNotify```
- 🔗 [UE5 액션] 자연스러운 대시를 구현할 순 없을까?  ```Motion Warping```
- 🔗 [UE5 액션] 아이템 및 몽타주 관리, 데이터 주도 설계 ```DataAsset```, ```DataTable```
- 🔗 [UE5 액션] 슬롯 기반 인벤토리 UI 동기화 전략  ```Inventory Component```, ```WidgetManager```
- 🔗 [UE5 팀 프로젝트] 다이나믹 머티리얼로 강조 효과 구현하기 
### 2-3. 네트워크 동기화 문제 해결 전략
- 🔗 [UE5 팀 프로젝트] 클라에서 스폰하면 안 보여요. ```SpawnActorDeferred```
- 🔗 [Dedicated Server] "서버에 접속할 수 없습니다" 안 보고 한 번에 접속하기
- 🔗 [Dedicated Server] 시간 오차는 어떻게 해결할까?
- 🔗 [Dedicated Server] 왜 님은 닉네임이 안 보여요? ```SeamlessTravel```
- 🔗 [Dedicated Server] 아니 방금 이겼는데 왜 내가 2등이예요? 
### 2-4. AI 시스템 구현
- 🔗 [DirectX 11] FSM 기반 몬스터 패턴
- 🔗 [UE5 액션] Behavior Tree를 활용한 몬스터 패턴
### 2-5. 커스텀 엔진 아키텍처 설계
- [DirectX 11] 언리얼 상속 기반 프레임워크 따라하기
### 2-6. 협업 및 버전 관리
- 🔗 [UE5 팀 프로젝트] Pull-Request 시행착오와 교훈
- 🔗 [UE5 팀 프로젝트] 테스트 레벨, 캐릭터 없이 UI로 기능 테스트
### 2-7. 최적화 전략 
- 🔗 [UE5 액션] ```Tick```에 미련을 버려라. 대안은 많다.
- 🔗 [Dedicated Server] 매번 배열 전체를 네트워크 복제해야 할까? ```Fast Array Serializer```
- 🔗 [DirectX 11] 드로우 콜을 줄이기 위한 전략 ```Mesh```, ```Material```
- 🔗 [DirectX 11] 모든 리소스를 다 로드하고 실행하나요? ```Thread```
### 2-8. 회고
- 🔗 이벤트 방식을 더 빨리 수용했더라면
- 🔗 인터페이스 vs 추상 클래스
- 🔗 PlayerController가 입력을 처리하는게 적절한가?

</br>

## 📄 1. 프로젝트 개요
### 🔭 [UE5] 액션 게임 프로젝트
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\SoulPlay.webp">
</p>

### 🔗 Youtube : [youtu.be/ut5GRCgf86Y?si=u_6SLFbson6Siksz](https://youtu.be/8U4345QKBfc)
### 🔗 Github : [github.com/kabu0330/UE_Soul2](https://github.com/kabu0330/UE_Soul2)

### 📋 프로젝트 정보

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
- ⚠️ 인터페이스 활용 부족 → 다음: Interface/Component 분리 원칙 적용
- ⚠️ 입력 처리 구조 한계 → 다음: Ability 시스템으로 입력-기능 분리

> 💡 **배운 점**: Tick 기반에서 이벤트 기반으로 전환하면서 코드가 훨씬 명확해졌습니다. "언제 실행되는지"를 Timer와 Delegate로 명시하니 디버깅도 쉬워지고, AnimNotify로 애니메이션과 로직을 분리하니 전투 시스템 확장이 보다 쉬워졌습니다. 

</p>

</br>

___


### 🔭 [UE5, AWS] Dedicated Server 프로젝트
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\DedicatedServer.webp">
</p>

### 🔗 Youtube : [youtu.be/8tyiK_7egvI?si=MP7l8gBIcKs95v6U](https://youtu.be/8tyiK_7egvI?si=MP7l8gBIcKs95v6U)
### 🔗 Github : [github.com/kabu0330/FPS_with_DedicatedServer](https://github.com/kabu0330/FPS_with_DedicatedServer)

### 📋 프로젝트 정보

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


### 🎯 작업 목표
**서버-클라이언트 아키텍처 및 AWS 클라우드 인프라 실전 경험**
- Dedicated Server 구조 이해 (Authority 기반 설계)
- AWS SDK 활용 (EC2, Lambda, DynamoDB, GameLift)
- 네트워크 동기화 문제 해결 (RPC/Replication, SeamlessTravel)

### 📊 핵심 성과
- ✅ AWS SDK C++ 빌드 및 UE 프로젝트 연동 (Lambda, DynamoDB)
- ✅ SeamlessTravel 시 PlayerState 동기화 문제 해결 (```OverrideWith```)
- ✅ 컨텐츠/서버 전용 모듈 분리
- ✅ 로그 기반 서버 디버깅 환경 구축 (AWS CloudWatch 연동)
- ✅ FFastArraySerializer 적용 네트워크 복제 비용 최적화

> 💡 **배운 점**: Dedicated Server를 직접 구축하며 **서버의 역할**을 보다 잘 이해하게 되었습니다. 클라이언트에서 보이는 것과 서버에서 계산하는 것을 분리하고, Replication 타이밍을 제어하는 과정에서 네트워크 게임의 기본 구조를 이해하게 되었습니다. "중단점 없이 로그만 보고 디버깅"하는 경험이 처음엔 어려웠지만, 덕분에 로그를 활용한 디버깅 능력을 기를 수 있었습니다.


___

</br>


### 🔭 [UE5 팀 프로젝트] 시뮬레이션 게임 (Overcooked! 2 모작)
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\Overcooked!2.gif">
</p>

### 🔗 Youtube : [youtu.be/zs3aQ8tSZ3E?si=R2VaHZ-xt10g0D2M](https://youtu.be/zs3aQ8tSZ3E?si=R2VaHZ-xt10g0D2M)
### 🔗 Github : [github.com/kabu0330/UE_Overcooked2](https://github.com/kabu0330/UE_Overcooked2)

### 📋 프로젝트 정보

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


### 🎯 작업 목표
**멀티플레이어 협업 게임 개발 및 팀 협업 경험**
- 네트워크 동기화 문제 해결 (재료 스폰, 상호작용 시스템, 머티리얼 동기화)
- Git 버전 관리 실전 경험 (Fork-PR 전략)
- 독립적인 기능 테스트 환경 구축

### 📊 핵심 성과
- ✅ SpawnActorDeferred로 Replicate 타이밍 문제 해결
- ✅ 클라이언트 전용 처리 결정으로 네트워크 최적화
- ✅ 테스트 레벨로 독립적 기능 검증 가능
- ✅ DataTable 기반 요리 시스템
- ⚠️ Fork-PR 방식의 시행착오 경험 → Stash 활용법을 나중에 알게 됨

> 💡 **배운 점**: 팀 프로젝트에서는 "**항상 내가 통제 가능한 상태에서 테스트할 수 없다**"는 현실을 체감했습니다. 테스트 레벨을 만들어 캐릭터 없이도 기능을 검증하고, Git 전략을 개선하며, 네트워크 동기화를 "필요한 것만" 하는 선택 기준을 익혔습니다

___

</br>


### 🔭 [DirectX 11] 2D 액션 게임 프로젝트 (Hollow Knight 모작)
### 📸 Gif

<p align="center">
 <img alt="이미지" src="readme\HollowKnight.gif">
</p>

### 🔗 Youtube : [youtu.be/vi6KnUeedrs?si=nJsI59Pi36cGy-Rn](https://youtu.be/vi6KnUeedrs?si=nJsI59Pi36cGy-Rn)
### 🔗 Github : [github.com/kabu0330/DX_HollowKnight2](https://github.com/kabu0330/DX_HollowKnight2)

### 📋 프로젝트 정보

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
- ✅ 드로우 콜 최적화 (메시, 머티리얼 재사용)

> 💡 **배운 점**: 엔진을 분석하며 **UE5의 설계 철학**을 이해하게 되었습니다. "왜 Actor와 Component를 분리하는가", "왜 Tick이 필요한가" 같은 질문에 답하며, UE5로 돌아왔을 때 단순히 "사용"하는 것이 아니라 "이해하고 활용"할 수 있게 되었습니다.
___

</br>

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

```cpp
// Player.h - 상태가 두 곳에 분산
enum class LowerState { IDLE, LEFT, RIGHT, UP, DOWN, DEATH };
enum class UpperState { 
    IDLE, LEFT, RIGHT, UP, DOWN,
    ATTACK_LEFT, ATTACK_RIGHT, ATTACK_UP, ATTACK_DOWN, DEATH 
};

LowerState BodyState;
UpperState HeadState;

// 추가로 bool 변수들도 필요
bool IsHit = false;
bool Invincibility = false;
bool IsDead = false;
```

```cpp
// Player.cpp - 거대한 Switch 문 (1226라인~)
void APlayer::CurStateAnimation(const float& _DeltaTime)
{
    switch (BodyState) {
    case LowerState::IDLE:
        BodyRenderer->ChangeAnimation("Body_Idle");
        break;
    case LowerState::LEFT:
        BodyRenderer->ChangeAnimation("Body_Left");
        break;
    // ... 5개 case 반복
    }
    
    switch (HeadState) {
    case UpperState::IDLE:
        HeadRenderer->ChangeAnimation("Head_Down");
        break;
    // ... 10개 case 반복
    }
}
```

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

FSM을 아래와 같이 활용했습니다. 

```cpp
void AKnight::SetFSM()
{
	// 이동 애니메이션
	CreateState(EKnightState::IDLE, &AKnight::SetIdle, "Idle");
	CreateState(EKnightState::RUN, &AKnight::SetRun, "Run");
	CreateState(EKnightState::RUN_TO_IDLE, &AKnight::SetRunToIdle, "RunToIdle");
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

프로젝트 종료 후 복기하며 "```StartFunction```을 vector로 만들었다면 초기화 로직과 Tick 로직을 분리할 수 있었을 것"이라는 생각이 들었습니다.

**이렇게 했다면:**
- 애니메이션 재생
- 플래그 초기화
- 사운드 재생
- 이펙트 스폰

**상태 진입 시 한 번만 실행될 로직들을** 모두 ```StartFunction```에서 처리할 수 있었을 것입니다.

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
| **가독성** | ⭐⭐ | ⭐⭐⭐⭐ |

</br>

___

</br>

### [UE5 액션] 복잡한 상태도 심플하게, ```GameplayTag Container```

### 🎮 구현 목표 
**복합 상태를 bool 변수 없이 직관적으로 표현하고, 상태 검사를 체계적으로 관리하기**

DirectX 프로젝트에서 FSM Component로 상태 전환은 개선했지만, "공격 중 + 경직 면역", "구르기 + 이동불가 + 무적" 같은 복합 상태는 여전히 bool 변수가 필요했습니다. </br>
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
    //...
};
```

</br>

### 🔧 활용
특정 동작을 실행하기 위한 상태 검사
```cpp
bool ASoulCharacterBase::CanPerformAttack(FGameplayTag& AttackTypeTag, const bool bHitCanceled, const bool bPairedAnimation)
{
	check(CombatComponent);
	check(StateComponent);
	check(AttributeComponent);

	// 공격의 기본 조건은 무기를 들고 있는가?
	if (IsValid(CombatComponent->GetMainWeapon()) == false) return false;

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
    //...

    return StateComponent->IsAnyActiveGameplayTags(CheckTags) == false && // 태그 검사
		CombatComponent->IsCombatEnabled() == true &&
		AttributeComponent->CheckHasEnoughStamina(StaminaCost) == true;
}
```

**이렇게 하면:**
- "공격 중 + 경직 면역" = 
  `Attacking` + `Poise` 두 태그 동시 보유
- "피격 시 경직 면역인가?" = 
  Container에 `Poise` 태그 있는지 검사
- 복잡한 조합 = 
  필요한 태그들만 추가/제거

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
- "왜 공격이 안 나가지?" → 화면 보고 `Movement_Disabled` 태그 발견 → 태그 추가 로직 디버그
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
| **가독성** | ⭐⭐ | ⭐⭐⭐⭐⭐ |


</br>

___

</br>

### [UE5 액션] 공격이 캔슬된 후 캐릭터가 안 움직여요. ```FOnMontageEnded Delegate```



### 2-2. 컨탠츠 구현
- [UE5 액션] 부드러운 콤보 연계는 어떻게 구현할까? ```AnimNotify State```
- [UE5 액션] 타격감의 핵심은 타이밍이다. ```AnimNotify```
- [UE5 액션] 자연스러운 대시를 구현할 순 없을까?  ```Motion Warping```
- [UE5 액션] 아이템 및 몽타주 관리, 데이터 주도 설계 ```DataAsset```, ```DataTable```
- [UE5 액션] 슬롯 기반 인벤토리 UI 동기화 전략  ```Inventory Component```, ```WidgetManager```
### 2-3. 네트워크 동기화 문제 해결 전략
- [UE5 팀 프로젝트] 클라에서 스폰하면 안 보여요. ```SpawnActorDeferred```
- [Dedicated Server] "서버에 접속할 수 없습니다" 안 보고 한 번에 접속하기
- [Dedicated Server] 시간 오차는 어떻게 해결할까?
- [Dedicated Server] 왜 님은 닉네임이 안 보여요? ```SeamlessTravel```
- [Dedicated Server] 아니 방금 이겼는데 왜 내가 2등이예요? 
### 2-4. AI 시스템 구현
- [DirectX 11] FSM 기반 몬스터 패턴
- [UE5 액션] Behavior Tree를 활용한 몬스터 패턴
### 2-5. 커스텀 엔진 아키텍처 설계
- [DirectX 11] 언리얼 상속 기반 프레임워크 따라하기
### 2-6. 협업 및 버전 관리
- [UE5 팀 프로젝트] Pull-Request 시행착오와 교훈
- [UE5 팀 프로젝트] 테스트 레벨, 캐릭터 없이 UI로 기능 테스트
- [UE5 팀 프로젝트] 다이나믹 머티리얼로 강조 효과 구현하기
### 2-7. 최적화 전략 
- [UE5 액션] ```Tick```에 미련을 버려라. 대안은 많다.
- [Dedicated Server] 매번 배열 전체를 네트워크 복제해야 할까? ```Fast Array Serializer```
- [DirectX 11] 드로우 콜을 줄이기 위한 전략 ```Mesh```, ```Material```
- [DirectX 11] 모든 리소스를 다 로드하고 실행하나요? ```Thread```
### 2-8. 회고
- 이벤트 방식을 더 빨리 수용했더라면
- 인터페이스 vs 추상 클래스
- PlayerController가 입력을 처리하는게 적절한가?


### 🎮 구현 목표 

</br>

### 🚨 문제 상황

</br>

### 💭 해결 방안 고민  

</br>

### 🔧 시행착오 

</br>

### ✅ 결과 

</br>

___

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
