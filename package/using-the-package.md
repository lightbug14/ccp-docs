# Using the package

## Directory

The recommended way to use this package \(and every package out there, really\) is by working on a separated path \(outside the _Character Controller Pro_ folder\). 

![](../.gitbook/assets/imagen%20%2822%29%20%281%29.png)

This is useful if you need to use and/or extend the asset in any way.

## Namespaces

Every part of this package is separated into namespaces. This is to prevent collisions between names.

All my assets are contained within the `Lightbug` namespace. In this case:

|  |  |
| :--- | :--- |
| Lightbug.CharacterControllerPro | The main "root namespace" for this asset. |
| Lightbug.CharacterControllerPro.Core | The _core_ code is hosted here \(character actor, body, graphics, etc.\). |
| Lightbug.CharacterControllerPro.Implementation | The _implementation_ code is hosted here \(state machine, state, actions, brain,platforms, etc.\). |
| Lightbug.CharacterControllerPro.Demo | The demo code is hosted here \(specific character states, demo scenes, menus, fps counters, etc. \). |
| Lightbug.Utilities | Here you will find all the utilities static methods and extensions i use. Some of them may be useful for your own projects. There are engine and editor utilities as well. |

## API

In simpler words, the API is the only interface between CCP internal code and you. Think of CCP as a black box with many buttons that don't mean anything at first. You need to press those buttons but you don't have any idea what they do 😰. Luckily for you there is an online **API reference** \(doxygen\).

![](../.gitbook/assets/imagen%20%2817%29%20%281%29.png)

## Assembly definition file

The entire asset is self-contained inside an assembly definition file \(_.asmdef_\). For more information about assembly definition files please check [Unity's documentation](https://docs.unity3d.com/2019.1/Documentation/Manual/ScriptCompilationAssemblyDefinitionFiles.html).

![](../.gitbook/assets/imagen%20%2868%29.png)



One very important thing to consider is that the asset \(internally\) does not interact with external scripts \(e.g. your custom scripts\). **If you are using a custom assembly definition file**, and you need to reference Character Controller Pro, just indicate the reference as shown in the following image:

![](../.gitbook/assets/imagen%20%2867%29.png)



