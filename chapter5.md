### 5. 网格

最常用的一种物体就是网格（Mesh），网格是由顶点、边、面等组成的物体；其他物体包括线段（Line）、骨骼（Bone）、粒子系统（ParticleSystem）等

网格的创建非常简单，只要把几何形状与材质传入其构造函数。最常用的物体是网格（Mesh），它代表包含点、线、面的几何体

```js
Mesh(geometry, material)
```

#### 修改属性

- 除了在构造函数中指定材质，在网格被创建后，也能对材质进行修改

- 位置、缩放、旋转

位置、缩放、旋转是物体三个常用属性。由于THREE.Mesh基础自THREE.Object3D，因此包含scale、rotation、position三个属性。它们都是THREE.Vector3实例，因此修改其值的方法是相同的

```js
mesh.position.z = 1;

mesh.position.set(1.5, -0.5, 0);

mesh.position = new THREE.Vector3(1.5, -0.5, 0);
```
