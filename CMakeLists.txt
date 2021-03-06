#
# 86Box		A hypervisor and IBM PC system emulator that specializes in
#		running old operating systems and software designed for IBM
#		PC systems and compatibles from 1981 through fairly recent
#		system designs based on the PCI bus.
#
#		This file is part of the 86Box distribution.
#
#		CMake build script.
#
# Authors:	David Hrdlička, <hrdlickadavid@outlook.com>
#
#		Copyright 2020,2021 David Hrdlička.
#

cmake_minimum_required(VERSION 3.16)

project(86Box
	VERSION 2.10
	DESCRIPTION "Emulator of x86-based systems"
	HOMEPAGE_URL "https://86box.github.io/"
	LANGUAGES C CXX)

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")
include(TargetArch)
target_architecture(CMAKE_TARGET_ARCHITECTURES)

include(CMakeDependentOption)

add_compile_definitions(CMAKE)

option(RELEASE "Release build" OFF)
option(USB "USB support" OFF)
option(DYNAREC "Dynamic recompiler" ON)
option(FLUIDSYNTH "FluidSynth" ON)
option(MUNT "MUNT" ON)
option(VRAMDUMP "Video RAM dumping" OFF)
option(DINPUT "DirectInput" OFF)
option(DISCORD "Discord integration" ON)

option(NEW_DYNAREC "Use the PCem v15 (\"new\") dynamic recompiler" OFF)

option(DEV_BRANCH "Development branch" OFF)
CMAKE_DEPENDENT_OPTION(AMD_K5 "AMD K5" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(CL5422 "Cirrus Logic CL-GD 5402/5420/5422" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(CYRIX_6X86 "Cyrix 6x86" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(GUSMAX "Gravis UltraSound MAX" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(HEDAKA "Hedaka HED-919" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(LASERXT "VTech Laser XT" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(MGA "Matrox Mystique graphics adapters" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(NO_SIO "Machines without emulated Super I/O chips" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(OPEN_AT "OpenAT" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(PAS16 "Pro Audio Spectrum 16" OFF "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(PS1M2133 "IBM PS/1 model 2133" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(PS2M70T4 "IBM PS/2 model 70 (type 4)" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(S3TRIO3D2X "S3 Trio3D/2X" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(SIO_DETECT "Super I/O Detection Helper" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(STPC "STPC machines" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(M1489 "ALi M1489" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(M154X "ALi ALADDiN IV" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(M6117 "ALi M6117" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(VGAWONDER "ATI VGA Wonder (ATI-18800)" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(VNC "VNC renderer" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(XL24 "ATI VGA Wonder XL24 (ATI-28800-6)" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(VECT486VL "HP Vectra 486VL" ON "DEV_BRANCH" OFF)
CMAKE_DEPENDENT_OPTION(DELLS4 "Dell Dimension XPS P60; Dell OptiPlex 560/L" ON "DEV_BRANCH" OFF)

add_subdirectory(src)
