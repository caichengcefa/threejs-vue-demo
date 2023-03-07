

<template>
      <canvas id="c"></canvas>
</template>


<script setup>
import { onMounted} from 'vue'
import * as THREE from 'three';
import {OrbitControls} from 'three/addons/controls/OrbitControls.js';
import {GUI} from 'three/addons/libs/lil-gui.module.min.js';

const gui = new GUI();


// Turns b

onMounted(() => {
  const canvas = document.querySelector('#c');
  const renderer = new THREE.WebGLRenderer({antialias: true, canvas});

  const fov = 45;
  const aspect = 2;  // the canvas default
  const near = 0.1;
  const far = 100;
  const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);


  camera.position.set(0, 0, 100);
  camera.up.x = 1;
  camera.up.y = 1;
  camera.up.z = 0;
  // // // 浏览器控制台查看.up属性的默认值
  // // console.log(`.up属性值`,camera);
  camera.lookAt(0,0,0);


  const scene = new THREE.Scene();
  scene.background = new THREE.Color('black');
	scene.add(new THREE.AxesHelper(1000))

  var material = new THREE.MeshBasicMaterial( {color: 0x00ff00} );
  var geometry = new THREE.BoxGeometry( 10, 10, 10 );
  var cube = new THREE.Mesh( geometry, material );
  scene.add( cube );


  var material2 = new THREE.MeshBasicMaterial( {color: 0xffff00} );
  var geometry2 = new THREE.BoxGeometry( 10, 10, 10 );
  var cube2 = new THREE.Mesh( geometry2, material2 );
  cube2.position.x = 10
  scene.add( cube2 );

  function resizeRendererToDisplaySize(renderer) {
    const canvas = renderer.domElement;
    const width = canvas.clientWidth;
    const height = canvas.clientHeight;
    const needResize = canvas.width !== width || canvas.height !== height;
    if (needResize) {
      renderer.setSize(width, height, false);
    }
    return needResize;
  }

  function render() {

    if (resizeRendererToDisplaySize(renderer)) {
      const canvas = renderer.domElement;
      camera.aspect = canvas.clientWidth / canvas.clientHeight;
      camera.updateProjectionMatrix();
    }

    
    cube.rotation.y += 0.01;
    // cube.rotation.y += 0.01;
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