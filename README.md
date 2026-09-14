# ROS 2 入门 21 讲示例代码

本仓库是《ROS 2 入门 21 讲》的配套示例，包含 ROS 2 节点、话题、服务、参数、动作、QoS、TF、Launch、URDF、Gazebo、OpenCV 和自定义接口等练习。

课程资源：

- [课程视频](https://class.guyuehome.com/detail/p_628f4288e4b01c509ab5bc7a/6)
- [图文教程](https://book.guyuehome.com/)
- [课程问答](https://www.guyuehome.com/Bubble/circleDetail/id/90/)

## 环境要求

- Ubuntu 20.04 + ROS 2 Foxy，或 Ubuntu 22.04 + ROS 2 Humble
- 已安装 `colcon`、CMake、C++ 编译器和 Python 构建工具
- Gazebo、OpenCV 等示例需要额外安装对应依赖

本工作区也已在 Ubuntu + ROS 2 Lyrical 环境中完成构建。不同 ROS 2 发行版之间可能存在 API 差异，参见 [Humble 与 Foxy 版本兼容性说明](src/ros2_21_tutorials/Humble与Foxy版本兼容性说明.md)。

## 获取代码

```bash
git clone <repository-url>
cd ros2_ws
```

源码位于 `src/ros2_21_tutorials`。如果使用已有工作区，只需要将该目录放入工作区的 `src` 目录。

## 安装依赖

先加载 ROS 2 环境：

```bash
source /opt/ros/$ROS_DISTRO/setup.bash
```

也可以使用源码目录中的安装脚本自动安装 ROS 2 和常用开发工具。脚本会修改系统软件源和 shell 环境，请确认内容符合本机环境后再执行：

```bash
cd src/ros2_21_tutorials
chmod +x install.sh
./install.sh
```

在依赖已安装的情况下，推荐使用 `rosdep` 检查工作区依赖：

```bash
rosdep install --from-paths src --ignore-src --rosdistro $ROS_DISTRO -r -y
```

## 编译

```bash
source /opt/ros/$ROS_DISTRO/setup.bash
colcon build
source install/setup.bash
```

只编译某个功能包：

```bash
colcon build --packages-select learning_node_cpp
```

清理构建结果后重新编译：

```bash
rm -rf build install log
colcon build
```

## 示例功能包

| 功能包 | 内容 |
| --- | --- |
| `learning_node`、`learning_node_cpp` | Python 和 C++ 节点基础 |
| `learning_topic`、`learning_topic_cpp` | 话题发布与订阅 |
| `learning_service`、`learning_service_cpp` | 服务通信 |
| `learning_action`、`learning_action_cpp` | Action 通信 |
| `learning_parameter`、`learning_parameter_cpp` | 参数使用 |
| `learning_launch` | Launch 文件 |
| `learning_qos` | QoS 配置 |
| `learning_tf`、`learning_tf_cpp` | TF 坐标变换 |
| `learning_interface` | 自定义消息、服务和动作接口 |
| `learning_urdf` | URDF 机器人模型 |
| `learning_gazebo`、`learning_gazebo_harmonic` | Gazebo 仿真 |
| `learning_cv` | OpenCV 图像处理 |

## 运行示例

编译并加载工作区后，使用 `ros2 run` 启动节点：

```bash
ros2 run learning_node_cpp node_helloworld
```

查看某个功能包提供的可执行文件：

```bash
ros2 pkg executables learning_node_cpp
```

Launch 示例使用：

```bash
ros2 launch learning_launch <launch-file>.launch.py
```

具体的可执行文件、Launch 文件和参数请以对应功能包中的 `README.md`、`package.xml` 和源码为准。

## 版本兼容性

本仓库的原始示例主要面向 Humble。Foxy、Humble、Jazzy 及更新发行版在头文件、Action 回调和接口包命名上可能存在差异。遇到编译错误时，优先检查当前 ROS 2 发行版的官方 API 和对应功能包依赖，不要混用不同发行版的 `build`、`install` 或 `log` 目录。
