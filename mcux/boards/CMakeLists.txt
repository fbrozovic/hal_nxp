#
# Copyright (c) 2018, NXP
#
# SPDX-License-Identifier: Apache-2.0
#

if(CONFIG_BOARD_MIMXRT1015_EVK)
  set(MCUX_BOARD evkmimxrt1015)
elseif(CONFIG_BOARD_MIMXRT1020_EVK)
  set(MCUX_BOARD evkmimxrt1020)
elseif(CONFIG_BOARD_MIMXRT1050_EVK OR CONFIG_BOARD_MIMXRT1050_EVK_QSPI)
  set(MCUX_BOARD evkbimxrt1050)
elseif(CONFIG_BOARD_MIMXRT1060_EVK OR CONFIG_BOARD_MIMXRT1060_EVK_HYPERFLASH)
  set(MCUX_BOARD evkmimxrt1060)
elseif(CONFIG_BOARD_MIMXRT1064_EVK)
  set(MCUX_BOARD evkmimxrt1064)
endif()

zephyr_compile_definitions_ifdef(CONFIG_NXP_IMX_RT_BOOT_HEADER XIP_BOOT_HEADER_ENABLE=1)
zephyr_compile_definitions_ifdef(CONFIG_DEVICE_CONFIGURATION_DATA XIP_BOOT_HEADER_DCD_ENABLE=1)
zephyr_compile_definitions_ifdef(CONFIG_BOOT_FLEXSPI_NOR BOARD_FLASH_SIZE=CONFIG_FLASH_SIZE)

zephyr_sources_ifdef(CONFIG_BOOT_FLEXSPI_NOR ${MCUX_BOARD}/${MCUX_BOARD}_flexspi_nor_config.c)
zephyr_sources_ifdef(CONFIG_DEVICE_CONFIGURATION_DATA ${MCUX_BOARD}/${MCUX_BOARD}_sdram_ini_dcd.c)
