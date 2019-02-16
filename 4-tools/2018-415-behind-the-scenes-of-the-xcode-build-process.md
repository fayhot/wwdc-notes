# [2018 415 Behind the Scenes of the Xcode Build Process](https://developer.apple.com/videos/play/wwdc2018/415/)

2018-415-behind-the-scenes-of-the-xcode-build-process.md

- Jake Petroules, Xcode Build System Team
- Jürgen Ributzka, Clang Frontend Team
- Devin Coughlin, Program Analysis Team
- Louis Gerbarg, Linker Team

Topic|Speaker|Time|Page
---|---|---|---
Build System | Jake Petroules, Xcode Build System Team | | 
Clang Builds | Jürgen Ributzka, Clang Frontend Team | 1320 | p61
Swift Builds | Devin Coughlin, Program Analysis Team | | p148
Linking | Louis Gerbarg, Linker Team | | p217


## Exploring the Xcode Build Process: Build System


Clang and Swift

Linker


The build process
automates a series of tasks

### Build Task Execution Order

Build tasks are executed in  dependency order

What Happens When You Press Build?

### Build Process Represented as a Directed Graph

Execution of the Build Graph

llbuild Execution Engine: Open Source

Discovered Dependencies

Incremental Builds


Change Detection and Task Signatures
• Each task in the build graph has a signature
• Computed from stat info of inputs and other task metadata
• Build system tracks task signatures of current and previous build
• Compared to determine whether a task should be run

> How can you help the build system?

Don't Think About the Order of Task Execution!

Think in Terms of Task Dependencies

### Where Do Dependencies Come From?

- Built in
- Target dependencies
- Implicit dependencies
- Build phase dependencies
- Scheme order dependencies
- lastly, You!


### Declare Inputs and Outputs!


### Avoid Auto-Link for Project Dependencies

### Add Explicit Dependencies

### Create Workspaces and Project References


## Clang Builds | Jürgen Ributzka, Clang Frontend Team | 1320 | p61

What Is Clang?
Apple’s official compiler for the C language family

C / C++ / Objective-C / Objective-C++

Traditional C Language Compilation


On the Search for Our Cat


`$ clang <list of arguments> -c Cat.mm -o Cat.o -v`

On the Search for Our Cat

#include "..." search starts here:   
   
#include <...> search starts here:

What Are Header Maps?

PetKit-project-headers.hmap:

PetKit-own-target-headers.hmap:

Clang Builds | Jürgen Ributzka, Clang Frontend Team | 1320 | p61

## Swift Builds | Devin Coughlin, Program Analysis Team | | p148


## Linking | Louis Gerbarg, Linker Team | | p217