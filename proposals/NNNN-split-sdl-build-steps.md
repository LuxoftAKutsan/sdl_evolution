# Split SDL build steps

* Proposal: [SDL-NNNN](NNNN-split-sdl-build-steps.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

Building of SDL should not affect user system implicitly. 
`make` command should perform only SDL building.
Building third party libs should be extracted to a separate build step.
All libs, required for SDL may be already installed in the system, and SDL should not force theirs reinstallation. 

## Motivation

Currently SDL is trying to build all third party libraries during 'make' command. 
Because of that, 'make' command requires sudo access during installation of third party libraries to the system.
First of all it prevents SDL building with IDE (as a rule IDE does not support password prompt)
Also that is a bad practice that SDL installs something to the system during build. 
Building third party libraries and installing them to the system should be separate steps.

## Proposed solution

Split SDL build to the folowing steps : 

#### 1 Build third party libraries in make target:

`make third-party`

Build all third party libraries

#### 2 Install third party libraries in make target:

`make third-party-install` 

_make third-party-install may require root access_

Install all third party libraries to the system or by path regulated by environment variables

#### 3. Build SDL
`make` 

#### 4. Install SDL
`make install`
Install all required stuff for runnng SDL to the `bin` folder or by path regulated by environment variables

If third party libraries are already installed in the system, only `make` step required.

## Potential downsides

Additional steps could be not obvious for newcommers, and should be documentated in README.md

## Impact on existing code

Impacts only configuration files. Should not impact neither SDL behaviour nor SDL code.  

## Alternatives considered

Third party libraries could be extracted to a separate repository however it may be hard to support their versions matching with SDL. 
