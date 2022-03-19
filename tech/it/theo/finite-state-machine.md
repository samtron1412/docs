[TOC]

# Overview

- A finite-state machine (FSM) or a state machine is a mathematical
  model of computation.
- It's an abstract machine that can be in exactly one of a finite number
  of states at any given time.
- The FSM can change from one state to another in response to some
  inputs; the change from one state to another is called `transition`.
- A FSM is described by a list of states, its initial state, and the
  inputs that trigger each transition.
- There are 2 types
    + `Deterministic finite-state machines`
    + `Nondeterministic finite-state machines`
- Examples
    + Simple examples are vending machines, which dispense products when
      the proper combination of coins is deposited
    + elevators, whose sequence of stops is determined by the floors
      requested by riders
    + traffic lights, which change sequence when cars are waiting
    + combination locks, which require the input of a sequence of
      numbers in the proper order.
- A FSM has less computational power than a Turing machine
    + A finite-state machine has the same computational power as a
      Turing machine that is restricted such that its head may only
      perform "read" operations, and always has to move from left to
      right

# References

[wiki]: https://en.wikipedia.org/wiki/Finite-state_machine
