<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<title>3D Car Chase</title>
<style>
  body { margin: 0; overflow: hidden; background: black; }
  #ui {
    position: absolute;
    top: 10px;
    left: 10px;
    color: white;
    font-family: Arial;
    font-size: 18px;
    z-index: 10;
  }
</style>
</head>
<body>

<div id="ui">
  Score: <span id="score">0</span><br>
  Car: <span id="carName">Basic</span>
</div>

<script src="https://cdn.jsdelivr.net/npm/three@0.152.2/build/three.min.js"></script>

<script>
/* ---------- SCENE ---------- */
const scene = new THREE.Scene();
scene.background = new THREE.Color(0x87ceeb);

const camera = new THREE.PerspectiveCamera(70, window.innerWidth/window.innerHeight, 0.1, 500);
camera.position.set(0, 6, 10);

const renderer = new THREE.WebGLRenderer({ antialias:true });
renderer.setSize(window.innerWidth, window.innerHeight);
document.body.appendChild(renderer.domElement);

const light = new THREE.DirectionalLight(0xffffff, 1);
light.position.set(5,10,5);
scene.add(light);

/* ---------- ROAD ---------- */
const road = new THREE.Mesh(
  new THREE.BoxGeometry(8,0.1,500),
  new THREE.MeshStandardMaterial({ color:0x333333 })
);
road.position.y = 0.05;
road.position.z = -200;
scene.add(road);

/* ---------- PLAYER CAR ---------- */
const carGeo = new THREE.BoxGeometry(1.5,1,3);
const carMat = new THREE.MeshStandardMaterial({ color:0xff0000 });
const playerCar = new THREE.Mesh(carGeo, carMat);
playerCar.position.y = 0.6;
scene.add(playerCar);

/* ---------- POLICE ---------- */
const police = new THREE.Mesh(
  carGeo,
  new THREE.MeshStandardMaterial({ color:0x0000ff })
);
police.position.set(0,0.6,-12);
scene.add(police);

/* ---------- CARS DATA ---------- */
const cars = [
  { name:"Basic", color:0xff0000, speed:0.18, cost:0 },
  { name:"Sport", color:0x00ff00, speed:0.25, cost:500 },
  { name:"Super", color:0xffff00, speed:0.32, cost:1
