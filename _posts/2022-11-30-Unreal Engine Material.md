---
title: "[Unreal Engine] Meteral"
date: 2022-11-30 00:01:36
categories:
- Unreal Engine
tags: UE Material
comments: true
---

[Material Expressions](https://docs.unrealengine.com/5.0/en-US/unreal-engine-material-expressions-reference/){:target="_blank"}관련 Unreal Engine Documentation을 참고하여 작성되었습니다. Unreal Engine의 Material을 생성하고 사용하는 Material Expressions을 서술합니다.

<!-- more -->

# Distance Field Material
![slime.png](/assets/images/Image_UE5/distance_1.png)
![slime.png](/assets/images/Image_UE5/distance_BP.png)
* `DistanceToNearestSurface` material에서 레벨의 Global Distance Field 까지의 모든 점을 샘플링할 수 있습니다. Distance Field로부터 가장 가까운 occluders까지의 signed distance를 world space 단위로 출력합니다.  
* `VertexNormalWS` world-space vertex normal을 출력합니다. WorldPositionOffset과 같이 vertex shader에서 실행되는 material 입력에만 사용할 수 있습니다. 이 기능은 mesh를 확대하거나 축소하는 데 유용합니다.

# Outline Post Process Effect
![post_process.png](/assets/images/Image_UE5/post_process.png)
![post_process.png](/assets/images/Image_UE5/post_process_BP.png)



# 참고
* https://docs.unrealengine.com/5.0/en-US/unreal-engine-material-expressions-reference/
* https://www.youtube.com/watch?v=tb8wZGMCPCw&ab_channel=UpsideDown
* https://www.youtube.com/watch?v=umzLSts3sto&ab_channel=UpsideDown