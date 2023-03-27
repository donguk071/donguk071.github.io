---
title: "[Unreal Engine] Niagara VFX System"
date: 2022-11-16 00:01:36
categories:
- Unreal Engine
tags: UE Niagara
comments: true
---


[Niagara VFX System](https://docs.unrealengine.com/5.0/en-US/creating-visual-effects-in-niagara-for-unreal-engine/){:target="_blank"}관련 Unreal Engine Documentation을 참고하여 작성되었습니다. Unreal Engine의 Niagara VFX System을 사용하여 Particle 효과를 실시간으로 생성하는 방법을 서술합니다. 본 내용은 UE4와 UE5의 Niagara Documentation을 혼합하여 작성되었습니다. 

<!-- more -->

# Niagara System 
## [Niagara Overview](https://docs.unrealengine.com/5.0/en-US/overview-of-niagara-effects-for-unreal-engine/){:target="_blank"}
Niagara는 Unreal Engine의 차세대 VFX 시스템입니다.

### Core Niagara Components
* [Systems](#systems)
* [Emitters](#emitters)
* [Modules](#modules)
* [Parameters](#parameters)


#### Systems
Niagara system은 효과를 만드는 데 필요한 모든 것을 담는 컨테이너입니다. 즉, 각각 하나의 이펙트로 결합된 여러 Emitter을 정의할 수 있습니다. 시스템 내부에는 전체적인 효과를 생성하는 데 도움이 되는 다양한 빌딩 블록이 쌓일 수 있습니다. Niagara system editor에서 시스템에 있는 Emitter 또는 Module의 모든 항목을 수정하거나 덮어쓸 수 있습니다.
<p align="center"><img src="/assets/images/Image_UE5/01-niagara-system.webp" width="300" height="300" /> </p>

#### Emitters
Emitter는 Niagara system에서 입자가 생성되는 곳입니다. 입자가 어떻게 태어나고, 나이가 들면서 입자에게 무슨 일이 일어나는지, 그리고 입자가 어떻게 보이고 행동하는지를 조절합니다.  
Emitter는 스택으로 구성되고 그 내부에는 여러 그룹이 있으며, 안에 개별 작업을 수행하는 모듈을 넣을 수 있습니다.
<p align="center"><img src="/assets/images/Image_UE5/02-emitters-with-groups.webp" width="300" height="300" /> </p>
1. **Emitter Spawn**  
CPU에 Emitter가 처음 생성될 때 발생하는 동작을 정의합니다. 이 그룹을 사용하여 초기 설정 및 기본값을 정의합니다.
2. **Emitter Update**  
CPU의 모든 프레임에서 발생하는 Emitter 수준 Module을 정의합니다. 이 그룹을 사용하여 모든 프레임에서 Particle을 계속 산란시킬 때 입자의 산란을 정의합니다.
3. **Particle Spawn**  
Particle이 처음 태어날 때 Particle 당 한 번으로 취급합니다. 여기서 Particle이 태어난 위치, 색상, 크기 등 입자의 초기화 세부 정보를 정의할 수 있습니다.
4. **Particle Update**  
각 프레임의 Particle 당 호출됩니다. Particle이 노화됨에 따라 프레임별로 변경해야 하는 모든 것을 여기서 정의할 수 있습니다. 예를 들어, Particle의 색이 시간이 지남에 따라 변하거나 Particle이 중력, curl noise 또는 점 인력과 같은 힘의 영향을 받는 경우를 정의할 수 있습니다.  
5. **Event Handler**  
특정 데이터를 정의하는 하나 이상의 Emitter에 Generate 이벤트를 생성할 수 있습니다. 그런 다음 생성된 이벤트에 대한 반응으로 동작을 트리거하는 다른 Emitter에서 수신 대기 이벤트를 생성할 수 있습니다.
6. **Render**  
Render 그룹에서 Particle의 표시를 정의하고 Particle에 대한 하나 이상의 Renderer를 설정할 수 있습니다. material를 적용할 수 있는 3D 모델을 Particle로 정의하려는 경우 Mesh Renderer를 사용할 수 있습니다. 또는 Sprite Renderer를 사용하여 Particle를 2D Sprite로 정의할 수 있습니다. 


#### Modules
Module은 Niagara 효과의 기본 구성 요소입니다. 그룹에 모듈을 추가하여 스택을 만들고, 위에서 아래로 순차적으로 처리됩니다. Module은 계산을 하기 위한 컨테이너 입니다. Module에 데이터를 전달하고 Module 내부에서 데이터를 계산한 다음 Module의 끝에 데이터를 다시 기록합니다.
<p align="center"><img src="/assets/images/Image_UE5/03-modules-in-an-emitter.webp" width="300" height="300" /> </p>
Module은 HLSL(High-Level Shading Language)을 사용하여 빌드되지만 노드를 사용하여 그래프에서 시각적으로 빌드할 수 있습니다. 함수를 만들거나 입력을 포함하거나 값 또는 parameter map에 쓸 수 있습니다. 그래프의 CustomHLSL 노드를 사용하여 HLSL 코드를 인라인으로 작성할 수도 있습니다.


#### Parameters
Parameter는 Niagara 시뮬레이션에서 데이터를 추상화한 것입니다. Parameter 유형은 나타내는 데이터를 정의하기 위해 Parameter에 할당됩니다.

* **<span style='background-color: #fff5b1'>Primitive</span>** : 다양한 정밀도와 채널 폭의 숫자 데이터를 정의합니다.
* **<span style='background-color: #fff5b1'>Enum</span>** : 이 매개 변수 유형은 명명된 값의 고정 집합을 정의하고 명명된 값 중 하나를 가정합니다.
* **<span style='background-color: #fff5b1'>Struct</span>** : Primitive 및 Enum 유형의 조합 세트를 정의합니다.
* **<span style='background-color: #fff5b1'>Data Interfaces</span>** : 외부 데이터 소스에서 데이터를 제공하는 기능을 정의합니다. 이는 UE4의 다른 부분에서 가져온 데이터이거나 외부 애플리케이션에서 가져온 데이터일 수 있습니다.
<p align="center"><img src="/assets/images/Image_UE5/03-modules-in-an-emitter.webp" width="300" height="300" /> </p>
더하기 기호 아이콘(+)을 클릭하고 새 매개 변수 또는 기존 매개 변수를 직접 설정을 선택하여 사용자 지정 매개 변수 모듈을 이미터에 추가할 수 있습니다. 그러면 Set Parameter 모듈이 스택에 추가됩니다. 매개 변수 설정 모듈에서 더하기 기호 아이콘(+)을 클릭하고 매개 변수 추가를 선택하여 기존 매개 변수를 설정하거나 새 매개 변수 만들기를 선택하여 새 매개 변수를 설정합니다.

# 참고
* https://docs.unrealengine.com/5.0/en-US/creating-visual-effects-in-niagara-for-unreal-engine/
* https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Niagara/EmitterEditorReference/
* https://docs.unrealengine.com/4.27/en-US/RenderingAndGraphics/Niagara/Overview/
 