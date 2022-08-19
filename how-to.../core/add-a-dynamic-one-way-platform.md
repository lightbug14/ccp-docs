# Add a dynamic one way platform

The process is very similar as the one for static one way platforms. However, there are a few important things to consider:

## 1. Create a static one way platform

(follow [these instructions](add-a-static-one-way-platform.md)).

## 2. Add a Rigidbody

Add a Rigidbody (Rigidbody2D) component to the platform. One way platforms should be kinematic, **make sure to enable the isKinematic property**.

## 3. Add a DynamicOneWayPlatform component

This component is responsible for re-simulating the platform physics and detecting multiple characters (using a BoxCast). It will automatically detect the BoxCollider component (whether is 2D or 3D) and Rigidbody component (whether is 2D or 3D).

The component itself exposes a layer mask that should be used to filter the collision results. Make sure to specify all the layers with characters on them (or leave it like that, "Everything" is set by default).

Here's an example of a dynamic 3D one way platform (with no movement behaviour).

![](<../../.gitbook/assets/imagen (94).png>)

## 4. Make it move

Once you have everything set up, it is time to add the movement behaviour. You can choose whatever method you want, using a custom script, using CCP's platform behaviours (e.g. ActionBasedPlatform), etc.
