# Create a state

You can create your own state in two ways:

1. Deriving from the CharacterState class and implement its abstract methods.
2. Using the "Create" menu.

![](../../.gitbook/assets/imagen%20%2842%29.png)

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Lightbug.CharacterControllerPro.Implementation;


public class YourCustomState : CharacterState
{

    // Write your initialization code here
    protected override void Awake()
    {
        base.Awake();
    }

    // Write your transitions here
    public override void CheckExitTransition()
    {
	  }

    // Write your transitions here
	  public override bool CheckEnterTransition( CharacterState fromState )
    {
        return base.CheckEnterTransition( fromState );
	  }

    // Write your update code here
	  public override void UpdateBehaviour( float dt )
    {
        
	  }
    
    
}
```

From the inspector:

![](../../.gitbook/assets/imagen%20%2843%29.png)

