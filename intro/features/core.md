# Core

### Dynamic rigidbody based

The character controller is Dynamic by nature, this means that the character uses a collider and a dynamic rigidbody to detect collisions and to do movement. However, almost all of its actions are predicted/calculated in a "kinematic way". This was intended that way in order to combine the best of both worlds, that is, the preciseness of a kinematic character and the collision detection/rigidbodies interaction of a dynamic character.

### Capsule body \(upright\)

The character is modelled as a 2D/3D upright capsule.

### **2D and 3D Physics**

This package supports 2D and 3D Physics, meaning that your character will detect and interact with 2D and 3D Colliders as well.

### **2D and 3D Movement**

Every component available in the package was created with 2D/3D movement in mind. No behaviour is specific neither to 2D nor 3D space.

### **Rigidbodies interaction**

Since the character is dynamic it can interact with other rigidbodies, push them, get pushed by them, and gather information from the interaction.

### **Technical level**

This character controller not only gives you good results, but also technical information about the world the character is interacting with.

### Step handling

The character can climb steps, no matter its height.

### Slope handling

It can handle steep slopes without problem. Also a _slopeLimit_ can be set to forbig certain slopes.

### Size handling

Change the size of the character without worrying about if it fit or not.

### Moving/Rotating platforms

The character will follow any _dynamic ground_ \(a.k.a _platform_\) movement and rotation properly. Of course without using object parenting 😱.

### Collision information

Use the character collision info to generate your custom behaviour \(ground normal, slope angle, edge detection, wall angle, and more.\)

### Collision events

Add listeners to any character event and do whatever you want with it.

### Orientation free

All the features work perfectly regardless the rotation value.

  


