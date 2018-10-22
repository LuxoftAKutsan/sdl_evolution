# HTTP App service 

* Proposal: [NNNN](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

Create additional service type : HTTP with HTTPS connection for AppServices 

## Motivation

In case if in-vehicle cellular data is not available but it's required for Policies, SDL may perform HTTP request via HTTP App service. 

Robust internet connection required for :
 - Policy update
 - System updates
 - Vehicle status monitoring
 - Emergency event 

SDL should provide internet connection through mobile within HTTP service in case if in-vehicle cellular connection is down.

## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered
