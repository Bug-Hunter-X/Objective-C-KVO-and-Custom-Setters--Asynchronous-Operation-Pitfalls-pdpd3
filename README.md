# Objective-C KVO and Custom Setters: Asynchronous Operation Pitfalls

This repository demonstrates a potential bug in Objective-C related to Key-Value Observing (KVO) and custom setters that perform asynchronous operations.  Improper handling in such scenarios can lead to infinite loops or race conditions. The provided example shows how this can happen and offers a solution.

## Bug Description
When a custom setter within a KVO-observed class executes asynchronously, it can cause unexpected behavior. The initial KVO notification may trigger the setter, which then triggers further KVO notifications during its asynchronous execution. This chain of events can easily result in an infinite loop or data inconsistencies.

## Solution
The solution involves careful handling of asynchronous operations within the custom setter.  Avoid triggering KVO notifications or further property changes until the asynchronous operation is complete. Often, using a flag or a dedicated dispatch queue for handling the asynchronous changes prevents recursive calls and keeps the KVO mechanism working correctly.

## Files
- `KVOAsyncBug.m`: Demonstrates the buggy implementation.
- `KVOAsyncSolution.m`: Shows the corrected implementation.