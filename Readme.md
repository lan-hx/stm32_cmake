## 环境配置

---

#### Linux

1. 安装必要的包：cmake, ninja, clang-format, clang-tidy

参考：

```shell
sudo apt install cmake git clang-format clang-tidy ninja-build bzip2
```

2. 安装交叉编译器arm-none-eabi

从ARM官网下载：https://developer.arm.com/downloads/-/gnu-rm

新版没有测试：https://developer.arm.com/downloads/-/arm-gnu-toolchain-downloads

参考：

```shell
cd /opt
sudo wget -O gcc-arm-none-eabi-10.3-2021.10-aarch64-linux.tar.bz2 'https://developer.arm.com/-/media/Files/downloads/gnu-rm/10.3-2021.10/gcc-arm-none-eabi-10.3-2021.10-x86_64-linux.tar.bz2?rev=78196d3461ba4c9089a67b5f33edf82a&hash=D484B37FF37D6FC3597EBE2877FB666A41D5253B'
sudo tar -xf gcc-arm-none-eabi-10.3-2021.10-aarch64-linux.tar.bz2
sudo mv gcc-arm-none-eabi-10.3-2021.10 gcc-arm-none-eabi
```

3. 安装STM32Cube

https://github.com/STMicroelectronics/STM32CubeF1

参考：

```shell
cd /opt
sudo git clone https://github.com/STMicroelectronics/STM32CubeF1.git
```

4. 克隆项目

注意：Drivers文件夹下的所有内容不参与编译。可以在创建项目时在`Code Generator Options`中勾选`Add necessary library files as reference in the toolchain project configuration file`避免复制driver文件。

参考：

```shell
cd ~
git clone https://github.com/lan-hx/stm32_cmake.git
cd stm32_cmake
```

5. configure

需要指定如下变量：

- STM32_TOOLCHAIN_PATH：交叉编译器位置
- STM32_CUBE_F1_PATH：STM32Cube位置
- CMAKE_BUILD_TYPE：（可选）优化等级：Debug，RelWithDebInfo，Release，MinSizeRel

参考：

```shell
cmake -B build -G Ninja -DSTM32_TOOLCHAIN_PATH:PATH=/opt/gcc-arm-none-eabi -DSTM32_CUBE_F1_PATH:PATH=/opt/STM32CubeF1 -DCMAKE_BUILD_TYPE=Debug
```

6. 编译

参考：

```shell
cmake --build ./build
```

7. 烧录

编译结果在build/*.elf，百度OpenOCD即可。

---

#### Windows

与Linux相同。

有Visual Studio的clang在类似C:\Program Files\Microsoft Visual Studio\2022\Community\VC\Tools\Llvm\bin的位置，ninja在类似C:\Program Files\Microsoft Visual Studio\2022\Community\Common7\IDE\CommonExtensions\Microsoft\CMake\Ninja的位置。

更推荐MinGW-w64+GCC+LLVM+Ninja+...的大礼包：https://winlibs.com/
