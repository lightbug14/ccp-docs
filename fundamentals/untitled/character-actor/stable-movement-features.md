# Stable movement features

These features from the CharacterActor component \(as seen in the previous section\) **will be applied only if the character is stable**.

## Movement

### Velocy projection

Internally, when the character is stable, the CharacterActor component will project the input velocity \(Linear Velocity\) onto the current ground surface \(Projected Velocity\).



![](../../../.gitbook/assets/velocityproj.png)

This process will always maintain the initial velocity magnitude, regardless of the slope angle.

### Collide and Slide

This algorithm is responsible for determining obstacles along the way. If the encountered surface is allowed the character will walk onto it \(maintaining always the displacement magnitude\). if not, the slope will be considered as an invisible wall.

 ![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LvxVSjyzvP6F7c9h_Hu%2F-Lyt9souh6_VeUiYsTZu%2F-LytFnIU3mJv2SpAT3_q%2FSlopes_3D.png?alt=media&token=4b2637cd-a160-4c7f-b9b0-f44c8c9d06fc) ​![](https://firebasestorage.googleapis.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LvxVSjyzvP6F7c9h_Hu%2F-Lyt9souh6_VeUiYsTZu%2F-LytFrrCQmHQOtJv-a52%2FSlopes_3D_allowed.png?alt=media&token=5102a348-1c78-47a4-9ded-db24192f7dad)

## Grounding

### Step up/down

This feature is responsible for putting the character on the ground \(if there is one\). There are two important values to consider:

* **Step up distance:** Any stable surface below this height will be walkable by the character.
* **Step down distance:** When losing contact with the ground, if the distance between the character and the ground is less or equal to this value, then the character will be automatically _grounded_ \(sticking to the ground\)_._ If there is no ground at all, then the character will be _not grounded_.

![Step up.](../../../.gitbook/assets/bitmap.png)

![Step down.](../../../.gitbook/assets/bitmap2.png)

### Edge Compensation

Normally, when a character is standing **on an edge** it collision shape will make contact with it. What edge compensation does is to lift up the capsule, simulating a cylinder shape. 

![](../../../.gitbook/assets/ledgenormal.png)    ![](../../../.gitbook/assets/ledgeon.png) 

This feature only works on edges, for slopes you will get the same results as before \(with edge compensation disabled\).

### Dynamic Ground

If the current ground the character is standing on moves/rotates, then the character will move and/or rotate with it \(only yaw rotation allowed\).

![](../../../.gitbook/assets/dynamic.png)



A valid dynamic ground must:

1. Be updated during the physics simulation. This also means that animated objects need to use the **AnimatePhysics** UpdateMode \(_Animator_ component\).

So, a valid dynamic can be:

* **Kinematic rigidbody** that moves/rotates using **MovePosition**/**MoveRotation**.
* **Kinematic rigidbody** that moves/rotates based on an **animation clip**.
* **Dynamic rigidbody** that moves/rotates using linear **velocity, angular velocity, forces, torque,** etc.

## Rigidbody interactions

### Weight

If the character is standing on top of a dynamic rigidbody this will automatically apply a force to it at the contact point, proportional to the rigidbody mass.

![](../../../.gitbook/assets/imagen%20%2860%29.png)

### Push

The character can push other dynamic rigidbodies by colliding with them. It is also possible to ignore some rigidbodies by using a dedicated layermask:

![](../../../.gitbook/assets/imagen%20%2861%29.png)



