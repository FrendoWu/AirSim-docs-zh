# 在Windows上构建AirSim

## 安装虚幻引擎

1. [点此下载](https://www.unrealengine.com/download) Epic Games登录器，尽管虚幻引擎是开源且免费的，但是目前步骤仍然是需要下载Epic并注册。

2. 运行Epic Games, 点击左侧的 `Library` 标签。   
  点击 `+`号，选择下 **Unreal 4.18** 。如果您安装了多个版本的虚幻引擎，请通过点击Launch旁边的下三角形确保**4.18版本是`目前（current）`正在使用的版本**。

   **注意**：如果您有基于UE4.16或者更老的版本的项目，请查阅 [升级指引](unreal_upgrade.md) 来升级您的项目。

## 构建AirSim的步骤

* 安装 Visual Studio 2017；
  **请确保**安装时勾选了**VC++**以及**Windows SDK 8.1**选项。
* 运行`x64 Native Tools Command Prompt for VS 2017`. 
* 克隆代码仓库：`git clone https://github.com/Microsoft/AirSim.git`，然后进入到AirSim所在目录`cd AirSim`. 
* 从命令行界面运行`build.cmd`。这会在目录 `Unreal\Plugins` 生成可以拖进任意虚幻引擎项目的即用插件文件。

## Build虚幻引擎项目

最终，您将会需要一个虚幻引擎项目并在其中试运行车辆/无人机。AirSim伊始便提供一个"Blcoks环境"，您可以自由构建您的项目，请参阅[设置虚幻环境](unreal_proj.md)。

## 配置遥控器控制功能（仅限无人机）

如果您想手动控制无人机，您需要一个遥控器。请查阅 [遥控器控制](remote_control.md) 获取更多细节。

当然，您也可以通过 [APIs](apis.md) 编写程序来进行操控，或者在 [计算机视觉模式](image_apis.md) 下使用键盘来预览环境。

## 如何使用AirSim

一旦您完成了上述步骤，您就可以

1. 双击`Unreal\Environments\Blocks`目录下的 .sln 文件来加载Blocks project （或者您自己 [客制](unreal_custenv.md) 的项目）。如果您未看见.sln文件，那可能是您未按照上述步骤执行。
2. 选择一个虚幻项目（project）进行开始（例如 Block project），并确保虚幻引擎的“Build”选项设置为“Develop Editor”（开发者编辑器）和x64模式。
3. 当虚幻编辑器加载后，单击“开始”按钮，小提示：进入“Edit->Editor Preferences“并搜索”CPU“，然后确保 'Use Less CPU when in Background' 未被勾选。

参阅 [使用 APIs](apis.md) 以及 [settings.json](settings.md) 来开启或设置更多功能。

# AirSim on Unity (试验性)

[Unity](https://unity3d.com/) 是另一个非常优秀的游戏引擎，我们目前发布了一个 [试验性](https://github.com/Microsoft/AirSim/tree/master/Unity) 的版本，其尚未完善。

# FAQ
#### 我运行build.cmd时提示 `error C100 : An internal error has occurred in the compiler` 

据我们观察这个错误一般出现在VS的版本为`15.9.0`时，并且已经在AirSim代码中进行了解决。如果您使用这个VS版本，请拉取最新的AirSim代码。 

#### 提示错误 "'corecrt.h': No such file or directory" or "Windows SDK version 8.1 not found"

应该是您安装Virsual Studio时未安装 [Windows SDK](https://developercommunity.visualstudio.com/content/problem/3754/cant-compile-c-program-because-of-sdk-81cant-add-a.html)。

#### 我应该怎么在AirSim中使用PX4固件？

AirSim默认使用其内置的名为[simple_flight](simple_flight.md)的固件，而无需额外的操作。如果您希望使用PX4来操控请参阅 [PX4指引](px4_setup.md)。

#### 我在Visual Studio中进行了更改但是无效果

若您仅修改了header文件，有时Unreal + VS 的build系统并不会对其进行编译。如若希望进行重编译，请在诸如AirSimGameMode.cpp的cpp文件中进行一些无关紧要的修改。

#### Unreal使用电脑中的VS2015或者提示“link error”

电脑中安装了数个VS会导致UE项目编译时出错。其中一个就是UE可能会尝试使用旧版本的VS来进行编译（然而会提示失败），Unreal中有两个设置项，一个是配置引擎的VS版本，另一个是配置项目的VS版本。

1. Edit -> Editor preferences -> General -> Source code
2. Edit -> Project Settings -> Platforms -> Windows -> Toolchain ->CompilerVersion

某些情况下，这些配置可能依然没法另您取得想要的结果，可能会出现如下错误提示：LINK : fatal error LNK1181: cannot open input file 'ws2_32.lib'

以下方式或可解决：

1. 使用[VisualStudioUninstaller](https://github.com/Microsoft/VisualStudioUninstaller/releases)卸载旧版本VS；
2. 修复/安装 VS2017；
3. 重启电脑并且安装Epic launcher和虚幻引擎。