# Add logic to your character

The term "logic" refers to the way of modifying the character controller over time. This must be created from zero using a C\# script or similar \(e.g. using visual scripting\).

{% hint style="info" %}
The Demo content does implement custom logic for all the states availables.
{% endhint %}

## Reference to the CharacterActor

To create your own behaviour just create a script \(e.g. Monobehaviour\) and get a reference to the CharacterActor you want to implement:

```csharp
using UnityEngine;
using Lightbug.CharacterControllerPro.Core; //<-- Required

public class CharacterLogic: Monobehaviour
{
    [SerializeField]
    CharacterActor characterActor = null;
}

```

## Update message

The character actor will be updated during FixedUpdate, so you'll probably need to call FixedUpdate as well.

```csharp
using UnityEngine;
using Lightbug.CharacterControllerPro.Core; //<-- Required

public class CharacterLogic: Monobehaviour
{
    [SerializeField]
    CharacterActor characterActor = null;
    
    void FixedUpdate()
    {        
        // Put the logic here ...
    }
}
```

## Execution order

Last but not least, sometimes can be useful to execute your code before the actual CharacterActor code. This can be easily achieved in Unity by modifying the execution order settings, however, there is a easier way. Unity includes an attribute called **DefaultExecutionOrder** which defines an execution order by code \(very handy\). The order is represented by a integer.

The "Core" includes an **ExecutionOrder class,** which contains predefined order values used by some of the components from CCP. For example:

```csharp
//CharacterActorOrder = 10
[DefaultExecutionOrder( ExecutionOrder.CharacterActorOrder )]
public class CharacterActor : MonoBehaviour
{
    ...
}
```

So, you can include this to your script, just to make sure this is running before \(in this case\) the CharacterActor script.

```csharp
using UnityEngine;
using Lightbug.CharacterControllerPro.Core; //<-- Required

[DefaultExecutionOrder( ExecutionOrder.CharacterActorOrder - 1)]
public class CharacterLogic: Monobehaviour
{
    [SerializeField]
    CharacterActor characterActor = null;
    
    void FixedUpdate()
    {        
        // Put the logic here ...
    }
}
```

{% hint style="info" %}
By default the execution order of any new script is equal to 0. Basically this means that the script will still run before the CharacterActor, even without this attribute applied. Nonetheless, it is recommended to use it if we must be sure the order is executed correctly.
{% endhint %}

