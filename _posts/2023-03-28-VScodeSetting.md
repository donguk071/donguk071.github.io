---
layout: post
title: "[환경구축] C / CPP + VScode"
date: 2023-03-28
categories:  C/CPP 개발환경 Cmake Clang Ninja VScode
photos: /assets/post_images/titleImg/vsc_c_cpp.png
tags: [C/CPP,개발환경설정, CS용어정리, VScode] 
description: "Cmake Clang Ninja를 이용한 VScode 개발 환경 구축과 간단한 개념 정리"
published: true
---

<br/>
<br/>

# 환경 세팅  
  
   
## Visual studio code 에서 c/cpp 환경구축
<br/>
이하 내용은 전부 window 환경을 전제한다.
<br/>

<aside>
💡 c/cpp 개발 환경을 vscode에서 구축하는 방법을 학습한다. visual studio와 같은 c 개발에 용이한 환경을 만들기 위해서는 CMake, LLVM-Clang, Ninja를 설치하여야 한다.

</aside>

Cmake : 프로젝트를 관리해주는 파일, 외부 라이브러리 링크, 소스코드 관리 등의 기능을 한다.(빌드 파일을 생성하는 프로그램)

LLVM-Clang : clang은 LLVM을 사용하여 컴파일 하기 때문에 최적화 단계에서 더 빠르게 실행이 가능하며, 타 컴파일러에 비해 엄격한 C++ 규칙을 적용하기 때문에 더욱 정확한 오류 메시지를 제공한다. 또한 라이선스 측면에서의 이점도 존재하는듯하다.

Ninja : cmake와 비슷한 build tool, 일반적으로 기본 make 와 같은 tool에 비해 빠르다고 알려져 있다. cmake 와 함께 사용한다. 

[ninja releases 설치링크](https://github.com/ninja-build/ninja/releases)

[llvm releases 설치링크](https://github.com/llvm/llvm-project/releases)

<br/>

개발환경 : 

```c
C:\Users\oooo>cmake --version
cmake version 3.25.2
C:\Users\oooo>ninja --version
1.11.1
C:\Users\oooo>clang --version
clang version 15.0.7
```
<br/>

Ninja 설치 시 유의 사항

- C:\ProgramFiles\Ninja\bin 경로 폴더 만든 후 ninja.exe 파일 추가
- C:\ProgramFiles\Ninja\bin\ 경로 시스템 환경 변수에 추가 (all users에 추가하는 것을 추천)

<br/>

## install extention

<aside>
>💡 recommend vs code extensions  <br/>
C/C++ : microsoft <br/>
C/C++ Extension Pack: microsoft <br/>
>CMake Tools: microsoft
</aside>
 <br/>

## starting project

 <br/>
이하 모든과정은 vs code 에서 ctrl + shift + p 를 눌러 탐색이 가능하다.
 <br/> 

1. 프로젝트 생성을 원하는 폴더에 command palette 에서 Cmake:Quick Sart 선택

    ![Untitled](/assets/post_images/vscSetting/Untitled.png)

2. Scan for kits 선택
    - 컴퓨터에 깔려있는 compiler 찾아준다.
    
    ![Untitled](/assets/post_images/vscSetting/Untitled1.png)

3. 1 번 반복

4. 원하는 compiler 선택(예제 경우 clang_cl 이 아닌 clang 선택)
    - clang_cl 은 visual studio 20XX용이다

5. 프로젝트명 입력 및 library executable 중 선택
    ![Untitled](/assets/post_images/vscSetting/Untitled2.png)

6. CMake: configure  (generate a build system for your project based on the contents of your env)

7. 하단 Status bar에서 프로젝트 빌드, 실행 등 진행 가능 , CMake: Select Variant 에서 Debug, Release 등 선택 가능
    ![Untitled](/assets/post_images/vscSetting/Untitled3.png)

 <br/>

## 기본 용어 정리

 <br/>

- object code : source code를 compile 한 결과물이다. 

- exe vs obj : complie 을 거치면 exe와 obj 파일이 생성된다. 먼저 exe file은 실행 가능한 파일로, 프로그램의 실행을 위해 필요한 모든 리소스를 포함한다. 이 필요한 리소스들이 바로 obj 파일이다. obj 파일은 컴파일된 코드와 데이터만을 포함하고 있으며, 링커에 의해 .exe 파일로 결합된다. 즉 .obj 파일은 .exe 파일을 만들기 위한 중간 단계의 파일이라고 할 수 있다.

- linker : obj 파일을 결합하여 실행 가능한 바이너리 파일을 생성한다.

- build : 컴파일, 링크, 바이너리파일 테스트 등을 진행하는 일련에 과정 

- Debug / Release : debug 모드를 통한 빌드시 선택 시 좀 더 구체적인 에러 메시지를 확인이 가능하며(당연히 시간은 더욱 오래 걸린다) release는 배포를 목적으로 한다, 상황에 따라 둘 중 적합한 것을 사용해주자 

- configure : 프로그램을 만들 때, 소스 코드를 컴파일하여 실행 파일을 만들어야 한다. 그러나 소스 코드가 복잡하고 여러 파일로 구성되어 있을 경우, 이를 수동으로 컴파일하는 것은 매우 어렵다. 이때 `cmake`와 `configure`와 같은 빌드 시스템을 사용하면, 소스 코드를 컴파일하는 데 필요한 모든 설정을 자동으로 수행할 수 있다

- cmake : configure 의 단점을 보완한 것으로, `cmake`를 사용하여 프로젝트를 구성하면, `CMakeLists.txt` 파일에 지정된 대로 빌드 구성을 생성할 수 있다. 이 구성은 빌드 환경에 따라 다르며, 예를 들어 Windows에서는 Visual Studio 프로젝트 파일을 생성하고, Linux에서는 Makefile을 생성할 수 있다. cmake configure단계는 `cmake`를 실행할 때 자동으로 수행되며,(빌드 폴더가 생성된다) 이후에는 `cmake build` 단계를 수행하여 실제 빌드를 수행할 수 있다. 이를 통해 코드를 더 쉽게 빌드하고 실행 파일을 만들 수 있다.



<br/>

궁금한 점이 있다면 남겨주세요! 함께 고민해보겠습니다.

------------------------