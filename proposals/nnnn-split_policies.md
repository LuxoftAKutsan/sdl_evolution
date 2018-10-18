# Split Policies to logicaly separated data bases 

* Proposal: [SDL-0168](nnnn-split_policies.md)
* Author: [Alexander Kutsan](https://github.com/LuxoftAKutsan)
* Status: **Reviewing**
* Impacted Platforms: [Core]

## Introduction

Extract data not related to policies from polcy table.

Data :
 - consumer friendly messages
 - usage statistics

This information has no influence to application and device restrictions. So it could be done separate logical data bases.

## Motivation

Resolved Problems with the approach :

    Big amount of communications for policy update
    Policy table is big and complicated
    Reduce frequency of policy Update

## Proposed solution
![New design approach](../assets/proposals/nnnn-split_policies/new_design.png)

## Potential downsides

## Impact on existing code

## Alternatives considered
