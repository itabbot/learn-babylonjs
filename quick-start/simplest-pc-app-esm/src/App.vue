<template></template>

<script setup>
import { Engine } from "@babylonjs/core/Engines/engine";
import { Scene } from "@babylonjs/core/scene";
import { FreeCamera } from "@babylonjs/core/Cameras/freeCamera";
import { Vector3 } from "@babylonjs/core/Maths/math.vector";
import { HemisphericLight } from "@babylonjs/core/Lights/hemisphericLight";
import { GridMaterial } from "@babylonjs/materials/grid/gridMaterial";
import { CreateSphere } from "@babylonjs/core/Meshes/Builders/sphereBuilder";
import { CreateGround } from "@babylonjs/core/Meshes/Builders/groundBuilder";

// 获取画布元素
const canvas = document.getElementById('render_canvas');

// 创建 BABYLON 引擎实例
// 并指定渲染的画布
const engine = new Engine(canvas, true);

// 创建一个基本的场景实例
// 并指定渲染此场景的引擎
const scene = new Scene(engine);

// 创建一个自由相机实例
// 并在场景中定位相机的起始位置
const camera = new FreeCamera('camera1', new Vector3(0, 5, -10), scene);
// 设置相机对准的目标位置：场景原点
camera.setTarget(Vector3.Zero());
// 将相机附加到画布上
camera.attachControl(canvas, true);

// 创建一个半球光源实例（不能投射阴影）
// 并指定光的反射方向
const light = new HemisphericLight('light', new Vector3(0, 1, 0), scene);
// 灯光默认强度为 1，这里把灯光调暗一点
light.intensity = 0.7;

// 创建一个网格材质实例
var material = new GridMaterial("grid", scene);

// 在场景中添加一个内置的 “球体” 形状
const sphere = CreateSphere('sphere', { diameter: 2 }, scene);
// 将球体向上移动一个单位高度
sphere.position.y = 1;
// 设置球体材质
sphere.material = material;

// 在场景中添加一个内置的 “地面” 形状
const ground = CreateGround('ground', { width: 6, height: 6, subdivisions: 2 }, scene);
// 设置地面材质
ground.material = material;

// 注册一个渲染循环来重复渲染场景
engine.runRenderLoop(() => {
  scene.render();
});

// 监听浏览器大小调整事件
window.addEventListener('resize', function () {
  engine.resize();
});
</script>