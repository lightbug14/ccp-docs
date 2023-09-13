# Create your own AI movement logic

When the character brain is set to AI, the actions stop being updated by the input handler (input devices). Now these actions **need to be defined by code**. This is what AI is all about, simulating a machine "pressing buttons".&#x20;

In order to set up an AI character from zero you need to:

1. **Change the brain mode to "AI"** in the _CharacterBrain_ component.
2. **Add an **_**CharacterAIBehaviour**_ component to the character (wherever you want).
3. **Assign the **_**CharacterAIBehaviour**_ to the _CharacterBrain_.

{% hint style="info" %}
Human and AI move around using the same components, there is no need to add a NavMeshAgent or something similar. Also you don't need a NavMesh for this to work, although you can use one if you want (see the AI Follow behaviour).
{% endhint %}

## The AI behaviour

The brain will use the character actions from the current AI behaviour. Basically this behaviour task is to define this action frame by frame, as simple as that.

To create an AI behaviour you need to derive your class from _CharacterAIBehaviour._&#x20;

```csharp
public class YourAIBehaviour : CharacterAIBehaviour
{
    // virtual (optional)
    public override void EnterBehaviour( float dt )
    {
    }
    
    // abstract (mandatory)
    public override void UpdateBehaviour( float dt )
    {
    }
    
    // virtual (optional)
    public override void ExitBehaviour( float dt )
    {
    }
}
```

From there you can create your own custom logic. For instance, to simulate the AI running forward:

```csharp
public class RunForwardBehaviour : CharacterAIBehaviour
{
        
    // abstract (mandatory)
    public override void UpdateBehaviour( float dt )
    {
            // Run is a Bool action (e.g. a button or a key)
            characterActions.run.value = true;
            
            // Movement is a Vector2 action (e.g. WASD)
            characterActions.movement.value = new Vector2( 0f , 1f );
    }
    
}
```

{% hint style="info" %}
You can check the character actions preview from the _CharacterBrain_ inspector.
{% endhint %}
