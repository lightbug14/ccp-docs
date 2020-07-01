# Components

The core consist of the following components:

### Character body

This component contains all the information related to the character body, such as body size, shape, physics supported, etc.

### Character actor

The main character component. It takes care of all the important actions \(movement, rotation, size, among other things\). It also holds all the collision information and is responsible for triggering events. Basically the entire package refer in one way or another to this component.

### Character debug

This component is used for debug purposes, mainly to print information on screen about the collision flags, values and triggered events.

### Scene Controller

A controller for all the characters and kinematic rigidbodies in the scene. This component is used to guarantee a correct rigidbody interpolation and execution order.



