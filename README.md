## threejs学习笔记

> threejs入门指南： https://www.ituring.com.cn/book/miniarticle/58552

- WebGL是基于OpenGL ES 2.0的Web标准，可以通过HTML5 Canvas元素作为DOM接口访问。

- Three.js是一个3D JavaScript库。

---

一个典型的Three.js程序至少要包括渲染器（Renderer）、场景（Scene）、照相机（Camera），以及你在场景中创建的物体。

WebGL和Three.js使用的坐标系是右手坐标系：如下示意：

```
   y
   ^
   |
   |
    —— ——> x
  /
 /
v
z
```
