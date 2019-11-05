# 在 AirSim 上使用C++的API

本文的提供了C++调用API的样例和一些切合C++特性的细节，在阅读本文档之前请先阅读 [通用 API 文档](apis.md)。

## 快速开始

最快的入门方式是在 Visual Studio 2017 内打开 AirSim.sln。您将在解决方案中看到名为 [Hello Car](https://github.com/Microsoft/AirSim/tree/master/HelloCar/) 以及 [Hello Drone](https://github.com/Microsoft/AirSim/tree/master/HelloDrone/) 的样例代码。这些代码内包含配置好的include路径以及lib路径，您也可以通过参考来迅速的在其他VC++项目中使用。如果您使用的是Linux，那么您需要在 [cmake file](https://github.com/Microsoft/AirSim/tree/master/cmake//HelloCar/CMakeLists.txt) 中配置好相关路径，或者在编译器命令行中传递相应路径。

#### Include 以及 Lib 文件夹
* Include 文件夹: `$(ProjectDir)..\AirLib\deps\rpclib\include;include;$(ProjectDir)..\AirLib\deps\eigen3;$(ProjectDir)..\AirLib\include`
* 依赖: `rpc.lib`
* Lib 文件夹: `$(ProjectDir)\..\AirLib\deps\MavLinkCom\lib\$(Platform)\$(Configuration);$(ProjectDir)\..\AirLib\deps\rpclib\lib\$(Platform)\$(Configuration);$(ProjectDir)\..\AirLib\lib\$(Platform)\$(Configuration)`

## Hello Car

以下代码展示的是如何使用 AirSim APIs  来控制仿真车辆（[Python 版本](apis.md#hello_car)的代码见此）:

```cpp
// 准备好运行这个样例
// ready to run example: https://github.com/Microsoft/AirSim/blob/master/HelloCar/main.cpp

#include <iostream>
#include "vehicles/car/api/CarRpcLibClient.hpp"

int main() 
{
    msr::airlib::CarRpcLibClient client;
    client.enableApiControl(true); //在此禁止手工控制
    CarControllerBase::CarControls controls;

    std::cout << "Press enter to drive forward" << std::endl; std::cin.get();
    controls.throttle = 1;
    client.setCarControls(controls);

    std::cout << "Press Enter to activate handbrake" << std::endl; std::cin.get();
    controls.handbrake = true;
    client.setCarControls(controls);

    std::cout << "Press Enter to take turn and drive backward" << std::endl; std::cin.get();
    controls.handbrake = false;
    controls.throttle = -1;
    controls.steering = 1;
    client.setCarControls(controls);

    std::cout << "Press Enter to stop" << std::endl; std::cin.get();
    client.setCarControls(CarControllerBase::CarControls());

    return 0;
}
```

## Hello Drone

Here's how to use AirSim APIs using Python to control simulated car (see also [Python example](apis.md#hello_drone)):

```cpp

// ready to run example: https://github.com/Microsoft/AirSim/blob/master/HelloDrone/main.cpp

#include <iostream>
#include "vehicles/multirotor/api/MultirotorRpcLibClient.hpp"

int main() 
{
    using namespace std;
    msr::airlib::MultirotorRpcLibClient client;

    cout << "Press Enter to enable API control" << endl; cin.get();
    client.enableApiControl(true);

    cout << "Press Enter to arm the drone" << endl; cin.get();
    client.armDisarm(true);

    cout << "Press Enter to takeoff" << endl; cin.get();
    client.takeoffAsync(5)->waitOnLastTask();

    cout << "Press Enter to move 5 meters in x direction with 1 m/s velocity" << endl; cin.get();  
    auto position = client.getMultirotorState().getPosition(); // 从当前位置开始移动
    client.moveToPositionAsync(position.x() + 5, position.y(), position.z(), 1)->waitOnLastTask();

    cout << "Press Enter to land" << endl; cin.get();
    client.landAsync()->waitOnLastTask();

    return 0;
}
```

## 进一步深入

* 在其他的AirSim项目中使用内部硬件（internal infrastructure）的[示例](../Examples)。
* [DroneShell](../DroneShell) 这个app展示了使用C++ APIs来对无人机进行简单的交互操控。
* [Python APIs](apis.md)

