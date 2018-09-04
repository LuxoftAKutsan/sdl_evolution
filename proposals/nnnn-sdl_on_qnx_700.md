# Porting SDL to QNX700 x86 platform

* Proposal: [SDL-NNNN](nnnn-sdl_on_qnx_700.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core, ATF]

## Introduction
This proposal is about porting SDL to QNX700 x86 platform and testing SDL on QNX700 x86.

## Motivation

**QNX 6.5** (currently supported by SDL) is already out of date. New version of QNX released is QNX7.0.  
**QNX 7.0** is widely used by OEM manyfactures, so SDL should support building and working on QNX7.0. 

## Proposed solution

Proposed default platform for QNX is x86 (same as for Linux). 

### Rework of SDL code 

#### 3rd party libraries for QNX7

All third party libraries compiled within SDL should be configured for QNX7(x86):
  - boost
  - libapr
  - libaprutils
  - liblog4cxx
  - bson-clib
  - json
  
For all SDL dependencies should be found versions for QNX7(x86) or alternatives.

#### Refactoring of cmake structure

SDL may use modern cmake approach of creating targets. It will simplify porting SDL on any platform.  
For each third party library used by SDL should be created `.cmake` file, that will expose library as `cmake_library`.

This will allow to make clearer dependencies, avoid dependency gaps (required for multithreading compilation)  
and replace dependency during porting to other platform just with replacing `.cmake` third party library file. 

#### Create QNX7.0 USB transport adapter 

Linux USB transport adapter uses `libusb` library.
For QNX will be used another usb library and additional transport adapter should be created.

#### Create QNX7.0 Bluetooth transport adapter 

Linux USB transport adapter uses `libbluetooth` library.
For QNX will be used another BT library and additional transport adapter should be created.

#### Modify utils component

Utils component will be affected with porting SDL to new QNX7 platform. 

### Provide Ability for automated testing 

Existing automated testing tool [sdl_atf](https://github.com/smartdevicelink/sdl_atf) and 
[scripts](https://github.com/smartdevicelink/sdl_atf_test_scripts)
should be used for checking SDL functionality on the new platform.

#### Modification in sdl_atf

sdl_atf tool should be executed on host workstation, but SDL will be executed on remote virtual QNX7 workstation. 

For support remote automated testing of SDL, the following proposal should be implemented:  https://github.com/LuxoftAKutsan/sdl_evolution/blob/sdl_watchdog/proposals/nnn-atf-sdl-watchdog-service.md 

#### Modification in test scripts

Some scripts should be modified to use sdl on remote workstation.  
All operations with sdl files ( hmi_capabilities, preloaded_pt, etc ...) should be covered with wrappers that support either local or remote execution. 

### Automated transport testing

ATF now supports only TCP transport. 
For automated testing SDL via Bluetooth or USB, the following proposal should be implemented.

## Potential downsides

N/A

## Impact on existing code

SDL core will be modified in platform specific places. Two additional transport adapters will be added. 

ATF will be reworked to support remote sdl testing.

ATF will be reworked to support Bluetooth and USB testing.

## Alternatives considered

Do not create Bluetooth and USB transport adapters for QNX.  
These transport adapters will not be used for real OEMs, the only place to use them is virtual x85 QNX7 workstation. 
But creating and supporting these adapters will help to keep SDL components independent and could be an example for OEM manufactures how to create their own transport adapters.
