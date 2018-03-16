---
layout: page
title: "October 23, 2017"
date: 2017-10-23
author: "Nate Foster"
category: ldwg
---

Attendees: Nate Foster (Cornell), Andy Fingerhut (Cisco), Chris
Sommers (IXIA), Kingshuk Mandal (IXIA), Cole Schlesinger, Milad
Sharif, Calin Cascaval (Barefoot), Mihai Budiu (Vmware), Andy Keep
(Cisco), Joe Tardo (Broadcom)

First meeting since spring. Goal is to discuss accumulated issues and
prioritize proposals for new language features.

# Accumulated Issues    
    
* [Issue 273](https://github.com/p4lang/p4-spec/issues/273)
    - reading undefined values
        - for portability we would like to see whether there is some pattern that we can agree on
    - **AI** @jafingerhut to generate PR that clarifies behavior 

* [Issue 284](https://github.com/p4lang/p4-spec/issues/284)
    - header stacks: do P4_X allow holes or not?
    - Goal: make sure that P4_16 and bmv2 are in sync, and ensure that the translation from P4_14 is correct
    - **AI** @jnfoster to generate PR that harmonizes specifications

* [Issues 294](https://github.com/p4lang/p4-spec/issues/294) and [Issue 331](https://github.com/p4lang/p4-spec/issues/331)
    - do we allow compile time constants into expressions?
    - **AI**: @jnfoster to convert into community project

* [Issue 364](https://github.com/p4lang/p4-spec/issues/364)
    - instantiation context and constructor params
    - matrix:
        - calling parsers from controls (and reverse) is not well defined due to the nature of operations (and restrictions).
        - externs have a clear interface for the data plane
        - tables can be wrapped into controls and passed around
        - tables in parsers -    - we could consider it
    - externs instantiated in packages?
        - package bodies
    - **AI** @ccascaval to re-merge

* P4-14 fixes
    - Ali Kheradmand at UIUC has been modeling P4_14 in K
    - Mihai: what happens to legacy code if the semantics changes?
        - owners of legacy code should push back
    - **AI** @jnfoster to encourage Ali finish these as PRs and then tackle P4_16

* [Issue 342](https://github.com/p4lang/p4-spec/issues/342)
    - bit vector structs within headers or structs
    - there is a PR 
    - ordering constraints depending on how it is used
    - **AI** @akeep to organize a small subgroup to explore the notion of serializable types with @jafingerhut, @mbudiu-vmware, @sethfowler

* [Issue 198](https://github.com/p4lang/p4-spec/issues/198) and [Issue 341](https://github.com/p4lang/p4-spec/issues/341)
    - issues: syntax ({} vs. []), holes, defaults, semantics of empty tuple
    - `setValid` and `setInvalid` operations
    - proposed extern: `void zero<T>(out T v)`?
    - **AI** @jnfoster to convert into community project
    
* [Issue 151](https://github.com/p4lang/p4-spec/issues/151) and [Issue 76](https://github.com/p4lang/p4-spec/issues/76)
    - calling actions from parsers
    - function definition: trivial to implement in the compiler (since basically already implemented)
    - virtual functions: allowed only in the body of the extern
    - named params
    - **AI** @milad14000 to organize a small subgroup

* [Issue 51](https://github.com/p4lang/p4-spec/issues/51)
    - field list: function that takes a struct and returns a tuple.
    - not a field reference.
    - **AI** @ccascaval to organize a small subgroup

* [Issue 264](https://github.com/p4lang/p4-spec/issues/264)
    - operations on varbits
    - **AI** @jnfoster to punt to later

# Next Version

* It's time to thinking about new features for next language version

# Future meetings
    
* Resolved to meet about once a month for now