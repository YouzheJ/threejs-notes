### 7. 外部模型

Three.js有一系列导入外部文件的辅助函数，是在three.js之外的，使用前需要额外下载，在https://github.com/mrdoob/three.js/tree/master/examples/js/loaders可以找到

*.obj是最常用的模型格式，导入*.obj文件需要OBJLoader.js

目前，支持的模型格式有：

```
*.obj
*.obj, *.mtl
*.dae
*.ctm
*.ply
*.stl
*.wrl
*.vtk
```

#### 无材质的模型

导入示例：

```js
// <script type="text/javascript" src="OBJLoader.js"></script>

var loader = new THREE.OBJLoader();
loader.load('../lib/port.obj', function(obj) {
    // 由于默认的情况下，只有正面的面片被绘制，而如果需要双面绘制
    obj.traverse(function(child) {
        if (child instanceof THREE.Mesh) {
            child.material.side = THREE.DoubleSide;
        }
    });

    mesh = obj;
    scene.add(obj);
});
```

#### 有材质的模型

1. 代码中设置材质

```js
var loader = new THREE.OBJLoader();
loader.load('../lib/port.obj', function(obj) {
    obj.traverse(function(child) {
        if (child instanceof THREE.Mesh) {
            // 设置材质
            child.material = new THREE.MeshLambertMaterial({
                color: 0xffff00,
                side: THREE.DoubleSide
            });
        }
    });

    mesh = obj;
    scene.add(obj);
});
```

2. 建模软件中设置材质

> 导出模型时，选择Export materials，最终导出port.obj模型文件以及port.mtl材质文件

```js
// <script type="text/javascript" src="MTLLoader.js"></script>
// <script type="text/javascript" src="OBJMTLLoader.js"></script>

var loader = new THREE.OBJMTLLoader();
loader.addEventListener('load', function(event) {
    var obj = event.content;
    mesh = obj;
    scene.add(obj);
});
loader.load('../lib/port.obj', '../lib/port.mtl');
```
