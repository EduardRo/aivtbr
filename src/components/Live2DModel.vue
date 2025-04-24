<template>
    <div>
        <canvas id="live2d-canvas" width="800" height="800"></canvas>
    </div>
</template>

<script setup>
import * as PIXI from 'pixi.js'
import { Live2DModel } from 'pixi-live2d-display'  // wrapper for Cubism SDK

const loadModel = async () => {
    const app = new PIXI.Application({
        view: document.getElementById('live2d-canvas'),
        autoStart: true,
        transparent: true,
        resizeTo: window
    })

    const model = await Live2DModel.from('/models/snow_leopard/Snow Leopard.model3.json')

    model.scale.set(0.2)
    model.x = window.innerWidth / 2
    model.y = window.innerHeight / 1.5

    app.stage.addChild(model)

    // Basic animation loop (if you add motion3.json later)
    model.motion('Idle')?.startRandomMotion()
}

onMounted(() => {
    loadModel()
})
</script>

<style scoped>
canvas {
    position: absolute;
    top: 0;
    left: 0;
}
</style>