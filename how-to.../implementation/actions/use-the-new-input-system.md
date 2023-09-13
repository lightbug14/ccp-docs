# Use the new input system

## Input handler

As mentioned in previous sections, an input handler must be created specifically for Unity's new input system. The following code shows one way to do it.

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



{% hint style="warning" %}
It is **recommended** to put the class file **outside CCP's main folder** in order to prevent missing reference errors. This happens because CCP's [asmdef file](../../../package/using-the-package.md#assembly-definition-file) does not include references to any external packages such as Unity's input system, Cinemachine, etc.
{% endhint %}

## InputAction assets

Keep in mind that the _InputActionAsset_ action names must match with the character actions names, otherwise actions will not be registered by the input handler. For example:

![](<../../../.gitbook/assets/imagen (88).png>)

## Downloads

{% file src="../../../.gitbook/assets/ccp-input-system-files.rar" %}

This file includes:&#x20;

* _InputSystemHandler.cs (code)_
* _CharacterActions.inputactions_
* _CameraActions.inputactions_

