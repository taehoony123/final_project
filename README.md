# final_project


# 정답

1-1 p5.js 특징 설명<br/>

1)간단한 문법: p5.js는 직관적이고 간결한 문법을 제공하여 초보자도 쉽게 배울 수 있습니다.<br/>
2)웹 친화적: 자바스크립트 기반으로 웹 브라우저에서 바로 실행할 수 있어, 별도의 설치 없이도 손쉽게 시작할 수 있습니다.<br/>
3)풍부한 기능: 2D 및 3D 그래픽, 사운드, 비디오, 데이터 시각화 등 다양한 멀티미디어 작업을 지원합니다.<br/>
4)오픈 소스: 무료로 사용할 수 있으며, 활발한 커뮤니티가 지속적으로 개선하고 있습니다.<br/>
5)다양한 활용: 교육, 예술, 인터랙티브 설치, 데이터 시각화 등 다양한 분야에서 활용할 수 있습니다.<br/>
<br/>
<br/>
1-2 인터랙티브 아트 개념 설명

인터랙티브 아트는 관객의 참여를 통해 작품이 변화하거나 반응하는 예술 형태를 말합니다. 
디지털 기술을 활용하여 관객의 행동이나 입력에 따라 실시간으로 변하는 그래픽, 소리, 움직임 등을 포함합니다.
 이러한 작업은 종종 감각적이고 몰입감 있는 경험을 제공합니다.

<br/>
<br/>
1-3 예제코드

function setup() {<br/>
    createCanvas(windowWidth, windowHeight);<br/>
    background(255); // Set background to white<br/>
}<br/>

function draw() {<br/>
    // No need to clear the background in draw(), we want to accumulate circles<br/>
}<br/>

function mouseMoved() {  마우스가 움직일 때마다 호출 됩니다.<br/>
    // Draw a circle at the mouse position with random color<br/>
    fill(random(255), random(255), random(255));<br/>
    noStroke();<br/>
    ellipse(mouseX, mouseY, 20, 20); // Draw a circle with diameter 20<br/>
}<br/>

--------------------------------------------------------------------------------------------------
2-1 ml5.js 기능과 장점 설명

1)사용자 친화적: 직관적이고 간결한 API를 제공하여 머신러닝의 복잡성을 줄이고, 초보자도 쉽게 접근할 수 있습니다.<br/>
2)웹 친화적: 브라우저 내에서 바로 실행할 수 있어, 설치나 설정 없이 간편하게 시작할 수 있습니다.<br/>
3)다양한 모델 지원: 이미지 분류, 포즈 인식, 스타일 트랜스퍼, 텍스트 생성 등 다양한 머신러닝 모델을 지원합니다.<br/>
4)오픈 소스: 무료로 사용 가능하며, 활발한 커뮤니티가 지속적으로 개선하고 있습니다.<br/>
5)실시간 처리: 브라우저에서 실시간으로 데이터를 처리할 수 있어 인터랙티브한 애플리케이션 개발이 가능합니다.<br/>

<br/>
<br/>
2-2 이미지 분류 구현 과정 서술

1)HTML 파일 설정: ml5.js와 p5.js 라이브러리를 포함한 HTML 파일을 작성합니다.
2)모델 로드 및 예측: ml5.js의 imageClassifier 기능을 사용하여 사전 학습된 모델을 로드하고 이미지를 분류합니다.
3)결과 표시: 예측 결과를 화면에 표시합니다.<br/>


이것을 소스코드로 보자면<br/>

let classifier;<br/>
let img;<br/>

function preload() {<br/>
    // 이미지와 모델을 사전 로드<br/>
    img = loadImage('path_to_your_image.jpg'); // 이미지 파일 경로를 설정<br/>
    classifier = ml5.imageClassifier('MobileNet'); // MobileNet 모델 로드<br/>
}<br/>

function setup() {<br/>
    createCanvas(400, 400);<br/>
    image(img, 0, 0, width, height); // 이미지를 캔버스에 그리기<br/>
    classifier.classify(img, gotResult); // 이미지를 분류<br/>
}<br/>

