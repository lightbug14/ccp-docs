# Use the new input system

## Input handler

### Code

This is an implementation of Unity's "new" input system

{% hint style="info" %}
Note that this is better implementation compared to the previous one \(from version 1.3.5\). This version brings some extra features and improvements.

* Actions are **stored inside a container** and read from there when needed \(better for performance\).
* Actions can be filtered by **action map** \(optional\).
* Binds can be filtered by **control scheme** \(optional\).
{% endhint %}

```csharp
using System.Collections;
using System.Collections.Generic;
using System.Linq;
using UnityEngine;
using UnityEngine.InputSystem;
using UnityEngine.InputSystem.Utilities;
using Lightbug.CharacterControllerPro.Implementation;


public class InputSystemHandler : InputHandler
{
    [SerializeField]
    InputActionAsset inputActionsAsset = null;

    [SerializeField]
    bool filterByActionMap = false;

    [SerializeField]
    string gameplayActionMap = "Gameplay";

    [SerializeField]
    bool filterByControlScheme = false;

    [SerializeField]
    string controlSchemeName = "Keyboard Mouse";


    Dictionary< string , InputAction> inputActionsDictionary = new Dictionary<string, InputAction>();

    protected virtual void Awake()
    {
        
        if( inputActionsAsset == null )
        {
            Debug.Log("No input actions asset found!");
            return;
        }

        inputActionsAsset.Enable();

        if( filterByControlScheme )
        {
            string bindingGroup = inputActionsAsset.controlSchemes.First( x => x.name == controlSchemeName ).bindingGroup;
            inputActionsAsset.bindingMask = InputBinding.MaskByGroup( bindingGroup );
        }

        ReadOnlyArray<InputAction> rawInputActions = new ReadOnlyArray<InputAction>();
        
        if( filterByActionMap )
        {
            rawInputActions = inputActionsAsset.FindActionMap( gameplayActionMap ).actions;

            for( int i = 0 ; i < rawInputActions.Count ; i++ )
                inputActionsDictionary.Add( rawInputActions[i].name , rawInputActions[i] );
        
        }
        else
        {
            for( int i = 0 ; i < inputActionsAsset.actionMaps.Count ; i++ )
            {
                InputActionMap actionMap = inputActionsAsset.actionMaps[i];

                for( int j = 0 ; j < actionMap.actions.Count ; j++ )
                {
                    InputAction action = actionMap.actions[j];
                    inputActionsDictionary.Add( action.name , action );
                }

            }

            
        }
        

        for( int i = 0 ; i < rawInputActions.Count ; i++ )
        {
            inputActionsDictionary.Add( rawInputActions[i].name , rawInputActions[i] );
        }

    }

    public override bool GetBool( string actionName )
    { 
        InputAction inputAction;

        if( !inputActionsDictionary.TryGetValue( actionName , out inputAction ) )
            return false;

        return inputActionsDictionary[actionName].ReadValue<float>() >= InputSystem.settings.defaultButtonPressPoint;
    }

    public override float GetFloat( string actionName )
    {       
        InputAction inputAction;

        if( !inputActionsDictionary.TryGetValue( actionName , out inputAction ) )
            return 0f;
        
        return inputAction.ReadValue<float>();
    }

    

    public override Vector2 GetVector2( string actionName )
    {
        InputAction inputAction;

        if( !inputActionsDictionary.TryGetValue( actionName , out inputAction ) )
            return Vector2.zero;
        
        return inputActionsDictionary[actionName].ReadValue<Vector2>(); 
    }

}


```

### Missing references \(asmdef file\)

There is a chance that after adding this class to your project you will get some compile errors. This is happening because the file \(containing the code\) is located inside CCP's main folder. CCP's asmdef file \(read [this section](../../package/using-the-package.md#assembly-definition-file)\) does not include references to any external packages \(Unity's input system, Cinemachine, etc.\), this is why you need to either:

1. Put the input handler file **outside CCP's main folder** \(e.g. _"Assets/YourStuff/InputSystemHandler.cs"_\) ... or
2. Add to CCP's asmdef file a reference to the new input system package.

## InputAction assets

Remember that the _InputActionAsset_ asset must have the same character actions names. For example:

![](../../.gitbook/assets/imagen%20%2866%29.png)

Here you can download all the input action assets required by the demo:

{% file src="../../.gitbook/assets/characteractions.rar" %}

{% file src="../../.gitbook/assets/cameraactions.rar" %}



