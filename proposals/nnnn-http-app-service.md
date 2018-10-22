# HTTP App service 

* Proposal: [NNNN](nnnn-http-app-service.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Awaiting review**
* Impacted Platforms: [Core]

## Introduction

This proposal is to create additional service type HTTP with HTTPS connection for AppServices. 

## Motivation

In case in-vehicle cellular data is not available but it's required for Policies, SDL may perform HTTP request via HTTP AppService. 

Robust internet connection is required for:
 - Policy update
 - System updates
 - Vehicle status monitoring
 - Emergency event 

SDL should provide internet connection through mobile within HTTP service in case in-vehicle cellular connection is off.

## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered

No alternatives considered.