function gotResult(error, results) {<br/>
    if (error) {<br/>
        console.error(error);<br/>
        return;<br/>
    }<br/>
    // 결과를 콘솔에 출력<br/>
    console.log(results);<br/>
    // 분류 결과를 화면에 표시<br/>
    let label = results[0].label;<br/>
    let confidence = nf(results[0].confidence, 0, 2);<br/>
    fill(0);<br/>
    textSize(24);<br/>
    textAlign(CENTER);<br/>
    text(`${label} (${confidence})`, width / 2, height - 10);<br/>
}<br/>
<br/>
<br/>
2-3이미지 분류모델의 윤리 설명

이미지 분류 모델은 입력된 이미지를 특정 클래스(예: 고양이, 강아지, 자동차 등)로 분류하는 머신러닝 모델입니다. 이 모델은 다음과 같은 과정을 통해 작동합니다:

1)특징 추출: 모델은 이미지의 중요한 특징(예: 가장자리, 질감, 패턴 등)을 추출합니다. 이는 여러 계층의 필터를 통해 이루어집니다.
2)피드포워드 신경망: 추출된 특징은 신경망의 여러 계층을 통과하며, 각 계층에서 특징이 더욱 추상화되고 고차원적으로 변환됩니다.
3)분류기: 마지막 계층에서는 추상화된 특징을 기반으로 각 클래스에 대한 확률을 계산합니다. 가장 높은 확률을 가진 클래스가 예측 결과로 선택됩니다.

MobileNet과 같은 사전 학습된 모델은 대규모 이미지 데이터셋(예: ImageNet)에서 미리 학습되어 있어, 새로운 이미지에 대해 빠르고 정확한 분류를 수행할 수 있습니다. ml5.js는 이러한 복잡한 과정을 간단한 API 호출로 처리할 수 있도록 하여, 사용자들이 쉽게 머신러닝 기능을 활용할 수 있게 합니다.



--------------------------------------------------------------------------------------------------


3-1 three.js의 주요 구성요소 설명<br/>
1)Scene (장면): 3D 객체들이 배치되는 공간입니다. 모든 3D 그래픽 요소는 이 장면에 추가됩니다.<br/>
2)Camera (카메라): 장면을 관찰하는 시점을 정의합니다. 다양한 종류의 카메라가 있지만, 일반적으로 PerspectiveCamera를 많이 사용합니다.<br/>
3)Renderer (렌더러): 장면과 카메라를 기반으로 3D 그래픽을 화면에 그려주는 역할을 합니다. 일반적으로 WebGLRenderer를 사용합니다.<br/>
4)Mesh (메쉬): 기하학적 형태와 재질(Material)을 결합하여 3D 객체를 만듭니다. 예를 들어, BoxGeometry와 MeshBasicMaterial을 사용하여 큐브를 만들 수 있습니다.<br/>
5)Light (조명): 장면에 빛을 추가하여 3D 객체가 더 현실감 있게 보이도록 합니다. AmbientLight, DirectionalLight 등이 있습니다.<br/>
<br/>

<br/>

3-2 3D 장면 구성 과정 설명

1)Scene 생성: 장면 객체를 생성합니다.<br/>
2)Camera 설정: 장면을 관찰할 카메라를 설정합니다.<br/>
3)Renderer 생성: 장면을 화면에 렌더링할 렌더러를 생성합니다.<br/>
4)3D 객체 추가: 메쉬를 생성하고 장면에 추가합니다.<br/>
5)Light 추가: 장면에 조명을 추가합니다.<br/>
6)애니메이션 루프 설정: 객체의 애니메이션을 구현하기 위해 렌더링 루프를 설정합니다.<br/>
<br/>

<br/>
3-3 예제 코드 작성 및 설명

예제 코드로 회전하는 큐브로 설명을 할 수 있습니다.

