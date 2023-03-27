---
title: "[Unreal Engine 5] Meta Human"
date: 2022-11-10 00:00:42
categories:
- Unreal Engine 5
tags: UE5 MetaHuman
comments: true
---


[Unreal Engine 5] 메타휴먼 사용법

<!-- more -->

# MetaHuman 사용하는 방법
## MetaHuman Creator를 통해 MetaHuman 만들기
[MetaHuman Creator](https://metahuman.unrealengine.com/){:target="_blank"}에 접속하면 아래와 같이 MetaHuman을 제작할 수 있는 Creator 사이트에 도달합니다. 좌측의 '최신 메타휴먼 크리에이터 시작' 버튼을 눌러 크리에이터를 시작할 수 있습니다.
![MetaHuman_Creator_start](/assets/images/Image_UE5/MetaHuman_Creater_start.png)
프리셋 갤러리에서 사전 설정할 MetaHuman을 선택한 다음 선택 생성 버튼을 클릭하여 MetaHuman을 생성을 시작합니다.
![MetaHuman_Create](/assets/images/Image_UE5/MetaHuman_create.png)
생성한 메터휴먼은 자동 저장되며, 나의 메타휴먼에서 확인할 수 있습니다.
![MetaHuman_Create](/assets/images/Image_UE5/my_MetaHuman.png)

## MetaHuman 다운로드 및 내보내기
Unreal Engine에서 MetaHumans를 사용하려면 먼저 Quixel Bridge에서 필요한 모든 파일과 에셋을 다운로드해야 합니다.
![plugin](/assets/images/Image_UE5/plugin.png)
Unreal Engine 5에서 Quixel Bridge열어 MetaHuman이나 asset을 다운받을 수 있습니다.
![Quixel Bridge](/assets/images/Image_UE5/bridge-5_0-open-bridge.webp)

# 애니메이션 적용하는 방법 
## Animation Retargeting
[Animation Retargeting](https://docs.unrealengine.com/5.0/en-US/animation-retargeting-in-unreal-engine/)은 동일한 skeleton asset을 사용하지만 비율이 크게 다를 수 있는 캐릭터 간에 애니메이션을 재사용할 수 있는 기능입니다. 대상을 다시 지정하면 모양이 다른 캐릭터의 애니메이션을 사용할 때 애니메이션 골격이 다르거나 불필요하게 변형되는 것을 방지할 수 있습니다. 애니메이션 리타겟팅을 사용하면 유사한 골격 계층을 공유하고 **Rig**를 사용하여 한 골격에서 다른 골격으로 애니메이션 데이터를 전달하는 한 서로 다른 skeleton asset을 사용하는 캐릭터 간에 애니메이션을 공유할 수 있습니다.
![Animation Retargeting](/assets/images/Image_UE5/retarget.png)
<iframe width="787" height="443" src="https://www.youtube.com/embed/5Or8yQ_QecQ" title="Unreal Engine 5 Tutorial - Animation Retargetting" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
애니메이션 리타겟팅은 위 튜토리얼 영상을 참고하여 새로운 skeleton의 애니메이션을 추출할 수 있습니다.

## Body Animation
[mixamo](https://www.mixamo.com/#/)에서 애니메이션을 다운받을 수 있습니다.
![Body Animation](/assets/images/Image_UE5/body_anim.png)
## Face Animation
`Layered blend per bone` 노드를 사용하면 정의된 골격 세트를 기준으로 여러 동적 혼합 포즈를 혼합할 수 있습니다. 이를 이용해 MetaHuman의 Live Link Pose와 얼굴 애니메이션을 blend하여 표정 애니메이션을 나타낼 수 있습니다.
![Face Animation](/assets/images/Image_UE5/face_anim_bp.png)

# 애니메이션 생성 및 수정하는 방법

# LOD 관련 내용

# 참고
* https://www.unrealengine.com/en-US/metahuman?sessionInvalidated=true
* https://docs.metahuman.unrealengine.com/en-US/
* https://docs.unrealengine.com/5.0/en-US/quixel-bridge-plugin-for-unreal-engine/
* https://docs.unrealengine.com/5.0/en-US/animation-retargeting-in-unreal-engine/
* https://www.youtube.com/watch?v=5Or8yQ_QecQ&ab_channel=RyanLaley
* https://forums.unrealengine.com/t/metahuman-head-floating-with-body-and-face-animation/559180
