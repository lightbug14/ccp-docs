# Organize the character \(hierarchy\)

The main rule is: **CharacterBody and CharacterActor should always be in the root object \(the "character" object\).**

You can be creative with the rest of the components.

The demo characters use the following hierarchy:

![](../../.gitbook/assets/imagen%20%2837%29.png)

|  |  |
| :--- | :--- |
| Root | Contains _**CharacterBody**_ and _**CharacterActor**_ |
| Graphics | Contains the **visual elements** of the character, from sprites to animated 3D meshes. |
| States | Contains the _**CharacterStateController**_ and every _**CharacterState**_ related to the character |
| Actions | Contains the _**CharacterBrain**_ and all the _**AIBehaviours**_ \(AI characters\). |
| Environment | Contains the _**MaterialController**_ \(Used by some of the states included in the Demo\) |



