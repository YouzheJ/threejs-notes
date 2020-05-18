### 4. 材质

材质（Material）是独立于物体顶点信息之外的与渲染效果相关的属性。通过设置材质可以改变物体的颜色、纹理贴图、光照模式等

#### 基本材质

使用基本材质（BasicMaterial）的物体，渲染后物体的颜色始终为该材质的颜色，而不会由于光照产生明暗、阴影效果。如果没有指定材质的颜色，则颜色是随机的

THREE.MeshBasicMaterial(opt)

opt可以缺省，或者为包含各属性的值

常用的属性:

```
visible：是否可见，默认为true
side：渲染面片正面或是反面，默认为正面THREE.FrontSide，可设置为反面THREE.BackSide，或双面THREE.DoubleSide
wireframe：是否渲染线而非面，默认为false
color：十六进制RGB颜色，如红色表示为0xff0000
map：使用纹理贴图
```

#### Lambert材质

Lambert材质（MeshLambertMaterial）是符合Lambert光照模型的材质。Lambert光照模型的主要特点是只考虑漫反射而不考虑镜面反射的效果，因而对于金属、镜子等需要镜面反射效果的物体就不适应，对于其他大部分物体的漫反射效果都是适用的。

其光照模型公式为：

```
Idiffuse = Kd * Id * cos(theta)
```

> Idiffuse是漫反射光强，Kd是物体表面的漫反射属性，Id是光强，theta是光的入射角弧度。

构造函数：

```
THREE.MeshLambertMaterial(opt)
```

color是用来表现材质对散射光的反射能力，也是最常用来设置材质颜色的属性。除此之外，还可以用ambient和emissive控制材质的颜色

ambient表示对环境光的反射能力，只有当设置了AmbientLight后，该值才是有效的，材质对环境光的反射能力与环境光强相乘后得到材质实际表现的颜色

emissive是材质的自发光颜色，可以用来表现光源的颜色

#### Phong材质

Phong材质（MeshPhongMaterial）是符合Phong光照模型的材质。和Lambert不同的是，Phong模型考虑了镜面反射的效果，因此对于金属、镜面的表现尤为适合。

漫反射部分和Lambert光照模型是相同的，镜面反射部分的模型为：

```
Ispecular = Ks * Is * (cos(alpha)) ^ n
```

Ispecular是镜面反射的光强，Ks是材质表面镜面反射系数，Is是光源强度，alpha是反射光与视线的夹角，n是高光指数，越大则高光光斑越小

构造函数：

```
new THREE.MeshPhongMaterial(opt)
```

由于漫反射部分与Lambert模型是一致的，因此，如果不指定镜面反射系数，而只设定漫反射，其效果与Lambert是相同的

specular值指定镜面反射系数

可以通过shininess属性控制光照模型中的n值，当shininess值越大时，高光的光斑越小，默认值为30

#### 法向材质

法向材质可以将材质的颜色设置为其法向量的方向，有时候对于调试很有帮助。

法向材质的设定很简单，甚至不用设置任何参数：

```
new THREE.MeshNormalMaterial()
```

材质的颜色与照相机与该物体的角度相关

#### 材质的纹理贴图

在此之前，我们使用的材质都是单一颜色的，有时候，我们却希望使用图像作为材质。这时候，就需要导入图像作为纹理贴图，并添加到相应的材质中

```js
// 将图像导入纹理中
var texture = THREE.ImageUtils.loadTexture('../img/0.png', {}, function () {
    // 没有重绘函数，所以在加载后调用重绘
    renderer.render(scene, camera);
});

// 将材质的map属性设置为texture：
var material = new THREE.MeshLambertMaterial({
    map: texture
});
```


