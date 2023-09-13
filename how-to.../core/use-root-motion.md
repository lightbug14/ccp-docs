# Use root motion

By using root motion you can switch from script-based movement to animation-based movement. For more information about what root motion is please visit [this link](https://docs.unrealengine.com/en-US/AnimatingObjects/SkeletalMeshAnimation/RootMotion/index.html).

Root motion can be enabled/disabled at any time by calling the _**useRootMotion**_ property from the `CharacterActor` component.

```csharp
CharacterActor.UseRootMotion = true;
```

![](<../../.gitbook/assets/image (1) (1) (1).png>)

In Addition, it is possible to tweak the way position and rotation get updated by root motion. For example, you can mix animation-based movement with script-based rotation.

Do you want to apply root motion for planar movement but at the same time use script-based vertical movement (e.g. gravity, jumping, etc)? No problem, choose the _Set Planar Velocity_ option from the _Root Motion Velocity Type_ field.



