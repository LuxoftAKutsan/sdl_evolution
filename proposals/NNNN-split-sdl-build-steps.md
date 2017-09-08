# Split SDL build steps

* Proposal: [SDL-NNNN](NNNN-split-sdl-build-steps.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

Building of SDL should not affect user system implicitely. 
`make` command should perform only sdl builing.
Building 3rd-party libs should be extracted to separate build step.
All libs, required for sdl may be already instelled in the sytem, and sdl should not force it's reinstalation. 

## Motivation

Currently SDL is trying to build all 3rd-party libraries during 'make' command. 
Because of that, 'make' command requires sudo access during to install 3rd paty libraries to the sysytem.
First of all it prevents building sdl from IDE(moustly IDE does not support password prompt)
Also it is bad practice that SDL install something to the system during build. 
Building third party libraries ans installing them to the system should be separate steps.

## Proposed solution

Split sdl build to the folowing steps : 

1. Build third party libraries in make target:

`make third-party`

Build all 3rd party libraries

2 Install third party libraries in make target:

`make third-party-install` 

_make third-party-install may require root access_
Install all 3rd party libraries to the system or path regulated by environment variables

3. Build sdl
`make` 

4. Install SDL
`make install`
Install all required stall for runnng SDL to the `bin` folder or path regulated by environment variables

If third party libraries are already in the system, only `make` step required.

## Potential downsides

Additional steps should be not obvious for wecommers, and should be codumentated in README

## Impact on existing code

Impacts only configuration files. Should not impact neither sdl behaviour nor sdl code.  

## Alternatives considered

Extract thirtparty libraries to separate repository. but t would be hard to support and keep matching versions with SDL. 
