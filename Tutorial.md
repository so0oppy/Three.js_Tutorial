## Three.js에 대한 소개와 기본 구조들을 활용하여 간단한 예제 구현하기
-------------------
- visual studio code (vscode) 미리 설치 권장


### Three.js 설치 방법
1. Three.js 공식 문서에서 직접 다운로드 https://threejs.org/ 
2. npm을 이용하여 다운로드(node.js 미리 설치) https://threejs.org/docs/index.html#manual/ko/introduction/Installation
3. Boilerplate(webpack) 사용 https://github.com/aakatev/three-js-webpack 
-----------------



### 웹팩이라는 모듈 번들러를 활용한 보일러플레이트를 설치하는 방법으로 three.js 설치하는 과정
- 웹팩이란?
    - 웹 애플리케이션을 구성하는 자원 즉, html, css, js, image등을 각각의 모듈로 보고 이를 병합된 하나의 결과물로 만드는 도구
    - 따라서, 웹 최적화를 위해 웹팩 사용을 추천
![boilerplate](https://user-images.githubusercontent.com/80036437/175783090-f535aad5-5eb8-424d-b28a-7c7d3b1fd856.png)
- 보일러플레이트란?
    - 기초 골격을 통으로 찍어내는 플레이트로, 매번 반복적인 코드를 짤 필요가 없는 코드를 의미
<br>

<p> - 웹팩 제공 깃헙 링크에 접속 > 사이트 하단에 나와있는 코드를 복사하여 vscode 터미널에 복사합니다. </p>
<img width="464" alt="git clone" src="https://user-images.githubusercontent.com/80036437/175782989-82e7ceb5-5690-4730-93bc-f300b3991a86.png">
<p> - 클론이 끝났으면, vscode에서 $cd 명령어를 통해 웹팩인 three-js-webpack 파일로 이동합니다. </p>
<img width="433" alt="cd" src="https://user-images.githubusercontent.com/80036437/175783303-cd6ede19-b934-442e-bf1f-e9bd473c4c87.png">
<p> - $npm i 명령어를 통해 json패키지 정보를 가지고 추가적인 모듈도 설치합니다. </p>
<p> - 먼저, 웹팩 내의 index.html파일로 들어갑니다. </p>
<p> - vscode 우측 하단의 Go Live 버튼을 통해 웹 서버를 실행하면, 웹팩에 만들어진 예제를 확인할 수 있습니다. </p>
<img width="800" alt="webpack" src="https://user-images.githubusercontent.com/80036437/175783478-13a7d393-6dd4-4a14-b677-e1ff786f90ec.png">
<p> - vscode에서 webpack.config.js 파일을 확인해보면, path를 가져와서 module export부분에 있는 entry인 index js파일을 bundle js파일로 변환하여 내보내는 것도 확인가능합니다. </p>
<p> - 그리고 src/webgl.js를 들어가보면 webgl에 대해 제공하는 브라우저인지 아닌지 확인해주는 코드가 있습니다. </p>
<p> - src/module.js 폴더는 필요 없으므로 삭제합니다. </p>
<p> - index.js 파일을 들어가보면, import를 통해 three를 불러왔고, 아까 봤던 webgl 스크립트를 불러온 것 확인가능하고 nodule파일은 지웠으므로 import './modal'는 삭제합니다. </p>
<p> - index.js 파일 내에 if문을 살펴보면, webgl이 가능한지 체크하는 코드가 있는데, 앞으로 여기에 추가적인 코드를 작성할 예정입니다. 그래서 우선 마지막 줄의 else문을 제외한 나머지 코드는 전부 삭제해주세요. </p>
<p> - 마지막으로, if문 안에 console.log를 넣어 three가 제대로 불러와졌는지 확인합니다. 아까 들어갔던 웹페이지로 다시 들어가서 개발자 도구를 확인해보면 모듈이 제대로 불러와진 것을 확인할 수 있습니다. </p>
<img width="250" alt="console" src="https://user-images.githubusercontent.com/80036437/175783801-548122db-61be-4d47-96b0-5f58a838e418.png">
<p> - 다시 vscode로 돌아가서, 불필요한 코드는 삭제해줍니다. index.html에서 body부분에 script를 제외한 나머지 코드는 삭제하고, style폴더의 main.css파일에서도 canvas{ }부분을 제외하고 삭제해줍니다. 그리고 texture폴더도 삭제해줍니다.</p>
<br>

-----------------

### THREE.js 기본 구조 이해하기
<p>Three.js의 기본구조는 크게 renderer, scene, camera가 있습니다.</p>
<p>장면을 만들어서 그 안에 3D 오브젝트를 넣고, 그걸 카메라로 비춘 다음 renderer를 통해 html파일에 보여주는 구조입니다.</p>
<br>

- Renderer: camera와 scene의 객체 데이터를 넘겨 받아서 화면 안에 이미지로 렌더링
- Scene: 여러 3D 오브젝트와 빛들이 모인 장면으로, 배경색, 안개 등의 요소 포함
- Camera: 장면을 화면에 담기 위한 요소이며, 카메라로 비춘 부분만 렌더러로 보냄
  - 예를 들면, 시야각, 종횡비, 카메라 시작 끝 지점과 카메라 위치 등을 설정할 수 있습니다.
<br>

<p>이제, 기본적인 코드를 통해 설명하겠습니다.
<br>

우선, if문 안에 장면 먼저 넣어주겠습니다.

```
const scene = new THREE.Scene();
```
<br>

다음으로 카메라 코드도 입력합니다.
```
const camera = new THREE.PerspectiveCamera();
```
<p>PerspectiveCamera의 괄호 안에는 화각, 종횡비, 가까운 부분, 먼 부분 을 숫자로 설정할 수 있습니다.</p>
<p>각각 75, window.innerWidth/window.innerHeight, 0.1, 1000으로 설정합니다.</p>
<br>

다음으로 렌더러도 추가해줍니다.
```
const renderer = new THREE.WebGLRenderer();
```

렌더러의 사이즈는
```
renderer.setSize(window.innerWidth, window.innerHeight); 
```
이렇게 설정해줍니다.
<br>

이제, 렌더러의 장면을 어디에, 어떤 태그에 노출시킬건지 정할 코드를 작성합니다.

```
document.body.appendChild(renderer.domElement); 
```

이렇게 appendChild를 통해 html body에 renderer요소를 추가해주고,

```
renderer.render(scene, camera); 
```

를 통해 scene과 camera도 연결시켜줍니다.
<br>

<p>실행 시키기전에 webpack config js파일을 확인해서 entry가 방금 수정한 파일명으로 되어있는지 확인합니다.</p>
<p>그리고 서버를 실행하면 검은 화면이 나오게 됩니다.</p>
<br>

제대로 실행된건지 확인하기 위해 아까 수정한 코드에서 장면 밑에

```
scene.background = new THREE.Color(0x004fff); 
```
<p>를 넣어줍니다.</p>

<img width="632" alt="bluepage" src="https://user-images.githubusercontent.com/80036437/175785024-fa763c9a-c2cd-4d4f-ac1b-87b7c7ea0144.png">
<p>다시 웹을 reload하면 파란색으로 배경색이 바뀐것을 확인할 수 있습니다.</p>

<br>
<br>

--------------------------

추가로, 애니메이션 코드를 넣고 싶다면,
```
function render(time) {
  time *= 0.001;  // convert time to seconds
 
  cube.rotation.x = time;
  cube.rotation.y = time;
 
  renderer.render(scene, camera);
 
  requestAnimationFrame(render);
}
requestAnimationFrame(render);
```

<p>렌더링을 loop하는 코드인 render(time)함수를 renderer.render코드 하단에 붙여넣습니다. </p>
<p>렌더 함수 안에 renderer.render()코드가 있기 때문에 기존의 겹치는 코드는 지워줍니다.</p>
<br>

<p>그리고, 아직 도형에 관련된 코드는 필요없으므로 cube.rotation코드는 주석처리 해주고, 렌더러의 setSize는 윈도우의 너비와 높이 값으로 렌더러의 사이즈를 지정해준 것이므로 css값으로 크기를 조정하고 싶다면 이 코드도 지워도 됩니다.
<p>*아직 도형을 넣지 않았기 때문에 웹을 확인해보면 겉보기에는 달라진 부분이 없을 겁니다.*</p>

