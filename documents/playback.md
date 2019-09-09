# 回放

AirSim支持播放使用MavLinkTest应用程序记录的* .mavlink日志文件中的高级命令，以便比较真实和模拟飞行。[[recording.mavlink](https://frendowu.github.io/AirSim-docs-zh/playback/logs/recording.mavlink)]是使用以下命令行使用真实无人机捕获的日志文件示例：	

```MavLinkTest -serial:/dev/ttyACM0,115200 -logdir:.```

然后日志文件包含执行的命令，其中包括几个“轨道”命令，得到的飞行GPS地图如下所示：

![real flight](images/RealFlight.png)

## 并排比较

现在我们可以将MavLinkTest记录的* .mavlink日志文件复制到运行AirSim插件的虚幻模拟器的PC上。 当模拟器运行并且无人机停在有空间进行相同操作的地图中时，我们可以运行此MavLinkTest命令行：

```**MavLinkTest** **-server**:127.0.0.1:14550```

这应该连接到模拟器。 现在您可以输入以下命令：

```**PlayLog** **recording**.mavlink```

您在真实无人机上执行的相同命令现在将在模拟器中再次播放。 然后你可以按't'查看轨迹，它会显示真实无人机和模拟无人机的踪迹。 每次再次按't'，你可以重置线路，使它们同步到当前位置，这样我就可以捕获在此录音中执行的“轨道”命令的并排轨迹， 生成下面的图片。 粉红线是模拟飞行，红线是真正的飞行：

![playback](images/Playback.png)

注意：我正在使用';' 键在模拟器中使用键盘控制相机位置以获得此镜头。

## 参数

使用您的真正无人机正在使用的一些相同飞行参数来设置模拟器可能会有所帮助，例如，在我的情况下，我使用的是低于正常的巡航速度，较慢的起飞速度，并且它有助于告诉模拟器 在解除武装之前等待很长时间（COM_DISARM_LAND）并关闭安全开关NAV_RCL_ACT和NAV_DLL_ACT（<font color=#FF0000 >不要</font>在真正的无人机上执行此操作）。

```param MPC_XY_CRUISE 2
param MPC_XY_CRUISE 2
param MPC_XY_VEL_MAX 2
param MPC_TKO_SPEED 1
param COM_DISARM_LAND 60
param NAV_RCL_ACT 0
param NAV_DLL_ACT 0
```

