# Use the new input system

## Input system actions vs Character actions?

This is probably one of the most asked questions about this asset. I totally love the new input system, it's a great system with many great things and improvements over the old one. Unfortunately the new system **cannot replace the CharacterActions completely** \(for now\). The reasons are:

1. It does not allow to change the actions values via code.
2. It does not allow to present and change the actions values using the iinspector.
3. In theory, "i" numbers of AI Characters should be handled by "i" different devices. Which becomes quite difficult to do.

So, instead of putting all the weight over the input system, it is best to use it as a custom input handler \(custom implementation\). The new input system can be adapted to the CCP actions system without significant problems. There are some clear disadvantages, though.

1. The actions are obtained using polling. This is not "bad" \(personally, i prefer this over events\) but you won't be able to use C\# events.
2. The actions are obtained through the InputActionAsset \(using FindAction\).

Other than that, you will enjoy all the good features of the new system. 

## Code

{% hint style="info" %}
At the moment the asset by itself does not include an input handler based on the new input system. This is due to packages dependence, since the new input system need to the downloaded and installed using the package manager.
{% endhint %}

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

Remember that the _InputActionAsset_ asset must have the same character actions names. For example:

![](../../.gitbook/assets/imagen%20%2854%29.png)

Here you can download some examples:

{% file src="../../.gitbook/assets/characteractions.rar" %}

{% file src="../../.gitbook/assets/cameraactions.rar" %}

