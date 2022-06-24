# [SWTT] Three.js Tutorial

## 오픈소스SW입문 기말과제 _ 202021069 한수빈


- Preparation
Visual Studio Code 설치 https://code.visualstudio.com/download

- Three.js 설치
1. 공식 문서에서 직접 다운
https://threejs.org/
2. npm으로 설치 (미리 node.js 설치)
https://threejs.org/docs/index.html#manual/ko/introduction/Installation
3. BoilerPlate Webpack 설치
https://github.com/aakatev/three-js-webpack

- Three.js 기본 구조
Renderer_ Camera에 담긴 Scene을 웹사이트에 구현
Scene_ 여러 3D 오브젝트와 빛이 모인 장면
Camera_ 장면을 화면에 담기 위한 카메라

- 3D 도형 만들기
* Box Geometry
Scene에 cube추가하고 회전을 통해 정육면체 확인
* Renderer Option
Anti-aliasing & Opacity
* 반응형 처리
Window의 크기에 맞춰 배경과 object 크기도 조정됨
