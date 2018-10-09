# Porting SDL to Automotive Grade Linux (AGL) x86 platform

* Proposal: [SDL-NNNN](nnnn-sdl_on_GL.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core, ATF]

## Introduction

This proposal is about porting SDL to Automotive Grade Linux (AGL) x86 platform and automated testing in this platform

## Motivation

Automotive Grade Linux (AGL) is new perspective opensource Linux distributive for automotive industry.
Most of auto supliers decalred support of AGL. 
SDL is Unix compatible system and should guarantee ability to use it on AGL. 

## Proposed solution

Add to list of compatible systems : Automotive Grage Linux. 

### Compilation

After implementation of **Porting SDL to QNX700 q86 platform** proposal new target system may be added just with creagin additional cmake toolchain file.

#### 3rd party libraries for AGL

All third party libraries compiled within SDL should be configured for AGL(x86):
  - boost
  - libapr
  - libaprutils
  - liblog4cxx
  - bson-clib
  - json

### Runtime SDL dependencies  

SDL has folowing runtime dependencies : 

```
$ ldd smartDeviceLink
    linux-vdso.so.1 (0x00007ffdbf543000)
    libpthread.so.0 => /lib/x86_64-linux-gnu/libpthread.so.0 (0x00007fb77f45f000)
    libdl.so.2 => /lib/x86_64-linux-gnu/libdl.so.2 (0x00007fb77f25b000)
    libbluetooth.so.3 => /usr/lib/x86_64-linux-gnu/libbluetooth.so.3 (0x00007fb77f038000)
    libusb-1.0.so.0 => /lib/x86_64-linux-gnu/libusb-1.0.so.0 (0x00007fb77ee20000)
    libPolicy.so (0x00007fb77e062000)
    libcrypto.so.1.0.0 => /usr/lib/x86_64-linux-gnu/libcrypto.so.1.0.0 (0x00007fb77dc1f000)
    libssl.so.1.0.0 => /usr/lib/x86_64-linux-gnu/libssl.so.1.0.0 (0x00007fb77d9b7000)
    libstdc++.so.6 => /usr/lib/x86_64-linux-gnu/libstdc++.so.6 (0x00007fb77d1ed000)
    libgcc_s.so.1 => /lib/x86_64-linux-gnu/libgcc_s.so.1 (0x00007fb77cfd5000)
    libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007fb77cbe4000)
    /lib64/ld-linux-x86-64.so.2 (0x00007fb78220b000)
    libudev.so.1 => /lib/x86_64-linux-gnu/libudev.so.1 (0x00007fb77c9c6000)
    libsqlite3.so.0 => /usr/lib/x86_64-linux-gnu/libsqlite3.so.0 (0x00007fb77c294000)
    libm.so.6 => /lib/x86_64-linux-gnu/libm.so.6 (0x00007fb77bef6000)
    librt.so.1 => /lib/x86_64-linux-gnu/librt.so.1 (0x00007fb77bcee000)
    libcrypt.so.1 => /lib/x86_64-linux-gnu/libcrypt.so.1 (0x00007fb77b882000)
```

This libraries should be ported and preinstalled on the distribution of of AGL linux before running SDL. 

### Automated testing 

Existing automated testing tool [sdl_atf](https://github.com/smartdevicelink/sdl_atf) and 
[scripts](https://github.com/smartdevicelink/sdl_atf_test_scripts)
should be used for checking SDL functionality on the new platform.

#### Modification in sdl_atf

sdl_atf tool should be executed on host workstation, but SDL will be executed on remote virtual AGL workstation. 

For support remote automated testing of SDL, the following proposal should be implemented:  https://github.com/LuxoftAKutsan/sdl_evolution/blob/sdl_watchdog/proposals/nnn-atf-sdl-watchdog-service.md 

#### Modification in test scripts

Some scripts should be modified to use sdl on remote workstation.  
All operations with sdl files ( hmi_capabilities, preloaded_pt, etc ...) should be covered with wrappers that support either local or remote execution. 

## Potential downsides

N/A

## Impact on existing code

SDL core will be modified in platform specific places. 

ATF will be reworked to support remote sdl testing.

ATF will be reworked to support Bluetooth and USB testing.

## Alternatives considered

N/A
