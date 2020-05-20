### 8. 光与影

#### 环境光

环境光是指场景整体的光照效果，是由于场景内若干光源的多次反射形成的亮度一致的效果，通常用来为整个场景指定一个基础亮度。因此，环境光没有明确的光源位置，在各处形成的亮度也是一致的。

```js
THREE.AmbientLight(hex)
```

hex是十六进制的RGB颜色信息，如红色表示为0xff0000

环境光并不在乎物体材质的color属性，而是ambient属性

当环境光不是白色或灰色的时候，渲染的效果往往会很奇怪。因此，环境光通常使用白色或者灰色，作为整体光照的基础。


#### 点光源

点光源是不计光源大小，可以看作一个点发出的光源。点光源照到不同物体表面的亮度是线性递减的，因此，离点光源距离越远的物体会显得越暗

```js
THREE.PointLight(hex, intensity, distance)
```

hex是光源十六进制的颜色值；intensity是亮度，缺省值为1，表示100%亮度；distance是光源最远照射到的距离，缺省值为0。


#### 平行光

平行光照射的亮度都是相同的，而与平面所在位置无关

```js
THREE.DirectionalLight(hex, intensity)
```

hex是光源十六进制的颜色值；intensity是亮度，缺省值为1，表示100%亮度。

此外，对于平行光而言，设置光源位置尤为重要

```js
var light = new THREE.DirectionalLight();
light.position.set(2, 5, 3);
scene.add(light);
```

#### 聚光灯

朝着一个方向投射光线。聚光灯投射出的是类似圆锥形的光线

```js
THREE.SpotLight(hex, intensity, distance, angle, exponent)
```

angle是聚光灯的张角，缺省值是Math.PI / 3，最大值是Math.PI / 2；exponent是光强在偏离target的衰减指数（target需要在之后定义，缺省值为(0, 0, 0)），缺省值是10

在调用构造函数之后，除了设置光源本身的位置，一般还需要设置target：

```js
light.position.set(x1, y1, z1);
light.target.position.set(x2, y2, z2);
```

除了设置light.target.position的方法外，如果想让聚光灯跟着某一物体移动（就像真的聚光灯！），可以target指定为该物体：

```js
var cube = new THREE.Mesh(new THREE.CubeGeometry(1, 1, 1),
                    new THREE.MeshLambertMaterial({color: 0x00ff00}));

var light = new THREE.SpotLight(0xffff00, 1, 100, Math.PI / 6, 25);
light.target = cube;
```

#### 阴影

能形成阴影的光源只有THREE.DirectionalLight与THREE.SpotLight；而相对地，能表现阴影效果的材质只有THREE.LambertMaterial与THREE.PhongMaterial

```js
// 开启渲染器渲染阴影
renderer.shadowMapEnabled = true;

// 对于光源以及所有要产生阴影的物体调用：
xxx.castShadow = true;

// 对于接收阴影的物体调用：
xxx.receiveShadow = true;

// 为了看到阴影照相机的位置，通常可以在调试时开启
light.shadowCameraVisible = true;
```
