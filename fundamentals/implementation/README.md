# Implementation

The _Implementation_ is a complete separate part of the asset that depends on the _Core_. Its main goal is to provide character-oriented systems that can be useful for the user.

These are some of the terms the implementation uses a lot:

|                 |                                                           |
| --------------- | --------------------------------------------------------- |
| StateController | A finite state machine (FSM) used to handling each state. |
| State           | Where the logic is stored.                                |
| Brain           | This component handles everything related to actions      |
| Action          | An interface that represents a virtual input signal.      |
