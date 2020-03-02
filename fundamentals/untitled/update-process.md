# Update process

The update process can be explained parting from the concept of a _**Scene**_. 

## Scene

In the eyes of CCP, a scene works just like a regular Unity's scene. Instead of game objects there are **actors** moving around and/or interacting with each other. 

There are two types of actors:

|  |  |
| :--- | :--- |
| Character Actor | It represents a **character**. This is also the main component of any character in the scene. |
| Kinematic Actor | It represents a **kinematic rigidbody**. This can be used to represent more than one type of kinematic rigidbodies, such as moving/rotating platforms, a camera, or anything else. |

### Scene Controller

A _scene controller_ is responsible for updating the position and rotation of all the actors in the scene. It is also responsible for guaranteeing a nice interpolated movement, especially for characters affected by dynamic platforms.

![](../../.gitbook/assets/scenecontroller.png)

A way to control the interpolation process is required because of the way that _MovePosition_ and _MoveRotation_ work \(For more information about these methods check the [Unity's scripting reference](https://docs.unity3d.com/ScriptReference/Rigidbody2D.MovePosition.html)\).

{% hint style="warning" %}
It is mandatory for the SceneController to be present in the scene, otherwise the characters and the kinematic actors won't update. 

**You do need to add manually this component to the scene \(1.0.4 onwards\).**
{% endhint %}



