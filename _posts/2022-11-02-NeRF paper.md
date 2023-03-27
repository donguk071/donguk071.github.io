---
title: '[Paper Review] NeRF Paper Review'
date: 2022-11-03 00:00:42
categories:
- Paper Review
tags: NeRF
comments: true
---


[Paper Review] [NeRF: Representing Scenes as Neural Radiance Fields for View Synthesis](https://arxiv.org/pdf/2003.08934.pdf)

<!-- more -->

# ABSTRACT
본 논문은 몇 장의 사진을 사용하여 continuous volumetric scene function을 최적화하고 복잡한 scene의 novel view를 합성하기 위한 새로운 방법을 제시합니다. 알고리즘의 **입력**은 단일 연속 5D 좌표(**공간 위치(x, y, z) 및 바라보는 방향((θ, φ)**)이고, **출력**은 해당 공간 위치에서 **volume density**와 **view-dependent emitted radiance(color)**로 이를 **fully-connected deep network**를 통해 학습하여 렌더링합니다. 카메라 ray를 따라 **5D 좌표를 쿼리**하여 view를 합성하고 **volume rendering** 기술을 사용하여 출력 색상과 밀도를 이미지에 투영합니다. 본 논문은 scene의 사실적인 novel view를 렌더링하기 위해 **neural radiance field**를 효과적으로 최적화하는 방법을 설명하고, 기존의 neural rendering 및 view synthesis의 작업을 능가하는 결과를 보여줍니다. 
* * * 

<br>

[Code Review][NeRF Code Review](/review/2022/11/02/NeRF-code/){:target="_blank"}
# INTRODUCTION
## Neural 3D Represenation

3D 모델은 컴퓨터 비전 및 그래픽 분야에서 활발하게 사용되는 일반적인 데이터 형식입니다. 그러나 3D 데이터에 직접 사용할 수 있는 기계 학습 모델은 이미지와 비디오에서 작동하는 모델에 비해 부족합니다. 그 이유는 다음과 같습니다.
1. 3D 모델의 대규모 데이터 세트를 구축하는 데 시간이 많이 걸리고, 전문 3D 모델러 또는 3D 스캐너가 필요하기 때문입니다. 
2. 2D 데이터와 달리 3D 데이터는 그리드 구조가 존재하지 않기 때문입니다.

Convolution 및 Pooling과 같은 기계 학습 작업은 그리드 구조가 아닌 3D 데이터에 직접 사용할 수 없습니다. 따라서 3D Geometry를 나타낼 데이터 구조의 선택은 학습하기 위해 사용할 수 있는 알고리즘의 유형을 결정하기 때문에 중요합니다. 3D Geometry를 나타내는 방법을 **3D Representation**이라고 하며, 이는 크게 두 가지로 구분합니다.

- Traditional **Explicit** Representations ⇒ Discrete
- **Implicit** Neural Representation ⇒ Continuous

![[https://www.cvlibs.net/publications/Peng2020ECCV_slides.pdf](https://www.cvlibs.net/publications/Peng2020ECCV_slides.pdf)](/assets/images/Image_NeRF/3D Representation.png)
*[<span style='color:#adadad'>https://www.cvlibs.net/publications/Peng2020ECCV_slides.pdf</span>](https://www.cvlibs.net/publications/Peng2020ECCV_slides.pdf){:target="_blank"}*
{: .text-center }

### Explicit Representations 
Voxel, Point cloud이나 Mesh와 같은 전통적인 방식으로 3D Object를 나타내는 방법입니다. Voxel은 큰 resolution을 표현하지 못하고, Point cloud는 topology의 표현을 잃고, Mesh는 neural network로 학습하기 어렵습니다. 또한, 지금까지 이러한 모델은 일반적으로 합성 3D 형상 데이터 세트에서 얻은 실제 3D geometry의 필요로 인해 한계가 있었습니다.

### Implicit Representations
이에 최근 컴퓨터 비전의 연구 방향은 3D 공간 위치를 implicit representation으로 직접 매핑하는 deep network를 최적화하여 해당 weight를 통해 연속적인 3D 모양 집합으로 implicit하게 표현하는 것이었습니다.


그러나 지금까지 이러한 모델은 일반적으로 explicit한 모델의 성능과 크게 다를 바가 없거나, 합성 3D 형상 데이터 세트에서 얻은 실제 3D geometry가 필요하다는 한계가 있었습니다. 이에 NeRF는 5D radiance field를 인코딩하여 복잡한 장면의 novel view를 사실적으로 렌더링하여, 고해상도 geometry 및 외관을 나타내는 결과를 보여줍니다.


## Novel View Synthesis
NeRF는 성능이 높지 않았던 View Synthesis 분야에 새로운 방식을 제안하였습니다. 
View Synthesis는 특정 몇 개의 시점에서 촬영한 이미지셋으로부터 주어지지 않은 위치와 방향에서 바라본 대상의 novel view를 연속적으로 합성해내는 기술입니다. 

NeRF 이전에도 view synthesis와 관련한 연구로 mesh-based representation이나 volumetric representation과 같은 방법이 연구되었으나,
이러한 방법들은 이산 샘플링으로 인한 시간과 공간의 복잡성으로 인해 더 나은 해상도로 확장할 수 없는 한계를 가졌습니다. 
NeRF는 fully connected neural network의 파라미터를 통해 연속 volume을 인코딩함으로써 이 문제를 회피하였으며,
이는 이전의 volumetric 접근 방식보다 더 저렴할 뿐만 아니라 훨씬 더 높은 품질의 렌더링 결과를 보여줍니다.


# 참고
* https://www.antoinetlc.com/blog-summary/3d-data-representations
* https://keras.io/examples/vision/nerf/