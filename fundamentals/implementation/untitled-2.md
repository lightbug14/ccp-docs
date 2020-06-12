# Kinematic actors

Just like character actors, a kinematic actor is another fundamental part of the scene. These objects can be **platforms** or **cameras**.

## Kinematic platforms

The package includes components that allow to script the movement/rotation of a platform in a particular way \(depending on the component\).

All the moving/rotating platforms components are child classes from the _KinematicPlatform_ class. Currently there are two types of kinematic platforms:

### Node based platform

These platforms movement and rotation are purely based on nodes. Use this component to create platforms that moves and rotate precisely following a predefined path.

![](../../.gitbook/assets/platform-node.gif)

### Action Based platform

These platforms movement and rotation are defined by a single action. Use this component if you want to create platforms with a pendulous nature, or infinite duration actions \(for instance, if the platform should rotate forever\).

![](../../.gitbook/assets/platform-action.gif)

### Externally controlled platform

The _KinematicPlatform_ component is not an abstract component, this basically means that can be assigned to a gameObject, just like any other component. If you assign

These platforms are completely handled by an external component, the most common case is the animation clip \(using the Animate Physics mode\).

![](../../.gitbook/assets/platform-animated.gif)

