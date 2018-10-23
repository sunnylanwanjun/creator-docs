# 3D Node

> 文： youyou

## Node Api 升级

由于 CocosCreator 在 2.1 支持了 3D 的特性，所以相应节点的 api 也需要由 2D 升级到支持 3D 的使用。

影响比较大的改动是 rotation 的类型会从 `Number` 改为 `cc.Quat`，如果想像之前一样在 2D 空间方便旋转节点，那么可以使用 `angle` 属性。相应的 `setRotation` 和 `getRotation` 也会改为对 `cc.Quat` 的使用。

具体的升级请参考下表：

API | 2.0.3 | 2.1 - 2.4 | 2.5
------------ | ------------- | --------- | --------
rotationX, rotationY | KEEP | DEPRECATE，<br>USE `eulerAngles` | DEPRECATE
rotation | KEEP，number | DEPRECATE，<br>USE `angle` | GET `cc.Quat`
angle | ADD，= `-rotation` | `-rotation` | `-rotation`
scale | KEEP，number | KEEP，number | KEEP，number
getRotation() | KEEP，number | DEPRECATE，<br>USE `angle` | GET `cc.Quat` 
getRotation(cc.Quat) | GET `cc.Quat` |  | 
setRotation | KEEP | DEPRECATE SET `Number`，<br>USE `angle` | SET `cc.Quat`
setRotation | SET `cc.Quat` | |
getScale() | KEEP，number | DEPRECATE，<br>USE `scale` | GET `cc.Vec2` / `cc.Vec3`
getScale(cc.Vec2/cc.Vec3) | GET `cc.Vec2` / `cc.Vec3` |  | 
setScale | KEEP | KEEP | KEEP
position | cc.Vec2 | cc.Vec3 | cc.Vec3

## 开启 3D 节点

在 Cocos Creator 2.1 加入了 3D 支持后，节点会分为 2D 节点和 3D 节点，他们的区别在于 2D 节点在做矩阵计算或者一些属性设置的时候只会在 2D 空间下进行考虑，这样能节省很大一部分运行开销。

默认新创建出来的节点都是 2D 节点，有两种方式设置这个节点为 3D 节点：

- 点击在编辑器属性检查器右上角的 **2.5D** 按钮进行切换

![3d-node-inspector](img/3d-node-inspector.png)

可以看到，当节点切换为 3D 节点后，旋转、位移、缩放都变成了可以设置 3 个值，我们在属性编辑器中可以方便的编辑节点的 3D 属性了。

- 在代码中切换

```js
node.is3DNode = true;
```