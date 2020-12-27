# Size

Internally the size of the character is stored in a Vector2 variable called _BodySize_ \(similar to CharacterBody size\). 

$$width = BodySize.x$$ 

$$height= BodySize.y$$ 

The size **is lerped over time** \(it does not change immediately\).

![](../../../.gitbook/assets/imagen%20%2863%29.png)

This lerp function do a linear interpolation between the current size and the target size. The user can set this target size at any time using the CharacterActor **SetBodySize** method. Once this value is passed to the character, this will internally check for collisions \(doing an overlap\), if the test is valid, then the target size is applied.

