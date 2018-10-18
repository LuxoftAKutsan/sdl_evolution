# HTTP App service 

* Proposal: [NNNN](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

Create for AppServices additional service type : HTTP

## Motivation

In case if cellular data in vehicle is not available but it required for Policies, SDL may perform HTTP request via HTTP App service. 

Robust internet connection required for :
 - Policy update
 - System updates
 - Vehicle status monitoring
 - Emergency event 

SDL should provide internet connection through mobile within HTTP service in case if in vehicle cellular is down.

## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered
