# Creating a Character Controller script

We are going to create and configure a really simple script where we are going to put all our code \(next sections\). This script is usually called a character controller \(or whatever you want to call it\).

## 1. The script

First of all let's create our script, we are going to call it "TutorialController". This 

```csharp
using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class TutorialController : MonoBehaviour
{    
}
```

## 2. Namespace and components

We need to include do some basic things first. These are:

1. Using the Core namespace
2. It would be nice to add a RequireComponent attribute, since we need a CharacterActor component to work with.
3. Add a CharacterActor field
4. Get the CharacterActor component in Awake

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{       
    CharacterActor characterActor = null;
     
    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
    }
    
}
```

## 3. The update methods

We will need to update the character actor one way or another. The question is, What update method you should use? Update? FixedUpdate? Another method? 

The answer is not clear, because again it depends. It's recommended to handle inputs in the Update method and modify the character properties in the FixedUpdate method. So, for this tutorial we are going to use both.

```csharp
using System.Collections; 
using System.Collections.Generic; 
using UnityEngine; 
using Lightbug.CharacterControllerPro.Core;

[RequireComponent( typeof( CharacterActor ) )] 
public class TutorialController : MonoBehaviour
{        
    CharacterActor characterActor = null;
    
    void Awake()
    {
        characterActor = GetComponent<CharacterActor>();
    } 
    
    void Update()
    {
        GetInputs();
    }
    
    void FixedUpdate()
    {
        UpdateCharacter();
    }
    
    void GetInputs()
    {        
    }
    
    void UpdateCharacter()
    {        
    }
    
    
    
}
```

Now we need to implement those methods. Now it would be good to define our vision. 

Let's say that we want our character to:

* Move in the right and forward direction axes \(positve and negative movement\).
* Rotate left and right.
* Be affected by gravity.
* Jump.
* Crouch.
* Teleport 10 meters \(high some key is pressed\).

The following sections will explain every item on this list one by one. But first, we need to get some inputs!











