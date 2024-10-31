# Copyright (c) 2024 LuckkMaker
# All rights reserved.
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

if(${CONFIG_OMNI_FAMILY} STREQUAL "stm32f1")
    set(FREERTOS_PORT "GCC_ARM_CM3" CACHE STRING "FreeRTOS port name" FORCE)
elseif(${CONFIG_OMNI_FAMILY} STREQUAL "stm32f4" OR ${CONFIG_OMNI_FAMILY} STREQUAL "apm32f4")
    set(FREERTOS_PORT "GCC_ARM_CM4F" CACHE STRING "FreeRTOS port name" FORCE)
elseif (${CONFIG_OMNI_FAMILY} STREQUAL "stm32h7")
    set(FREERTOS_PORT "GCC_ARM_CM7" CACHE STRING "FreeRTOS port name" FORCE)
else()
    message(FATAL_ERROR "CONFIG_OMNI_FAMILY is not set")
endif()

# Add the FreeRTOS configuration file
set(FREERTOS_CFG_SOURCE_FILE ${CMAKE_CURRENT_LIST_DIR}/FreeRTOSConfig.in)
set(FREERTOS_CFG_TARGET_FILE ${OMNI_RTOS_CFG_DIR}/FreeRTOSConfig.h)
omni_add_configure_file(${FREERTOS_CFG_SOURCE_FILE} ${FREERTOS_CFG_TARGET_FILE})

# Set the FreeRTOS configuration file directory
set(FREERTOS_CONFIG_FILE_DIRECTORY ${OMNI_RTOS_CFG_DIR} CACHE STRING "FreeRTOS config file")

add_subdirectory(Source)

add_library(omni-cmsis-freertos INTERFACE)

file(GLOB OMNI_CMSIS_FREERTOS_SOURCES
    "CMSIS/RTOS2/FreeRTOS/Source/cmsis_os2.c"
    "CMSIS/RTOS2/FreeRTOS/Source/os_systick.c"
)

target_sources(omni-cmsis-freertos INTERFACE
    ${OMNI_CMSIS_FREERTOS_SOURCES}
)

target_include_directories(omni-cmsis-freertos INTERFACE
    CMSIS/RTOS2/FreeRTOS/Include
)

target_link_libraries(omni-cmsis-freertos INTERFACE
    freertos_kernel
)
