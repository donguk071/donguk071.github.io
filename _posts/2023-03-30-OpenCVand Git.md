---
layout: post
title: "[환경구축] C / CPP + VScode + OpenCV + Git"
date: 2023-03-30
categories:  C/CPP 개발환경 VScode git ssh github
photos: /assets/post_images/titleImg/c_opencv_git.png
tags: [C/CPP,개발환경설정, VScode, git, ssh, github] 
description: " VScode 환경에서의 OpenCV 라이브러리 사용과 Git ssh 정리"
published: true
---


# 환경 세팅  
  
 <br/>

시작하기 앞서 이전 포스팅을 보고 오는것 을 추천한다. [VScode에서 CPP 개발환경 구축](https://github.com/ninja-build/ninja/releases)

<br/>

## git hub

git을 사용할 때 SSH를 사용하면 보안성과 속도 면에서 이점을 얻을 수 있다.

```bash
cd ~ 
ls .ssh # 최초설정이라면 별 내용이 생기지않을 것
ssh-keygen
ls .ssh #id_rsa  id_rsa.pub  known_hosts 이런식에 무언가 나와야한다, 사전 git 사용 여부에 따라 조금 달라질 수 있다.
cat .ssh/id_rsa.pub #id_rsa는 개인키임으로 유출하지 않도록 조심하자
#다음 값을 모두 복사한다(ssh-rsa AA~~~~) 복사한 값은 github 설정에서 SSH key에 적당한 이름과 함께 등록해준다
ssh -T git@github.com #깃허브와 연결해준다

#git 설정이 처음인 사람들은 git config 를 통해 이메일과 유저명을 추가적으로 등록해주어야한다
```

![Untitled](/assets/post_images/vscSetting/Untitled4.png)

SSH key등록을 하는 github 설정 창이다. 만약 모든 과정을 잘 마무리하였다면 문제없이 SSH를 이용하여 프로젝트를 clone해올 수 있을 것이다. 

 <br/>

## OpenCV 환경 구축

 <br/>

1. 적당한 버전에 opencv를 본인 환경에 맞도록 다운 받는다. mac은 직접 빌드하여야한다. 
    
    [https://opencv.org/releases/](https://opencv.org/releases/)
    
2. 프로젝트 root에  빈 thrid_party 폴더를 생성한다.
3. 다운 받은 opencv exe파일을 실행하고 앞서 만든 thrid_party의 경로로 설치 경로를 바꿔준다. 
4. cmake 파일이 다운 받은 opencv 폴더를 인식할 수 있도록 cmakelists.txt 를 수정한다.
    
    ```makefile
    cmake_minimum_required(VERSION 3.0.0)
    project(Top)
    
    # OpenCV 4.7.0
    set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/third_party/opencv/build)
    set(OpenCV_STATIC_LIB  ${OpenCV_DIR}/x64/vc16/lib/opencv_world470.lib)
    set(OpenCV_DYNAMIC_LIB ${OpenCV_DIR}/x64/vc16/bin/opencv_world470.dll)
    include_directories(${OpenCV_DIR}/include)
    
    # Data
    
    # Projects
    
    #cmake 의 기본적인 함수들은 아래 블로그를 참고하면 좋을 것 같다.
    #https://coding-robot.tistory.com/8
    #https://www.tuwlab.com/ece/27260
    ```
    
5. 이제 Variant를 Release로 설정한 후  build all 을 시도하여본다 마찬가지로 status bar에서 조절이 가능하다.
    
    ![Untitled](/assets/post_images/vscSetting/Untitled5.png)
 
6. 이제 원하는 cpp 파일을 실행하거나 디버그 하면 된다!(status bar을 이것저것 눌러보며 기능을 탐색하는 것을 추천한다.)

![Untitled](/assets\post_images\vscSetting\Untitled6.png)


<br/>

궁금한 점이 있다면 남겨주세요! 함께 고민해보겠습니다.

------------------------