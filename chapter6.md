### 6. 动画

动画的本质是利用了人眼的视觉暂留特性，快速地变换画面，从而产生物体在运动的假象

- 每秒帧数FPS（Frames Per Second）的概念，是指每秒画面重绘的次数

- setInterval方法
- requestAnimationFrame方法 (cancelAnimationFrame)

#### stats

```js
var stat = null;

function init() {
    stat = new Stats();
    stat.domElement.style.position = 'absolute';
    stat.domElement.style.right = '0px';
    stat.domElement.style.top = '0px';
    document.body.appendChild(stat.domElement);

    // Three.js init ...
}

function draw() {
    stat.begin();

    mesh.rotation.y = (mesh.rotation.y + 0.01) % (Math.PI * 2);
    renderer.render(scene, camera);

    stat.end();
}
```
