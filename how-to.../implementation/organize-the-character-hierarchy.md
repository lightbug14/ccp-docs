# Organize the character hierarchy

The main rule is: **CharacterBody and CharacterActor should always be in the root object (the "character" object).**

You can be creative with the rest of the components.

The demo characters use the following hierarchy:

![](<../../.gitbook/assets/imagen (63).png>)

|             |                                                                                                     |
| ----------- | --------------------------------------------------------------------------------------------------- |
| Root        | Contains _**CharacterBody **_and _**CharacterActor**_                                               |
| Graphics    | Contains the **visual elements **of the character, from sprites to animated 3D meshes.              |
| States      | Contains the _**CharacterStateController **_and every _**CharacterState **_related to the character |
| Actions     | Contains the _**CharacterBrain **_and all the _**AIBehaviours **_(AI characters).                   |
| Environment | Contains the _**MaterialController **_(used by some of the states included in the Demo)             |

