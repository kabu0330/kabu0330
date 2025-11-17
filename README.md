<h1 align="left"> 게임 클라이언트 프로그래머 류성민입니다.</h1>

## 프로젝트 링크
### 🔗 1. [UE5] 액션 게임 프로젝트 [github.com/kabu0330/UE_Soul2](https://github.com/kabu0330/UE_Soul2)
### 🔗 2. [UE5, AWS] Dedicated Server 프로젝트 [github.com/kabu0330/FPS_with_DedicatedServer](https://github.com/kabu0330/FPS_with_DedicatedServer)
### 🔗 3. [UE5 팀 프로젝트] 시뮬레이션 게임 (Overcooked! 2 모작) [github.com/kabu0330/UE_Overcooked2](https://github.com/kabu0330/UE_Overcooked2)
### 🔗 4. [DirectX 11] 2D 액션 게임 프로젝트 (Hollow Knight 모작) [github.com/kabu0330/DX_HollowKnight2](https://github.com/kabu0330/DX_HollowKnight2)
### 🔗 5. [WinAPI] 슈팅 게임 프로젝트 (The Binding of Isaac 모작) [github.com/kabu0330/WinAPI](https://github.com/kabu0330/WinAPI)
</p>

</br>

## 📜 목차
### 1. 📄 프로젝트 개요
- 📋 프로젝트 정보
- 💻 작업 내용
- 🎯 작업 목표
- 📊 배운 점 / 회고

</br>

