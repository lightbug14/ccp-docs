# Use root motion

With root motion you can switch between animation-based movement and script-based movement.

Root motion can be enabled/disabled anytime by calling the _useRootMotion_ property from the _CharacterStateController_.

```csharp
CharacterStateController.UseRootMotion = true;
```

After that, the animator controller will determine the position and rotation of the character. 

{% hint style="info" %}
There is no "correct" way of doing movement, choose whatever approach fits your needs best.

For instance, the NormalMovement offers a script-based movement \(root motion disabled\). The LadderClimbing and LedgeHanging states offer an animation-based movement \(root motion enabled\).
{% endhint %}

