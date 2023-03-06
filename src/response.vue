

<template>
      <canvas id="c"></canvas>
</template>


<script setup>
import { onMounted} from 'vue'
import * as THREE from 'three';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';


console.log('here')

onMounted(() => {
  const scene = new THREE.Scene();


const fov = 75;
const aspect = 2;  // the canvas default
const near = 0.1;
const far = 5;
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
camera.position.z = 2;


const canvas = document.querySelector('#c');
const renderer = new THREE.WebGLRenderer({antialias: true, canvas});

const boxWidth = 1;
const boxHeight = 1;
const boxDepth = 1;
const geometry = new THREE.BoxGeometry(boxWidth, boxHeight, boxDepth);
// const material = new THREE.MeshPhongMaterial({color: 0x44aa88}); 
//  new THREE.MeshBasicMaterial( { color: 0x44aa88 } );
// const cube = new THREE.Mesh( geometry, material );
// scene.add( cube );

function makeInstance(geometry, color, x) {
  const material = new THREE.MeshPhongMaterial({color});
  const cube = new THREE.Mesh(geometry, material);
  scene.add(cube);
  cube.position.x = x;
  return cube;
}

const cubes = [
  makeInstance(geometry, 0x44aa88,  0),
  makeInstance(geometry, 0x8844aa, -2),
  makeInstance(geometry, 0xaa8844,  2),
];

const color = 0xFFffff;
const intensity = 1;
const light = new THREE.DirectionalLight(color, intensity);
light.position.set(-1, 2, 4);
scene.add(light);

function resizeRendererToDisplaySize(renderer) {
  const canvas = renderer.domElement;
    const pixelRatio = window.devicePixelRatio;
    const width  = canvas.clientWidth  * pixelRatio | 0;
    const height = canvas.clientHeight * pixelRatio | 0;
    const needResize = canvas.width !== width || canvas.height !== height;
    if (needResize) {
      renderer.setSize(width, height, false);
    }
    return needResize;
}

function render(time) {
    
  time *= 0.001;  // convert time to seconds


  if(resizeRendererToDisplaySize(renderer)){
    
  const canvas = renderer.domElement;
  camera.aspect = canvas.clientWidth / canvas.clientHeight;
  camera.updateProjectionMatrix();
  }
  
//   console.log('time',time)
//   cube.rotation.x = time;
//   cube.rotation.y = time;

    // cubes.forEach((cube, ndx) => {
    //     const speed = 1 + ndx * .1;
    //     const rot = time * speed;
    //     cube.rotation.x = rot;
    //     cube.rotation.y = rot;
    // });
 
  renderer.render(scene, camera);
 
  requestAnimationFrame(render);
}
requestAnimationFrame(render);





})


</script>

<style>
html, body {
   margin: 0;
   height: 100%;
}
#app{
  height: 100%;
}
#c {
   width: 100%;
   height: 100%;
   display: block;
}
</style>