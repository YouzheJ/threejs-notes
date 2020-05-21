### 9. 着色器

使用着色器可以更灵活地控制渲染效果，结合纹理，可以进行多次渲染，达到更强大的效果

#### 渲染

将模型数据在屏幕上显示出来的过程

#### 着色器

着色器是屏幕上呈现画面之前的最后一步，用它可以对先前渲染的结果做修改，包括对颜色、位置等等信息的修改，甚至可以对先前渲染的结果做后处理，实现高级的渲染效果。

着色器通常分为几何着色器（Geometry Shader）、顶点着色器（Vertex Shader）、片元着色器（Fragment Shader）等

由于WebGL基于OpenGL ES 2.0，因此WebGL支持的着色器只有顶点着色器与片元着色器。

- 顶点着色器

顶点着色器中的“顶点”指的正是Mesh中的顶点，对于每个顶点调用一次。因此，如果场景中有一个正方体，那么对八个顶点将各自调用一次顶点着色器，可以修改顶点的位置或者颜色等信息，然后传入片元着色器。

- 片元着色器

片元是栅格化之后，在形成像素之前的数据。片元着色器是每个片元会调用一次的程序，因此，片元着色器特别适合用来做图像后处理。

#### 着色器说明

1. 调试着色器：

- chrome插件: WebGL Insight
- js插件：Grimoire.js

> !! 最常发生错误的原因就是忘记float类型和int类型不会自动转换的，因此，当你想表达浮点数零的时候，一定要写成0.0而非0

语法：...

2. 着色器文件

着色器代码可以写在单独的文件中（顶点着色器的文件名后缀为.vs，片元着色器的文件名后缀为.fs），也可以在HTML文件中定义script标签实现

- 单独文件

```js
// load shader
$.get('shader/my.vs', function(vShader){
    $.get('shader/my.fs', function(fShader){
        material = new THREE.ShaderMaterial({
            vertexShader: vShader,
            fragementShader: fShader
        });
    });
});
```

- HTML中

```html
<!-- 定义顶点着色器；使用 -->
<script id="vs" type="x-shader/x-vertex">
    // 这里的内容相当于.vs文件中的内容
</script>

<!-- 定义片元着色器。 -->
<script id="fs" type="x-shader/x-fragment">
   // 这里的内容相当于.fs文件中的内容
</script>

<script>
    material = new THREE.ShaderMaterial({
        vertexShader: document.getElementById('vs').textContent,
        fragmentShader: document.getElementById('fs').textContent
    });
</script>
```
