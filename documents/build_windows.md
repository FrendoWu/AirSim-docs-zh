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

## Setup Remote Control (Multirotor only)

A remote control is required if you want to fly manually. See the [remote control setup](remote_control.md) for more details.

Alternatively, you can use [APIs](apis.md) for programmatic control or use the so-called [Computer Vision mode](image_apis.md) to move around using the keyboard.

## How to Use AirSim

Once AirSim is set up by following above steps, you can,

1. Double click on .sln file to load the Blocks project in `Unreal\Environments\Blocks` (or .sln file in your own [custom](unreal_custenv.md) Unreal project). If you don't see .sln file then you probably haven't completed steps in Build Unreal Project section above.
2. Select your Unreal project as Start Up project (for example, Blocks project) and make sure Build config is set to "Develop Editor" and x64.
3. After Unreal Editor loads, press Play button. Tip: go to 'Edit->Editor Preferences', in the 'Search' box type 'CPU' and ensure that the 'Use Less CPU when in Background' is unchecked.

See [Using APIs](apis.md) and [settings.json](settings.md) for various options available.

# AirSim on Unity (Experimental)
[Unity](https://unity3d.com/) is another great game engine platform and we have an [experimental release](https://github.com/Microsoft/AirSim/tree/master/Unity) of AirSim on Unity. Please note that this is work in progress and all features may not work yet. 

# FAQ
#### I get `error C100 : An internal error has occurred in the compiler` when running build.cmd
We have noticed this happening with VS version `15.9.0` and have checked-in a workaround in AirSim code. If you have this VS version, please make sure to pull the latest AirSim code.

#### I get error "'corecrt.h': No such file or directory" or "Windows SDK version 8.1 not found"
Very likely you don't have [Windows SDK](https://developercommunity.visualstudio.com/content/problem/3754/cant-compile-c-program-because-of-sdk-81cant-add-a.html) installed with Visual Studio. 

#### How do I use PX4 firmware with AirSim?
By default, AirSim uses its own built-in firmware called [simple_flight](simple_flight.md). There is no additional setup if you just want to go with it. If you want to switch to using PX4 instead then please see [this guide](px4_setup.md).

#### I made changes in Visual Studio but there is no effect

Sometimes the Unreal + VS build system doesn't recompile if you make changes to only header files. To ensure a recompile, make some Unreal based cpp file "dirty" like AirSimGameMode.cpp.

#### Unreal still uses VS2015 or I'm getting some link error
Running several versions of VS can lead to issues when compiling UE projects. One problem that may arise is that UE will try to compile with an older version of VS which may or may not work. There are two settings in Unreal, one for for the engine and one for the project, to adjust the version of VS to be used.
1. Edit -> Editor preferences -> General -> Source code
2. Edit -> Project Settings -> Platforms -> Windows -> Toolchain ->CompilerVersion

In some cases, these settings will still not lead to the desired result and errors such as the following might be produced: LINK : fatal error LNK1181: cannot open input file 'ws2_32.lib'

To resolve such issues the following procedure can be applied:
1. Uninstall all old versions of VS using the [VisualStudioUninstaller](https://github.com/Microsoft/VisualStudioUninstaller/releases)
2. Repair/Install VS2017
3. Restart machine and install Epic launcher and desired version of the engine