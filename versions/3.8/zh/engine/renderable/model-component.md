# MeshRenderer 组件参考

MeshRenderer（网格渲染器）组件用于显示一个静态的 3D 模型。通过 **Mesh** 属性设置模型网格，通过 **Materials** 属性控制模型的显示外观。

在 **属性检查器** 中点击 **添加组件 -> Mesh -> MeshRenderer** 即可添加 MeshRenderer 组件。

![Mesh Renderer properties](meshrenderer-properties.png)

## MeshRenderer 属性

| 属性 | 功能 |
| :--- | :--- |
| **Materials** | 网格资源允许使用多个材质资源，所有材质资源都存在 `materials` 数组中。<br>如果网格资源中有多个子网格，那么 Mesh Renderer 会从 `materials` 数组中获取对应的材质来渲染此子网格。 |
| **Dynamic Shadow Settings** | 动态阴影配置，详情请参考下方 **动态阴影配置** 文档 |
| **Bake Settings** | 烘焙配置，详情请参考下方 **烘焙配置** 文档 |
| **Mesh** | 指定渲染所用的网格资源，详情请参考下文 **网格资源** 部分的内容 |

### 动态阴影配置

| 属性 | 说明 |
| :-- | :-- |
| **Shadow Bias** | 阴影偏移
| **Shadow Normal Bias** | 阴影法线偏移
| **Shadow Casting Mode** |  指定当前模型是否会投射阴影，需要先在场景中 [开启阴影](../../concepts/scene/light/shadow.md#%E5%BC%80%E5%90%AF%E9%98%B4%E5%BD%B1)。|
| **Receive Shadow** | 指定当前模型是否会接收并显示其它物体产生的阴影效果，需要先在场景中 [开启阴影](../../concepts/scene/light/shadow.md#%E5%BC%80%E5%90%AF%E9%98%B4%E5%BD%B1)。该属性仅在阴影类型为 **ShadowMap** 时生效。|

### 烘焙配置

烘焙设置指的是网格如何使用或写入离线光照信息。

该配置包含：[光照贴图](../../concepts/scene/light/lightmap.md)、[光照探针](probe/light-probe.md) 和 [反射探针](../../concepts/scene/light/probe/reflection-probe.md)。

#### 光照贴图

| 属性 | 说明 |
| :-- | :-- |
| **Bakeable** | 是否会被烘焙到光照贴图内 |
| **Cast Shadow** | 是否投射阴影 |
| **Receive Shadow** | 是否接收阴影 |
| **Lightmap Size** | 光照贴图的大小 |

#### 光照探针

| 属性 | 说明 |
| :-- | :-- |
| **Use Light Probe** | 配置是否使用光照探针 |
| **Bake To Light Probe** | 配置是否烘焙光照探针 |

#### 反射探针

| 属性 | 说明 |
| :-- | :-- |
| **Reflection Probe** | [反射探针](../../concepts/scene/light/probe/reflection-probe.md) 的类型 <br> 支持 **PLANNAR_REFLECTION** 、 **CUBE_REFLECTION**、**BLEND_PROBES**、**BLEND_PROBES_AND_SKYBOX** <br> **PLANNAR_REFLECTION**：配置为动态反射探针 <br> **CUBE_REFLECTION**：配置为使用烘焙后的反射探针 <br> **BLEND_PROBES**：配置为使用烘焙后的反射探针并且反射探针之间会进行混合。 <br> **BLEND_PROBES_AND_SKYBOX**：配置为使用烘焙后的反射探针并且在BLEND_PROBES项的基础上增加了和天空盒混合的功能 |
| **Bake To Reflection Probe** | 配置是否烘焙至反射探针生成的贴图内 |

网格渲染器组件相关接口请参考 [MeshRenderer API](%__APIDOC__%/zh/class/MeshRenderer)。

蒙皮网格渲染器组件相关接口请参考 [SkinnedMeshRenderer API](%__APIDOC__%/zh/class/SkinnedMeshRenderer)

### 网格资源

Mesh 资源是渲染网格的必要资源，目前网格主要是在 [导入模型资源](../../asset/model/mesh.md#%E6%A8%A1%E5%9E%8B%E5%AF%BC%E5%85%A5) 到 Creator 中时，由 Creator 自动生成的。

Mesh 资源中包含了一组顶点和多组索引。索引指向顶点数组中的顶点，每三组索引组成一个三角形。网格则是由多个三角形组成的，是 3D 世界中最基本的图元。多个三角形拼接成一个复杂的多边形，多个多边形则拼接成一个 3D 模型。

Creator 提供了几个简单的静态 3D 模型，其中包含了立方体、圆柱体等基础模型，开发者可根据自己的需要在 **层级管理器** 中创建几个，以初步了解。

![create model](create-model.png)

## 模型分组渲染

分组渲染功能是通过相机组件的 [Visibility 属性](../../editor/components/camera-component.md#%E8%AE%BE%E7%BD%AE-visibility-%E5%B1%9E%E6%80%A7) 配合节点的 [Layer 属性](../../concepts/scene/node-component.md#%E8%AE%BE%E7%BD%AE%E8%8A%82%E7%82%B9%E7%9A%84-layer-%E5%B1%9E%E6%80%A7) 共同决定。用户可通过代码设置 `Visibility` 的值来完成分组渲染。所有节点默认都属于 **DEFAULT** 层，在所有相机都可见。

## 静态合批

目前静态合批方案为运行时静态合批，通过调用 `BatchingUtility.batchStaticModel` 可进行静态合批。<br>
该函数接收一个节点，然后将该节点下的所有 `MeshRenderer` 里的 `Mesh` 合并成一个，并将其挂到另一个节点下。<br>
在合批后，将无法改变原有的 `MeshRenderer` 的 `transform`，但可以改变合批后的根节点的 `transform`。

只有满足以下条件的节点才能进行静态合批：
- 子节点中只能包含 `MeshRenderer`；
- 子节点下的 `MeshRenderer` 的 `Mesh` 的顶点数据结构必须一致；
- 子节点下的 `MeshRenderer` 的材质必须相同。

## 动态合批

引擎目前提供 instancing 动态合批功能。<br>
要开启合批，只需在模型所使用的材质中对应勾选 `USE_INSTANCING` 开关即可。

> **注意**：目前的合批流程会引入一些限制：
>
> 1. 同一批次的透明模型间的绘制顺序无法保证，可能导致混合效果不准确；
> 2. 合批后没有传递逆转置世界矩阵信息，带有非均一缩放的模型的法线会不准确；
> 3. 只支持普通 3D 模型和预烘焙骨骼动画控制下的蒙皮模型（实时计算骨骼动画、2D 物体、UI、粒子等均不支持动态合批）。

### Instancing 合批

通过 Instancing 的合批适用于绘制大量顶点数据完全相同的动态模型，启用后绘制时会根据材质和顶点数据分组，每组内组织 instanced attributes 信息，然后一次性完成绘制。

关于蒙皮模型的支持及相关设定，参考 [骨骼动画组件](../../animation/skeletal-animation.md#关于动态-Instancing)。

另外 instancing 还支持自定义额外的 instanced attributes，可以传递更多不同 instance 之间的差异性数据（比如不同人物间给一个漫反射颜色的外观差异，或大片草地中的风力影响）。<br>
这需要自定义 effect 的支持，更详细的说明可以参考 [语法指南](../../shader/effect-syntax.md#%E8%87%AA%E5%AE%9A%E4%B9%89%E5%87%A0%E4%BD%95%E4%BD%93%E5%AE%9E%E4%BE%8B%E5%8C%96%E5%B1%9E%E6%80%A7)

### 合并 VB 合批

考虑到合并 VB 合批在每帧合并顶点等操作会引入一部分 CPU 开销，相当于是用CPU开销来替换 drawcall 的开销（大多数情况下前者反而要大于后者，在 JS 中尤其昂贵），未经严格测试的滥用反而会引起性能降低，**此功能在3.6.2已移除，请优先使用 Instancing 或静态合批来替代**。

另外需要提醒 <font color=#ff0000>drawcall 数量并非唯一的性能指标[^2]</font>，最佳性能往往是 CPU 与 GPU 负载均衡的结果，所以在尝试使用合批功能时，请一定多做测试，明确性能瓶颈，做有针对性的优化。

## 合批的最佳实践

通常来说合批系统的使用优先级为：**静态合批 > instancing 合批**。<br>
首先要确保材质统一，在这个前提下，如果确定某些模型在游戏周期内完全静止不会变化，就可以使用静态合批。<br>
如果存在大量相同的模型重复绘制，相互间只有相对可控的小差异，就可以使用 instancing 合批。<br>

## 预览网格

鼠标悬停在 **Mesh** 属性中下拉的网格上时，可以在场景视图中对模型进行预览。

![view model](mesh-renderer/view-model.gif)

[^1]: 注意目前使用 uniform 上传合批后的世界变换矩阵，考虑到 WebGL 标准的 uniform 数量限制，目前一批最多绘制 10 个模型，所以对大量同材质的模型，开启合批后 drawcall 数量预期最多会减少 10 倍。
[^2]: 关于合批与性能的话题业界一直有不少探讨，比如可以参考 [这里](https://www.nvidia.com/docs/IO/8228/BatchBatchBatch.pdf) 的 slide。
