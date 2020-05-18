### 3. 几何形状

---

1. **基本几何体**

#### 立方体

立方体（CubeGeometry），但它其实是长方体，也就是长宽高可以设置为不同的值。其构造函数是：

```js
THREE.CubeGeometry(width, height, depth, widthSegments, heightSegments, depthSegments)
```

width是x方向上的长度；height是y方向上的长度；depth是z方向上的长度；后三个参数分别是在三个方向上的分段数，缺省值为1

#### 平面

这里的平面（PlaneGeometry）其实是一个长方形，而不是数学意义上无限大小的平面。其构造函数为：

```js
THREE.PlaneGeometry(width, height, widthSegments, heightSegments)
```

width是x方向上的长度；height是y方向上的长度；后两个参数同样表示分段

#### 球体

球体（SphereGeometry）的构造函数是：

```js
THREE.SphereGeometry(radius, segmentsWidth, segmentsHeight, phiStart, phiLength, thetaStart, thetaLength)
```

radius是半径；segmentsWidth表示经度上的切片数；segmentsHeight表示纬度上的切片数；phiStart表示经度开始的弧度；phiLength表示经度跨过的弧度；thetaStart表示纬度开始的弧度；thetaLength表示纬度跨过的弧度

#### 圆形

圆形（CircleGeometry）可以创建圆形或者扇形，其构造函数是：

```js
THREE.CircleGeometry(radius, segments, thetaStart, thetaLength)
```

#### 圆柱体

圆柱体（CylinderGeometry）的构造函数是：

```js
THREE.CylinderGeometry(radiusTop, radiusBottom, height, radiusSegments, heightSegments, openEnded)
```

openEnded是一个布尔值，表示是否没有顶面和底面，缺省值为false，表示有顶面和底面

#### 正四面体、正八面体、正二十面体

正四面体（TetrahedronGeometry）、正八面体（OctahedronGeometry）、正二十面体（IcosahedronGeometry）的构造函数较为类似，分别为：

```js
THREE.TetrahedronGeometry(radius, detail)
THREE.OctahedronGeometry(radius, detail)
THREE.IcosahedronGeometry(radius, detail)
```

radius是半径；detail是细节层次（Level of Detail）的层数，对于大面片数模型，可以控制在视角靠近物体时，显示面片数多的精细模型，而在离物体较远时，显示面片数较少的粗略模型。这里我们不对detail多作展开，一般可以对这个值缺省。

#### 圆环面


圆环面（TorusGeometry）就是甜甜圈的形状，其构造函数是：

```js
THREE.TorusGeometry(radius, tube, radialSegments, tubularSegments, arc)
```

radius是圆环半径；tube是管道半径；radialSegments与tubularSegments分别是两个分段数，详见上图；arc是圆环面的弧度，缺省值为Math.PI * 2

#### 圆环结

如果说圆环面是甜甜圈，那么圆环结（TorusKnotGeometry）就是打了结的甜甜圈，其构造参数为：

```js
THREE.TorusKnotGeometry(radius, tube, radialSegments, tubularSegments, p, q, heightScale)
```

p和q是控制其样式的参数，一般可以缺省

---

2. **文字形状**

使用文字形状需要下载和引用额外的字体库 [github](https://github.com/mrdoob/three.js/tree/master/examples/fonts)

```js
// 加载字体
var loader = new THREE.FontLoader();
loader.load('../lib/helvetiker_regular.typeface.json', function(font) {
    var mesh = new THREE.Mesh(new THREE.TextGeometry('Hello', {
        font: font,
        size: 1,
        height: 1
    }), material);
    scene.add(mesh);

    // render
    renderer.render(scene, camera);
});
```

构造函数：

```js
THREE.TextGeometry(text, parameters)
```

text是文字字符串，parameters是以下参数组成的对象：

```
size：字号大小，一般为大写字母的高度
height：文字的厚度
curveSegments：弧线分段数，使得文字的曲线更加光滑
font：字体，默认是'helvetiker'，需对应引用的字体文件
weight：值为'normal'或'bold'，表示是否加粗
style：值为'normal'或'italics'，表示是否斜体
bevelEnabled：布尔值，是否使用倒角，意为在边缘处斜切
bevelThickness：倒角厚度
bevelSize：倒角宽度
```

---

3. **自定义形状**

对于Three.js没有提供的形状，可以提供自定义形状来创建。

由于自定义形状需要手动指定每个顶点位置，以及顶点连接情况，如果该形状非常复杂，程序员的计算量就会比较大。在这种情况下，建议在3ds Max之类的建模软件中创建模型，然后使用Three.js导入到场景中，这样会更高效方便。

自定义形状使用的是Geometry类，它是其他如CubeGeometry、SphereGeometry等几何形状的父类，其构造函数是：

```js
THREE.Geometry()
```

- 梯台：

```js
// 初始化几何形状
var geometry = new THREE.Geometry();

// 设置顶点位置
// 顶部4顶点
geometry.vertices.push(new THREE.Vector3(-1, 2, -1));
geometry.vertices.push(new THREE.Vector3(1, 2, -1));
geometry.vertices.push(new THREE.Vector3(1, 2, 1));
geometry.vertices.push(new THREE.Vector3(-1, 2, 1));
// 底部4顶点
geometry.vertices.push(new THREE.Vector3(-2, 0, -2));
geometry.vertices.push(new THREE.Vector3(2, 0, -2));
geometry.vertices.push(new THREE.Vector3(2, 0, 2));
geometry.vertices.push(new THREE.Vector3(-2, 0, 2));

// 设置顶点连接情况
// 顶面
geometry.faces.push(new THREE.Face3(0, 1, 3));
geometry.faces.push(new THREE.Face3(1, 2, 3));
// 底面
geometry.faces.push(new THREE.Face3(4, 5, 6));
geometry.faces.push(new THREE.Face3(5, 6, 7));
// 四个侧面
geometry.faces.push(new THREE.Face3(1, 5, 6));
geometry.faces.push(new THREE.Face3(6, 2, 1));
geometry.faces.push(new THREE.Face3(2, 6, 7));
geometry.faces.push(new THREE.Face3(7, 3, 2));
geometry.faces.push(new THREE.Face3(3, 7, 0));
geometry.faces.push(new THREE.Face3(7, 4, 0));
geometry.faces.push(new THREE.Face3(0, 4, 5));
geometry.faces.push(new THREE.Face3(0, 5, 1));
```

需要注意的是，new THREE.Vector3(-1, 2, -1)创建一个矢量，作为顶点位置追加到geometry.vertices数组中。

而由new THREE.Face3(0, 1, 3)创建一个三个顶点组成的面片，追加到geometry.faces数组中。三个参数分别是四个顶点在geometry.vertices中的序号。