// 장면, 카메라, 렌더러 생성<br/>
const scene = new THREE.Scene();<br/>
const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);<br/>
const renderer = new THREE.WebGLRenderer();<br/>
renderer.setSize(window.innerWidth, window.innerHeight);<br/>
document.body.appendChild(renderer.domElement);<br/>

// 큐브 생성<br/>
const geometry = new THREE.BoxGeometry();<br/>
const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });<br/>
const cube = new THREE.Mesh(geometry, material);<br/>
scene.add(cube);<br/>

// 카메라 위치 설정<br/>
camera.position.z = 5;<br/>

// 애니메이션 루프 설정<br/>
function animate() {<br/>
    requestAnimationFrame(animate);<br/>

    // 큐브 회전<br/>
    cube.rotation.x += 0.01;<br/>
    cube.rotation.y += 0.01;<br/>

    // 장면 렌더링<br/>
    renderer.render(scene, camera);<br/>
}<br/>

// 애니메이션 시작<br/>
animate();<br/>

// 창 크기 변경 시 카메라와 렌더러 크기 조정<br/>
window.addEventListener('resize', () => {<br/>
    camera.aspect = window.innerWidth / window.innerHeight;<br/>
    camera.updateProjectionMatrix();<br/>
    renderer.setSize(window.innerWidth, window.innerHeight);<br/>
});<br/>




--------------------------------------------------------------------------------------------------

4-1 R3F의 특징 및 이점 설명

1)React와의 통합: R3F는 Three.js를 React의 컴포넌트 방식으로 사용할 수 있게 하여, React 개발자들이 익숙한 방식으로 3D 그래픽스를 구현할 수 있게 합니다.<br/>
2)선언적 방식: R3F는 선언적 문법을 사용하여 3D 장면을 구성합니다. 이는 코드의 가독성을 높이고 유지보수를 쉽게 합니다.<br/>
3)재사용성: React 컴포넌트를 활용하여 3D 객체를 모듈화하고 재사용할 수 있습니다.<br/>
4)상태 관리: React의 상태 관리 기능을 그대로 사용할 수 있어, 3D 객체의 상태를 손쉽게 관리할 수 있습니다.<br/>
5)애니메이션: React의 리렌더링 방식과 Three.js의 애니메이션 루프를 통합하여 애니메이션을 자연스럽게 구현할 수 있습니다.<br/>

<br/>

<br/>
4-2 R3F를 사용한 3D 장면 생성 과정 서술

1)React 프로젝트 설정: Create React App 등을 사용하여 React 프로젝트를 설정합니다.<br/>
2)R3F 설치: R3F 라이브러리를 설치합니다.<br/>
3)3D 장면 구성: R3F 컴포넌트를 사용하여 3D 장면을 구성합니다.<br/>
4)렌더링 설정: React 컴포넌트 내에서 3D 객체를 렌더링합니다.<br/>


<br/>

<br/>
4-3 예제 코드 작성 및 설명

예제코드로 회전하는 큐브로 설명 할 수 있습니다.

import React from 'react';
import { Canvas } from '@react-three/fiber';

function Box() {
  // Ref를 사용하여 메쉬에 접근
  const meshRef = React.useRef();

  React.useEffect(() => {
    const animate = () => {
      if (meshRef.current) {
        meshRef.current.rotation.x += 0.01;
        meshRef.current.rotation.y += 0.01;
      }
      requestAnimationFrame(animate);
    };
    animate();
  }, []);

  return (
    <mesh ref={meshRef}>
      <boxGeometry args={[1, 1, 1]} />
      <meshStandardMaterial color="orange" />
    </mesh>
  );
}

function App() {
  return (
    <Canvas>
      <ambientLight />
      <pointLight position={[10, 10, 10]} />
      <Box />
    </Canvas>
  );
}

export default App;

<br/>
이 코드는 R3F를 사용하여 회전하는 큐브를 포함한 간단한 3D 장면을 생성합니다. React의 컴포넌트 방식과 상태 관리 기능을 활용하여 Three.js의 복잡한 3D 그래픽스를 쉽게 구현할 수 있습니다.