### 2. 📑 주요 구현 내용 
* 제가 가장 깊이있게 고민한 대표 문제 해결 사례 세 개를 뽑아 ✅ 표시했습니다.
### 2-1. 상태 관리 시스템
- 🔗 [[DirectX 11] ```Enum```의 한계 → ```FSM Component```](#directx-11-enum의-한계--fsm-component)
- 🔗 [[UE5 액션] 복잡한 상태도 심플하게, ```GameplayTag Container```](#ue5-액션-복잡한-상태도-심플하게-gameplaytag-container)
- 🔗 [[UE5 액션] 공격이 캔슬된 후 캐릭터가 안 움직여요.](#ue5-액션-공격이-캔슬된-후-캐릭터가-안-움직여요-fonmontageended-delegate) 

### 2-2. 컨탠츠 구현
- 🔗 [[UE5 액션] 부드러운 콤보 연계는 어떻게 구현할까? ```AnimNotify State```](#ue5-액션-부드러운-콤보-연계는-어떻게-구현할까-animnotify-state)
- 🔗 [[UE5 액션] 자연스러운 대시를 구현할 순 없을까?  ```Motion Warping```](#ue5-액션-자연스러운-대시를-구현할-순-없을까--motion-warping)
- 🔗 [[UE5 액션] 무기별 전투 스타일, 데이터 주도 설계](#ue5-액션-무기별-전투-스타일-데이터-주도-설계)
- 🔗 [UE5 액션] 슬롯 기반 인벤토리 UI 동기화 전략  ```Inventory Component```, ```WidgetManager```
- 🔗 [UE5 팀 프로젝트] 다이나믹 머티리얼로 강조 효과 구현하기 
### 2-3. 네트워크 동기화 문제 해결 전략
- 🔗 [UE5 팀 프로젝트] 클라에서 스폰하면 안 보여요. ```SpawnActorDeferred``` 
- 🔗 [Dedicated Server] "서버에 접속할 수 없습니다" 메시지 없이 한 번에 접속하기
- 🔗 [Dedicated Server] 시간 오차는 어떻게 해결할까?
- 🔗 [Dedicated Server] 왜 님은 닉네임이 안 보여요? ```SeamlessTravel``` 
- 🔗 [Dedicated Server] 아니 방금 이겼는데 왜 내가 2등이예요? 
### 2-4. AI 시스템 구현
- 🔗 [UE5 액션] Behavior Tree를 활용한 몬스터 패턴
### 2-5. 커스텀 엔진 아키텍처
- 🔗 [DirectX 11] 언리얼 상속 기반 프레임워크 따라하기
### 2-6. 협업 및 버전 관리
- 🔗 [UE5 팀 프로젝트] Pull-Request 시행착오와 교훈
- 🔗 [UE5 팀 프로젝트] 테스트 레벨, 캐릭터 없이 UI로 기능 테스트
### 2-7. 최적화 전략 
- 🔗 [UE5 액션] ```Tick```에 미련을 버려라. 대안은 많다. 
- 🔗 [Dedicated Server] 매번 배열 전체를 네트워크 복제해야 할까? ```Fast Array Serializer```
- 🔗 [DirectX 11] 드로우 콜을 줄이기 위한 전략 ```Mesh```, ```Material```
- 🔗 [DirectX 11] 모든 리소스를 다 로드할 때까지 기다리나요? ```Thread```
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

</br>

___



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

</br>
___


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
</br>

FSM을 아래와 같이 활용했습니다. 

```cpp
void AKnight::SetFSM()
{
	//            상태                Update          애니메이션
	CreateState(EKnightState::IDLE, &AKnight::SetIdle, "Idle");
	CreateState(EKnightState::RUN, &AKnight::SetRun, "Run");
	CreateState(EKnightState::RUN_TO_IDLE, &AKnight::SetRunToIdle, "RunToIdle");
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
| **가독성** | ⭐⭐ | ⭐⭐⭐⭐ |

</br>

___

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
- "왜 공격이 안 나가지?" → 화면 보고 `Movement_Disabled` 태그 발견 → 태그 제거 로직 검사
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

### [UE5 액션] 공격이 캔슬된 후 캐릭터가 안 움직여요. ```FOnMontageEnded Delegate```

### 🎮 구현 목표 

전투 중 **입력으로 스킬을 캔슬**하거나 **피격으로 몽타주가 중단**되는 등, 몽타주가 끝까지 재생되지 않는 상황에서도 캐릭터 상태가 정상적으로 복구되는 전투 시스템을 구현하고자 했습니다.

</br>

### 🚨 문제 상황
**몽타주가 중단되면 Gameplay Tag가 제거되지 않는 현상 발생**

기존 구조에서는 공격/피격 시작 시 상태 태그를 추가하지만, 종료 시 태그 제거는 ```AnimNotify```에 의존했습니다.

```cpp
void UAnimNotify_RemoveGameplayTag::Notify(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation,
                                          const FAnimNotifyEventReference& EventReference)
{
	// ...
	if (UStateComponent* StateComponent = Character->GetStateComponent())
	{
		StateComponent->RemoveGameplayTags(GameplayTags);
	}
}
```

**AnimNotify의 치명적인 한계:**
- ❌ **몽타주가 중단되면** 해당 프레임의 Notify가 **호출되지 않음**
- ❌ **블렌드 아웃** 발생 시 몽타주 끝부분 Notify가 **누락될 위험**

즉, 몽타주가 **끝까지 재생되고 블렌드 없이 종료**된다는 보장이 있어야만 AnimNotify로 상태 관리가 가능합니다. 

**실제 발생한 문제:**
- 공격 중 회피 → `TAG_Character_State_Attacking` 미제거 → 캐릭터 영구 이동 불가, 공격 입력 무시
- 피격으로 공격 중단 → `TAG_Character_State_Attacking` 미제거 → 캐릭터 영구 이동 불가, 공격 입력 무시

</br>

### 💭 해결 방안 고민  
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

### 🔧 시행착오 
#### 1차 시도: AnimNotify 위치 조정
- 몽타주 끝부분에 Notify 배치 → 여전히 캔슬 시 미호출
- **실패 원인:** 구조적 문제 미해결

#### 2차 시도: FOnMontageEnded Delegate 적용
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

AnimNotify는 **특정 타이밍의 이벤트**(이펙트 재생, 사운드 등)에 적합하지만, **상태 초기화**처럼 반드시 실행되어야 하는 로직은 **Delegate로 보장**해야 합니다. UE5가 제공하는 몽타주 콜백 시스템을 활용하면 복잡한 예외 처리 없이 안전한 상태 관리가 가능합니다.

</br>

___

### 2-2. 컨탠츠 구현
### [UE5 액션] 부드러운 콤보 연계는 어떻게 구현할까? ```AnimNotify State```

### 🎮 구현 목표 
**자연스러운 콤보 시스템 구현**
- 공격 중 입력이 들어오면 **후딜레이를 캔슬**하고 즉시 다음 콤보로 연계
- 공격 종료 후에도 **일정 시간 내 입력** 시 다음 콤보 진행
- 입력 타이밍에 따라 **정확한 프레임에서 콤보 전환**

</br>

### 🚨 문제 상황
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

### 💭 해결 방안 고민  
**"입력 체크 타이밍을 애니메이션 기준으로 제어할 수 있다면?"**

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
    //...
	if (UCombatComponent* CombatComp = Character->GetCombatComponent())
	{
		CombatComp->EnableComboWindow();
	}
}

void UAnimNotifyState_ComboWindow::NotifyEnd(USkeletalMeshComponent* MeshComp, UAnimSequenceBase* Animation,
	const FAnimNotifyEventReference& EventReference)
{
     //...
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
	else
	{
		if (ASoulCharacterBase* CharacterBase = Cast<ASoulCharacterBase>(GetOwner()))
		{
			CharacterBase->SetState(SoulGameplayTag::Character_State_Attacking_Recovery);
		}
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

조작감을 높이겠다는 의도로 후딜레이 캔슬이라는 혜택을 제공한 것은 좋았으나, 패널티(후딜레이간 입력/이동 불가)가 너무 강력했습니다.

</br>


#### 2-1차 시도: ComboWindow 범위 확장
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

#### 3차 개선: 이중 입력 윈도우 시스템
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
    //...
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
	
	ASoulCharacterBase* CharacterBase = Cast<ASoulCharacterBase>(GetOwner());
	if (false == IsValid(CharacterBase)) return;
	
	// 상태 처리를 위해 캐릭터로 내려 보낸다.
	CharacterBase->AttackFinished();
}
```
```cpp
void UCombatComponent::ExecuteComboAttack(const FGameplayTag& AttackTypeTag)
{
    //...
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

**왜 결국 Timer를 다시 썼는가?**

AnimNotifyState는 **애니메이션 구간**만 제어할 수 있지, **시간 기반 유예 기간**은 제공할 수 없습니다.

Timer의 역할 재정의:
- ❌ (기존) 콤보 전환 타이밍 결정 → 부정확, 유연성 부족
- ✅ (개선) 콤보 시퀀스 유지 시간 보장 → 정확한 역할 분담

**NotifyState + Timer 조합의 시너지:**
- NotifyState: **정밀한 보상 구간** (후딜 캔슬 가능)
- Timer: **넓은 허용 구간** (콤보 유지만 보장)

</br>

### ✅ 결과 
**조작감을 챙긴 3단계 입력 시스템**

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

### [UE5 액션] 자연스러운 대시를 구현할 순 없을까?  ```Motion Warping```

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

### 💭 해결 방안 고민  
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

즉, 제가 찾던 **"애니메이션과 이동을 하나로 묶는 방법"**이었습니다.

</br>

### 🔧 시행착오 

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


#### 2차 시도: C++ 구현 및 레이캐스트 통합

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


대시 애니메이션의 **특정 구간**에 Motion Warping Notify를 추가:
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

### [UE5 액션] 무기별 전투 스타일, 데이터 주도 설계

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

### 🔧 시행착오 
#### 핵심 고민: 정말 필요한 데이터만 남기기

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
   /** 핵심 */
	UPROPERTY(EditDefaultsOnly, Category = "Setting|Animation")
	TObjectPtr<UMontageActionData> MontageActionData;

	UPROPERTY(EditDefaultsOnly, Category = "Setting|Weapon")
	TObjectPtr<UWeaponStatData> WeaponStatDataAsset;

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
	Super::EquipItem();
    //...
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
	if (false == IsValid(Montage)) 
	{
       // 콤보 초기화하고 첫 번째 공격으로
		CombatComponent->SetComboCounter(0);
		ComboCounter = CombatComponent->GetComboCounter();
		Montage = Weapon->GetMontageForTag(NewAttackTypeTag, ComboCounter);

        // 그래도 없다면 이 무기에 해당 공격이 없는 것
		if (false == IsValid(Montage))
		{
			return;
		}
	}
    //...

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

### [UE5 액션] 슬롯 기반 인벤토리 UI 동기화 전략  ```Inventory Component```, ```WidgetManager```

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


- [UE5 팀 프로젝트] 다이나믹 머티리얼로 강조 효과 구현하기

### 2-3. 네트워크 동기화 문제 해결 전략
- [UE5 팀 프로젝트] 클라에서 스폰하면 안 보여요. ```SpawnActorDeferred```
- [Dedicated Server] "서버에 접속할 수 없습니다" 메시지 없이 한 번에 접속하기
- [Dedicated Server] 시간 오차는 어떻게 해결할까?
- [Dedicated Server] 왜 님은 닉네임이 안 보여요? ```SeamlessTravel```
- [Dedicated Server] 아니 방금 이겼는데 왜 내가 2등이예요? 
### 2-4. AI 시스템 구현
- [UE5 액션] Behavior Tree를 활용한 몬스터 패턴
### 2-5. 커스텀 엔진 아키텍처 설계
- [DirectX 11] 언리얼 상속 기반 프레임워크 따라하기
### 2-6. 협업 및 버전 관리
- [UE5 팀 프로젝트] Pull-Request 시행착오와 교훈
- [UE5 팀 프로젝트] 테스트 레벨, 캐릭터 없이 UI로 기능 테스트

### 2-7. 최적화 전략 
- [UE5 액션] ```Tick```에 미련을 버려라. 대안은 많다.
- [Dedicated Server] 매번 배열 전체를 네트워크 복제해야 할까? ```Fast Array Serializer```
- [DirectX 11] 드로우 콜을 줄이기 위한 전략 ```Mesh```, ```Material```
- [DirectX 11] 모든 리소스를 다 로드할 때까지 기다리나요? ```Thread```
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





___


<p align="center">
 <img alt="이미지" src="readme\ComboWindow.png">
</p>

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
