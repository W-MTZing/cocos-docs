# 术语

本章旨在搜集和整理 Cocos Creator 以及和开发相关的一些术语和缩写，并提供解释。

## 联系我们

我们会持续更新此文档，如果您发现有未经解释的术语或描述不清的情况请点击屏幕右侧的提交反馈或 [获取帮助和支持](../getting-started/support.md)。

## 编辑器

| 术语 | 描述 |
| :--- | :--- |
| Editor | 通常指的是 Cocos Creator 的编辑器界面|
| Gizmo | 场景编辑器内的一些控制器，比如用于调整节点的位置、旋转、缩放或者光照等等。|

## 图形

| 术语 | 描述 |
| :--- | :--- |
| VB, Vertex Buffer | 顶点缓存，通常是指的一个模型内，顶点的合集，常用数组描述上，数组内的每个元素为一个复合结构，包括位置（Position）、纹理坐标（Tex-coord)、顶点颜色（Color）或者法线（Normal）等属性 |
| IB, Index Buffer | 索引缓存，内部存储的是上述 VB 中的顶点的索引，通过这些索引组合出特定的几何形状， 示例： 如 VB 为 { (0, 0, 0), (1, 0, 0), (1, 1, 0) }，IB 为 [0, 2, 1]， 那么此时绘制出的三角形顶点和顺便如下： { VB[0], VB[2]，VB[1] } |
| FPS | 帧率，指的是每秒中可以渲染的次数 |
| 层级，Layer | 指的是在渲染时，节点的分组情况，和 [相机的 Visibility 属性](../editor/components/camera-component.md) 配合可以处理某些节点是否被该相机渲染 |
| 多层次细节，LOD | Level of details, 通过不同层级拥有不同细节的模型，来提升渲染效率 |

### 光照

| 术语 | 描述 |
| :--- | :--- |
| GI, Global Illumination | 全局光照或者局部光照，指的是在计算机图形学中用于计算和模拟真实光源的一组算法 |
| LDR | 低动态范围光，通常指单个颜色的色域在 [0,255]（整数） 之间 或者 [0,1.0]（浮点数） 之间的颜色范围，也就是大多数显示设备可显示的颜色空间 |
| HDR | 高动态范围光，指的是颜色色域超出上条所述的颜色空间的颜色，显示中的颜色很可能会超出这个颜色范围，所以在显示设备显示时，需要使用 **色调映射** 将其转化到显示器可识别的区域 |

## 2D/UI

| 术语 | 描述 |
| :--- | :--- |
| 2D Object | 通过在 **层级管理器** 右键选单内创建的 2D 对象 |
| UI Object | 通过在 **层级管理器** 右键选单内创建的 UI 对象，通常是封装了某些用于交互的 UI 元素 |
| Sprite Atlas | [图集](../asset/atlas.md)，通过将一些碎片合并成单张的大图用于提高渲染效率，引擎提供 [自动合图](../asset/auto-atlas.md) 功能 |

## 动画

| 术语 | 描述 |
| :--- | :--- |
| Spine | 一款 2D 动画制作软件，其输出的动画文件可以被 Cocos Creator 识别 |
| DragonBone | 一款 2D 动画制作软件，其输出的动画文件可以被 Cocos Creator 识别 |
| Animation  | 动画，引擎内置的动画，无蒙皮功能，支持不同节点可以通过编辑器内的动画功能制作，[更多](../animation/index.md)
| SkeletalAnimation | 骨骼动画，带有蒙皮功能的动画组件，[更多](../animation/skeletal-animation.md) |
| Marionette | 支持用户自定义状态图的动画系统，和 SkeletalAnimation 配合可以实现丰富的功能，[更多](../animation/marionette/index.md) |

## 物理

| 术语 | 描述 |
| :--- | :--- |
| 力 | 使物体可以线性移动的力 |
| 扭矩 | 转矩，使物体旋转的力 |

### 2D 物理

| 术语 | 描述 |
| :--- | :--- |
| 物理后端 | 引擎封装的物理引擎的类型，Cocos Creator 提供两种物理后端分别是 **内置** 和 **Box2D** |
| Box2D | Box2D 是有名且高效的 2D 物理引擎 |
| 刚体 | 定义了可受力、速度影响的具有质量的物体，通常有三种类型：运动学、动力学以及静态 |
| 关节 | Joint 2D 物理关节，用于描述物体之间的物理连接情况 |
| 物理材质 | 用于调整两个物理碰撞体碰撞时的摩擦力、弹力处理情况 |

### 3D 物理

| 术语 | 描述 |
| :--- | :--- |
| 物理后端 | 引擎封装的物理引擎的类型，Cocos Creator 提供多种物理引擎包括： **内置**、**Bullet**、**PhysX** 和 **cannon.js** 等，可以在项目设置中修改以适配不同的平台和情况，**注意**：引擎抹平了大部分物理引擎的差异，但某些物理特定仅在特定的物理后端支持。|
| 刚体 | 定义了可受力、速度影响的具有质量的物体，通常有三种类型：运动学、动力学以及静态 |
| 约束 | 物理约束，用于描述物体之间的物理连接情况 |
| 物理材质 | 用于调整两个物理碰撞体碰撞时的摩擦力、弹力处理情况 |
| 力 | 使物体可以线性移动的力 |
| 扭矩 | 转矩，使物体旋转的力 |

## 资源系统

| 术语 | 描述 |
| :--- | :--- |
| Bundle， Asset Bundle | 一种处理资源的方式，引擎会将一个或者多个资源通过算法整合到单个文件内（通常是某种压缩文件）用于提升存储和下载的效率 |
| Resources | 特殊目录，引擎会将该目录打包为特殊的 Bundle，通过 `Resources.load` 等方法加载|
| Cocos Store | Cocos 的资源商店，开发者可以在上面出售和购买资产、源码或完整的商业游戏 |

## 脚本与编程

| 术语 | 描述 |
| :--- | :--- |
| 组件 | 继承自 `cc.Component` 的脚本，可以挂在在节点上 |
| 事件 | Cocos Creator 基于 [Web 的事件冒泡及捕获标准](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events#%E4%BA%8B%E4%BB%B6%E5%86%92%E6%B3%A1%E5%8F%8A%E6%8D%95%E8%8E%B7) 实现的事件系统，用于响应硬件输入或者节点间的通信，[更多](../engine/event/index.md)

## 原生开发

| 术语 | 描述 |
| :--- | :--- |
| 原生| 指的是 Cocos Creator 提供的，得以不依赖浏览器，在各桌面原生平台或移动原生平台运行的能力 |
| CMake | 一种组织 C ++ 代码的文件格式或者工具 |

## 其他功能

| 术语 | 描述 |
| :--- | :--- |
| XR | Extended Reality。适配 OpenXR 的 Cocos Creator 扩展程序，可以协助您制作增加现实功能，[更多](../xr/index.md) |
| AR | Augmented reality，增强现实。将虚拟世界和现实联系起来的技术，您可以使用 Cocos Creator 实现自己的 AR 应用。[更多](../xr/index.md) |