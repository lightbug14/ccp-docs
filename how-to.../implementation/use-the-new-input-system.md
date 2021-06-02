# Use the new input system

## Input handler

### Code

This is a simple implementation of the Unity's "new" input system:

```csharp
using UnityEngine;
using UnityEngine.InputSystem;
using Lightbug.CharacterControllerPro.Implementation;

public class NewInputSystemHandler : InputHandler
{
    [SerializeField]
    InputActionAsset characterActionsAsset = null;

    void Awake()
    {
        characterActionsAsset.Enable();
    }

    public override float GetFloat( string actionName )
    {       
        return characterActionsAsset.FindAction( actionName ).ReadValue<float>();     
    }

    public override bool GetBool( string actionName )
    { 
        return characterActionsAsset.FindAction( actionName ).ReadValue<float>() >= InputSystem.settings.defaultButtonPressPoint;  
    }

    public override Vector2 GetVector2( string actionName )
    {
        return characterActionsAsset.FindAction( actionName ).ReadValue<Vector2>(); 
    }
    
}
```

### Missing references \(asmdef file\)

So, after importing creating the class Unity is not able to compile your project, it seems there are some missing references associated with the new input system package 🤔 . 

This is happening because the file \(containing the code\) is located inside CCP's main folder. CCP's asmdef file \(read [this section](../../package/using-the-package.md#assembly-definition-file)\) does not include a reference to external packages \(Unity's input system, Cinemachine, etc.\), this is why you need to either:

1. Put the input handler file outside CCP's main folder \(e.g. _"Assets/YourStuff/InputSystemHandler.cs"_\) ... or
2. Add to CCP's asmdef file a reference to the new input system package.

## InputAction assets

Remember that the _InputActionAsset_ asset must have the same character actions names. For example:

![](../../.gitbook/assets/imagen%20%2866%29.png)

Here you can download all the input action assets required by the demo:

{% file src="../../.gitbook/assets/characteractions.rar" %}

{% file src="../../.gitbook/assets/cameraactions.rar" %}



