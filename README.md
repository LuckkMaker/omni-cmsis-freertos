# omni-cmsis-freertos

[![Version](https://img.shields.io/github/v/release/LuckkMaker/omni-cmsis-freertos)](https://github.com/LuckkMaker/omni-cmsis-freertos/releases/latest)


## 介绍

**omni-cmsis-freertos** 是 [omni](https://github.com/LuckkMaker/omni) 的一个库。 它基于 [CMSIS-FreeRTOS](https://github.com/ARM-software/CMSIS-FreeRTOS) 项目，增加 CMakeLists.txt 使其能够与 omni 一起使用。

[omni](https://github.com/LuckkMaker/omni) 项目是一个利用 CMake 和 kconfig 构建的嵌入式开发框架，同时提供 HAL 层驱动和各种组件驱动。用户可以根据不同板卡、不同模块的需求，自由选择需要的组件，构建自己的固件。并且提供 dev container 的支持，让可以在 docker 容器中快速开发、编译、调试固件，免去搭建开发环境的烦恼。

可以从 [releases page](https://github.com/LuckkMaker/omni/releases) 获取最新的 omni 版本。
