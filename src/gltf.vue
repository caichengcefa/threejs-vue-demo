

<template>
    <canvas id="c"></canvas>
</template>

<script setup>
import { onMounted} from 'vue'
import * as THREE from 'three';
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js';



onMounted(() => {

const scene = new THREE.Scene();


const fov = 75;
const aspect = 2;  // the canvas default
const near = 0.1;
const far = 5;
const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);



// const camera = new THREE.PerspectiveCamera( 45,2,1,1000 );
// 75, window.innerWidth / window.innerHeight, 0.1, 1000
camera.position.z = 2;



const canvas = document.querySelector('#c');
const renderer = new THREE.WebGLRenderer({antialias: true, canvas});
// const renderer = new THREE.WebGLRenderer();
// renderer.setSize( window.innerWidth, window.innerHeight );
// document.body.appendChild( renderer.domElement );

// const geometry = new THREE.BoxGeometry( 1, 1, 1 );
// const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
// const cube = new THREE.Mesh( geometry, material );
// scene.add( cube );

const loader = new GLTFLoader();

loader.load( '/untitled.glb', function ( gltf ) {

    console.log('ok')
	scene.add( gltf.scene );

}, undefined, function ( error ) {
    console.log('error')
	console.error( error );

} );

console.log('here11')

function animate() {
    requestAnimationFrame( animate );

    // cube.rotation.x += 0.01;
    // cube.rotation.y += 0.01;

    renderer.render( scene, camera );
}

animate();

})


</script>