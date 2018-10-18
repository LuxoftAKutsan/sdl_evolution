# Low level non RPC application services 

* Proposal: [SDL-0168](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Reviewing**
* Impacted Platforms: [Core]

## Introduction

Provide for application ability to register own non RPC services that may handle arbitary data. 

Communication between SDL and mobile consist of Different levels:
 
 1. Transport level
 2. Protocol level
 3. RPC/Streaming/Bulk level

SmartDeviceLink Protocol may also transfer arbitary data. 
So if application will not be required to implement and to use RPC for communication with SDL for some use cases. 

 
## Motivation
## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered
