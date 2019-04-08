# 下载场景包

您只需下载预编译好的场景文件，直接运行即可。 如果您想搭建自己的虚幻环境，请参阅 [该链接子目录"如何获得它"](https://frendowu.github.io/AirSim-docs-zh/)。

### 虚幻引擎

**Windows**: 从 [latest release](https://github.com/Microsoft/AirSim/releases) 中下载您需要的场景。

**Linux**: 尚未提供相关功能，但是您可以自行 [在linux上搭建](build_linux.md)。

### Unity引擎（试验性）

在[Unity Asset Store](https://assetstore.unity.com/) 中一个叫做""的免费环境可以运行试验性的AirSim，因为尚未开发完成，故目前可能会存在些许问题。

## 控制车辆

大多数的使用者广泛使用 [APIs](apis.md) 来控制车辆。但是您也可以手动控制车辆，您可以用键盘、手柄或者[方向盘](steering_wheel_installation.md)来操控。如果您希望手动控制无人机，您需要使用XBox手柄或者一个遥控器（您也可以帮忙[完善](CONTRIBUTING.md)键盘控制模块）。更多细节请参阅[配置遥控器](remote_control.md)。同样的，您可以使用[APIs](apis.md)来实现程序控制，或者使用键盘搭配[计算机视觉模块](image_apis.md)在虚拟环境中漫游。

## 没有一块强力的GPU？

想要运行AirSim的场景文件如CityEnviron，您需要一块配置较高的GPU来流畅运行。您可以在通过修改Windows系统下的`run.bat`来实现低分辨率运行：

```
start CityEnviron -ResX=640 -ResY=480 -windowed
```

