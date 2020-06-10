# Hierarchy

Referring back to the [Character graphics](../../../fundamentals/untitled/character-graphics.md) section, this is the recommended hierarchy structure for any CCP character:

![](../../../.gitbook/assets/character_hierarchy.png)

By looking at the _Capsule Blank Character_, we can see the following hierarchy:

![](../../../.gitbook/assets/imagen%20%2846%29.png)

The _Graphics_ has the CharacterGraphics component \(as it should, because this will be the root of every graphics related content\). Then we have the _Capsule_ object with its child, both of these represents the Capsule mesh and the arrow mesh on top.

Since we aren't gonna need these objects anymore we can delete them.

![](../../../.gitbook/assets/imagen%20%2822%29.png)

Finally, just drag the _Demo Character_ model \(in your case your custom model\) into the _Graphics_ object

![](../../../.gitbook/assets/imagen%20%2839%29.png)

The hierarchy part is done. Notice that the Animator component has been added to the _Demo Character_ game object \(this is because of the Rig settings\).

![](../../../.gitbook/assets/imagen%20%2845%29.png)

{% hint style="info" %}
This may sound a little obvious, remember to modify the body size \(_CharacterBody_\) until the body fits exactly like you want with the mesh. You can do this at any time.
{% endhint %}

