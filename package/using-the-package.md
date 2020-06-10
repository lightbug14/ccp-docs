# Using the package

## Directory

The recommended way to use this package \(and every package out there, really\) is by working on a separated path \(outside the _Character Controller Pro_ folder\). 

![](../.gitbook/assets/imagen%20%2822%29%20%281%29.png)

This is useful if you need to use and/or extend the asset in any way.

## Namespaces

Every part of this package is separated into namespaces. This is to prevent collision between names.

All my assets are contained within the `Lightbug` namespace. In this case:

|  |  |
| :--- | :--- |
| Lightbug.CharacterControllerPro | The main "root namespace" for this asset. |
| Lightbug.CharacterControllerPro.Core | All the _core_ code is hosted here \(character actor, kinematic actor, scene controller, etc\). |
| Lightbug.CharacterControllerPro.Implementation | All the _implementation_ code is hosted here \(state machine, states,brain,platforms,cameras, etc.\). |
| Lightbug.CharacterControllerPro.Demo | All the demo scripts are hosted here \(demo scenes, menus, fps counters, etc. \). |
| Lightbug.Utilities | Here you will find all the utilities static methods and extensions i use. Some of them may be useful for your own projects. There are engine and editor utilities as well. |

A little example in code. Let's say you want to get a reference to the _CharacterActor_ component:

```csharp
namespace YourCompany.YourCoolGame
{
    public class YourCoolScript : Monobehaviour
    {
        Lightbug.CharacterControllerPro.Core.CharacterActor characterActor = null;
        
    }
}
```

Or more commonly preferred:

```csharp
using Lightbug.CharacterControllerPro.Core;  //<-- Needed

namespace YourCompany.YourCoolGame
{
    public class YourCoolScript : Monobehaviour
    {
        CharacterActor characterActor = null;
        
    }
}
```

## API

In simpler words, the API is the only interface between CCP and you. Think of CCP as a black box with many buttons that don't mean anything at first. You need to press those buttons but you don't have any idea what they do. 😰 

Luckly for you there is an API reference in the package. Go to _CharacterControllerPro/Documentation and you will find it there._ 

The API reference is an **html reference** \(made with DoxyGen\). In order to open this documentation you need to open the `index.html` file.

![](../.gitbook/assets/imagen%20%2817%29%20%281%29.png)

### 

