# Download Binaries

You can simply download precompiled binaries and run to get started immediately. If you want to set up your own Unreal environment then please see [these instructions](https://github.com/Microsoft/AirSim/#how-to-get-it).

### Unreal Engine

**Windows**: Download the binaries for the environment of your choice from the [latest release](https://github.com/Microsoft/AirSim/releases).

**Linux**: Binaries for Ubuntu 16.04 LTS is coming soon. For now you will need to [build it on Linux](build_linux.md) yourself.

### Unity (Experimental)
A free environment called Windridge City is available at [Unity Asset Store](https://assetstore.unity.com/) as an experimental release of AirSim on Unity. Please note that this is work in progress and all features may not work yet.

## Controlling Vehicles
Most of our users typically use [APIs](apis.md) to control the vehicles. However if you can also control vehicles manually. You can drive the car using keyboard, gamepad or [steering wheel](steering_wheel_installation.md). To fly drone manually, you will need either XBox controller or a remote control (feel free to [contribute](../CONTRIBUTING.md) keyboard support). Please see [remote control setup](remote_control.md) for more details. Alternatively you can use [APIs](apis.md) for programmatic control or use so-called [Computer Vision mode](image_apis.md) to move around in environment using the keyboard.

## Don't Have Good GPU?
The AirSim binaries, like CityEnviron, requires a beefy GPU to run smoothly. You can run them in low resolution mode by editing the `run.bat` file on Windows like this:
```
start CityEnviron -ResX=640 -ResY=480 -windowed
```

