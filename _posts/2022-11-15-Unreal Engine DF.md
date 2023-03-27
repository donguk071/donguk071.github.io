---
title: "[Unreal Engine] Distance Field"
date: 2022-11-15 00:01:36
categories:
- Unreal Engine
tags: UE DistanceField
comments: true
---


[Mesh Distance Fields](https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LightingAndShadows/MeshDistanceFields/){:target="_blank"}관련 Unreal Engine Documentation을 참고하여 작성되었습니다. Unreal Engine를 개발할 때 사용할 수 있는 Distance Field의 사용에 대한 개요를 서술합니다.

<!-- more -->

# Distance Field
언리얼 엔진은 Distance Field를 활용하여 Static Mesh Actor를 위한 dynamic ambient occlusion 및 그림자 기능을 제공합니다. 이 외에도, Actor의 Mesh Distance Field representation은 GPU particle collision이나 동적 흐름 맵을 만드는 Material Editor와 함께 사용될 수 있습니다.

## Signed Distance Field
Static Mesh의 표면을 나타내기 위해서 **Signed Distance Field (SDF)**가 사용됩니다. Signed Distance Field란 위치를 입력으로 받아 해당 위치에서 object의 가장 가까운 부분까지의 거리를 출력하는 함수를 이용해 object를 나타내는 방식입니다. UE에서 이는 volume texture에 가장 가까운 표면까지의 거리를 저장하여 작동합니다. Mesh 외부의 모든 점은 양의 거리로 간주되고 메쉬 내부의 모든 점은 음의 거리로 저장합니다.  
<p align="center"><img src="/assets/images/Image_UE5/SDF.png" width="300" height="300" /> </p>
*[<span style='color:#adadad'>그림 1. Signed Distance Field가 픽셀에서 어떻게 보이는지에 대한 예</span>](http://bytewrangler.blogspot.com/2011/10/signed-distance-fields.html){:target="_blank"}*
{: .text-center }

## Mesh Distance Field
Level에 배치된 Actor는 모두 Mesh Distance Field로 구성됩니다. Mesh Distance Field가 생성될 때 결과를 volume texture에 저장하는 triangle raytracing을 사용하여 **"오프라인"**으로 생성됩니다. 이 때문에 Mesh Distance Field 생성은 런타임에 수행할 수 없습니다. 이 방법은 모든 방향에서 Signed Distance Field 광선을 계산하여 가장 가까운 표면을 찾고 해당 정보를 저장합니다.
![MDF](/assets/images/Image_UE5/ODFVisualization.webp)
회색보다 흰색에 가까운 영역이 표시되면 메쉬 표면의 교차점을 찾는 데 많은 단계가 필요했음을 의미합니다. 표면에 대한 grazing angle(스침각: 입사 광선과 반사 표면 사이의 각도)의 광선은 단순한 메시보다 교차하는 데 훨씬 더 많은 단계를 거칩니다.
<p align="center"><img src="/assets/images/Image_UE5/grazing_angle.png"/> </p>
*[<span style='color:#adadad'>Grazing Angle</span>](https://www.mathworks.com/help/radar/ref/grazingang.html){:target="_blank"}*
{: .text-center }

### Enabling Mesh Distance Field
Mesh Distance Field를 활성화하기 위해서는 [Edit] - [Project Settings] - [Rendering] - [Lighting] - [Generate Mesh Distance Fields]를 체크합니다.
<p align="center"><img src="/assets/images/Image_UE5/GeneratedMeshDF.webp" width="300" height="300"/> </p>

### Visualize Mesh Distance Field
뷰포트에서 전역 거리 필드를 시각화기 위해서는 [Show] - [Visualize] - [Mesh Distance Field]를 체크합니다.
<p align="center"><img src="/assets/images/Image_UE5/MeshDF.webp" width="300" height="300" /> </p>
단일 메시가 가질 수 있는 최대 볼륨 텍스처 크기는 128x128x128 해상도에서 8MB입니다.

## Global Distance Field
Global Distance Field는 해당 Level에서 카메라를 따라 Signed Distance Field occlusion을 사용하는 low-resolution Distance Field입니다. 이는 object 별 Mesh Distance Field의 캐시를 생성하고 카메라를 중심으로한 몇 개의 볼륨 텍스처인 clipmap으로 합성합니다. 새로 보이는 영역이나 장면 수정의 영향을 받는 영역만 업데이트하면 되기 때문에 구성 비용이 많이 들지 않습니다.
![MDF](/assets/images/Image_UE5/GDFVisualization.webp)

### Visualize Global Distance Field
뷰포트에서 전역 거리 필드를 시각화기 위해서는 [Show] - [Visualize] - [Global Distance Field]를 체크합니다.
<p align="center"><img src="/assets/images/Image_UE5/EnableGDFViewMode.webp" width="300" height="300" /> </p>


# 참고
* https://docs.unrealengine.com/4.27/en-US/BuildingWorlds/LightingAndShadows/MeshDistanceFields/
* http://bytewrangler.blogspot.com/2011/10/signed-distance-fields.html
* https://www.mathworks.com/help/radar/ref/grazingang.html

