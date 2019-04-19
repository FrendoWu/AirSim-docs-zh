# 在Linux上构建AirSim

目前验证并推荐的Linux版本为 **Ubuntu 16.04 LTS**。理论上您可以在其他版本或者OSX上构建，但是我们目前并未验证。

## 安装以及Build

1. 确保您已 [注册了Epic Games](https://docs.unrealengine.com/latest/INT/Platforms/Linux/BeginnerLinuxDeveloper/SettingUpAnUnrealWorkflow/1/index.html)。这一步用以获取虚幻引擎的代码。
2. 克隆虚幻引擎到您期望的目录，然后Build。注意：我们目前仅提供对UE4.18版本的支持。
   ```bash
   git clone -b 4.18 https://github.com/EpicGames/UnrealEngine.git
   cd UnrealEngine
   ./Setup.sh
   ./GenerateProjectFiles.sh
   make
   ```
3. 克隆AirSim然后build:
   ```bash
   git clone https://github.com/Microsoft/AirSim.git
   cd AirSim
   ./setup.sh
   ./build.sh
   ```

## Build Unreal Environment

最终，您需要一个内有环境 (environment) 的项目 (project) 来运行AirSim。AirSim内置"Blocks Environment"，或者您也可以参考[设置虚幻环境](unreal_proj.md)来创建自己的项目。

## 配置遥控器控制功能（仅限无人机）

如果您想手动控制无人机，您需要一个遥控器。请查阅 [遥控器控制](remote_control.md) 获取更多细节。

当然，您也可以通过 [APIs](apis.md) 编写程序来进行操控，或者在 [计算机视觉模式](image_apis.md) 下使用键盘来预览环境。

## 如何使用AirSim

一旦您完成了上述步骤，您就可以

1. 进入 `UnrealEngine` 文件夹，然后运行 `UnrealEngine/Engine/Binaries/Linux/UE4Editor`。
2. 当UE提示打开或创建项目时，选择浏览并选择  `AirSim/Unreal/Environments/Blocks` （或者您自己 [客制](unreal_custenv.md) 的项目）。
3. If you get prompts to convert project, look for 当提示您需要转换（convert）项目时，找到并配置More选项或者Convert-In-Place选项。如果提示您build，选择yes，如果提示您禁用AirSim插件，选择no。
4. 加载Unreal Editor后，单击“开始”按钮，小提示：进入“Edit->Editor Preferences“并搜索”CPU“，然后确保 'Use Less CPU when in Background' 未被勾选。

参阅 [使用 APIs](apis.md) 以及 [settings.json](settings.md) 来开启或设置更多功能。

## FAQ

#### 提示错误"<MyProject> could not be compiled. Try rebuilding from source manually"。

This could either happen because of compile error or the fact that your gch files are outdated. Look in to your console window. Do you see something like below?
```
fatal errorfatal error: : file  '/usr/include/linux/version.h''/usr/include/linux/version.h'  has  been  modified  since  the  precompiled  header
```

If this is the case then look for *.gch file(s) that follows after that message, delete them and try again. Here's [relevant thread](https://answers.unrealengine.com/questions/412349/linux-ue4-build-precompiled-header-fatal-error.html) on Unreal Engine forums.

If you see other compile errors in console then open up those source files and see if it is due to changes you made. If not, then report it as issue on GitHub.

#### Unreal crashed! How do I know what went wrong?

Go to the `MyUnrealProject/Saved/Crashes` folder and search for the file `MyProject.log` within its subdirectories. At the end of this file you will see the stack trace and messages. You can also take a look at the `Diagnostics.txt` file.

#### How do I use an IDE on Linux?

You can use Qt Creator or CodeLite. Instructions for Qt Creator are available [here](https://docs.unrealengine.com/latest/INT/Platforms/Linux/BeginnerLinuxDeveloper/SettingUpAnIDE/index.html).

#### Can I cross compile for Linux from a Windows machine?

Yes, you can, but we haven't tested it. You can find the instructions [here](https://docs.unrealengine.com/latest/INT/Platforms/Linux/GettingStarted/index.html).

#### What compiler and stdlib does AirSim use?

We use the same compiler that Unreal Engine uses, **Clang 5.0**, and stdlib, **libc++**. AirSim's `setup.sh` will automatically download them both. The libc++ source code is cloned into the `llvm-source-(version)` folder and is built into the `llvm-build` folder, from where CMake uses libc++.

#### What version of CMake does the AirSim build use?

3.9.0 or higher. This is *not* the default in Ubuntu 16.04 so setup.sh installs it for you. You can check your CMake version using `cmake --version`. If you have an older version, follow [these instructions](cmake_linux.md) or see the [CMake website](https://cmake.org/install/).

#### Can I compile AirSim in BashOnWindows?

Yes, however, you can't run Unreal from BashOnWindows. So this is kind of useful to check a Linux compile, but not for an end-to-end run. See the [BashOnWindows install guide](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide). Make sure to have the latest version (Windows 10 Creators Edition) as previous versions had various issues. Also, don't invoke `bash` from `Visual Studio Command Prompt`, otherwise CMake might find VC++ and try and use that!

#### Where can I find more info on running Unreal on Linux?

* Start here: [Unreal on Linux](https://docs.unrealengine.com/latest/INT/Platforms/Linux/index.html)
* [Building Unreal on Linux](https://wiki.unrealengine.com/Building_On_Linux#Clang)
* [Unreal Linux Support](https://wiki.unrealengine.com/Linux_Support)
* [Unreal Cross Compilation](https://wiki.unrealengine.com/Compiling_For_Linux)
