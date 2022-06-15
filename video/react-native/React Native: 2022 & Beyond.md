React Native: 2022 & Beyond - Gant Laborde & Jamon Holmgren
- https://www.youtube.com/watch?v=AY5OWFerN6g&list=WL&index=2&t=2s

## React Native Origins
- Generalized Components
View, ScrollView, Text, TextInput

Virtual DOM 			Shadow Tree
DOM Layout Rules --> 	Yoga Layout

## The Text Component
- A UILabel is created on IOS devices.
- A TextView is created on Android devices.

## Abstract Comopnents
- The React Native platform independence

React concepts for all platform UIs

React Native -> Shadow Tree Bridge -> Host Platform

## React Native 
### Dev-Divide

- React Powered Code
React knowledge

- Javascript Expertise
NPM Etc

- Platform Specifics
Platform knwledge Native Language

- React Native Abstraction
React Native Components

## React Native
### Device Diversity


## React Native Bridge
###  The Layer that permits Javascript and host platforms to interact

Single-threaded
- Host Native Swift/Kotlin
- Serialized Batched Payload(strings)
- Serialized Batched Responsed(strings)
- Javascript

## Saturating the Bridge
### It's rare but it can happen

The Bridge Has Limits
And each of these native modules has a significant impact on app startup time.

Speeding Up with Hermes
- OS Javascript Engine for React Native

Improve Performance
Enable Hermes

1. Faster Start-up
2. Smaller App Size
3. Decreased Memory
4. Open Source

## What's Fabric?
### And why sould i care?

## Fabric Renderer
### Why re-render?

- Easier Server Side Rendering
- Concurrent Features
- Integration with React Suspense
- Improved Interoperability
- Priority and Synchronous Events

## Fabric Renderer
### New architecture - New benefits

- Type safety JS to Host
- JSI Direct Access
- Shared C++ Core
- Faster Startup

## The JSI
### Bye Bye Bridge!!! C++ core

React Native, JSI, Hermes -> Shadow Tree

## Abstract Components
### The React Natie platform independence

- React concepts for all platform UIs

React Event Handling -> Fabric Tree Creation -> Fabric Layout with Yoga -> Fabric Commit -> Mount into Host Platform

## What are TurboModules?
### And why should i care?

## Original Native Modules
### Host platform communication

- Eager Initialization
- No Call Verification
- Singleton Lifecycle
- Repeat Runtime Packaing
- Runtime Native Constants

TurboModules
- JSI C++ to the rescue

- Lazy Load Native Modules
- Untethered from UI
- CodeGen C++ Shapes / Types
- Backwards Compatible

What is Codegen?
- And why should i care?

When!?
- When can we start using this?

In Summary
- It's about efficiency

React 18 
- Concurrent renderer
- Suspense
- Automatic batching

No Bridge
- JSI - direct communication between host & JS
- No serializing/deserializing

