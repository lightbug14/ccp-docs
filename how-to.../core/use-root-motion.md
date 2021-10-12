# Use root motion

By using root motion you can switch from script-based movement to animation-based movement. For more information about what root motion is please visit [this link](https://docs.unrealengine.com/en-US/AnimatingObjects/SkeletalMeshAnimation/RootMotion/index.html).

Root motion can be enabled/disabled at any time by calling the _**useRootMotion **_property from the `CharacterActor` component.

```csharp
CharacterActor.UseRootMotion = true;
```

After doing that, the animator controller will determine the position and rotation of the character. 

{% hint style="info" %}
There is no "correct" way of doing movement, choose whatever approach fits your needs best.

For instance, NormalMovement offers a script-based movement (root motion disabled). LadderClimbing and LedgeHanging offer an animation-based movement approach (root motion enabled).
{% endhint %}
