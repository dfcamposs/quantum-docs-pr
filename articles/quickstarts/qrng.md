---
title: Create a Quantum Random Number Generator
description: Build a Q# project that demonstrates fundamental quantum concepts like superposition by creating a quantum random number generator.
author: megbrow
ms.author: megbrow@microsoft.com
ms.date: 10/25/2019
ms.topic: article
uid: microsoft.quantum.quickstarts.qrng
---


# Quickstart: Implement a Quantum Random Number Generator in Q#
A simple example of a quantum algorithm written in Q# is a quantum random number generator. This algorithm leverages the nature of quantum mechanics to produce a random number. 

## Prerequisites

- The Microsoft [Quantum Development Kit](install).
- [Create a Q# Project](xref:microsoft.quantum.howto.createproject)


## Write a Q# operation

As mentioned in our [What is Quantum Computing?](xref:microsoft.quantum.overview.what) a qubit is a unit of quantum information that can be in superposition. When measured, a qubit can only be either 0 or 1, however during execution, the state of the qubit represents the probability of reading either a 0 or a 1 during measurement. We can use this probability to generate random numbers.

### Q# operation code

1. Replace the contents of the Operation.qs file with the following code:

    ```qsharp
    namespace Quantum {
    open Microsoft.Quantum.Intrinsic;

    operation QuantumRandomNumberGenerator() : Result {
        using(q = Qubit())  { // Allocate a qubit.
            H(q);             // Put the qubit to superposition. It now has a 50% chance of being 0 or 1.
            let r = M(q);     // Measure the qubit value.
            Reset(q);
            return r;
            }
        }
    }
    ```

Here we introduce the `Qubit` datatype, native to Q#. We can only allocate a `Qubit` with a `using` statement. When it gets allocated a qubit is always in the `Zero`  state. 

Using the `H` operation, we are able to put our `Qubit` in superposition. To measure a qubit and read its value you use the `M` intrinsic operation.

By putting our `Qubit` in superposition and measuring it, our result will be a different value each time the code is invoked. 

When a `Qubit` is de-allocated it must be explicitly set back to the `Zero` state, otherwise the simulator will report a runtime error. An easy way to achieve this is invoking `Reset`.