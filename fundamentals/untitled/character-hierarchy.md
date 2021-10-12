# Character

## Hierarchy

The core components associated with the character controller do not require to be organized in a very specific way, although it is recommended to follow the following (very simple and functional) structure:

![](<../../.gitbook/assets/imagen (78).png>)

|                      |                                                                                                                                                                                                                                                                 |
| -------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Character            | This object represents the physics of the character (collider and rigidbody). This object will also have two very important components, the CharacterBody and the CharacterActor, **these components will provide a Rigidbody and Collider component for you**. |
| Graphics             | This is an object in between the main physics object (Character) and the animated character (e.g. Animator). It becomes very useful when there is a need to modify the graphics (and model) without affecting the character (parent).                           |
| Animated mesh/sprite | Here, under "Graphics" is where you should put the character visual elements, such as 3D meshes, humanoids, sprites, etc.                                                                                                                                       |

All the demo characters follow this hierarchy, there are even graphics-related component that were designed with this structure in mind (e.g. CharacterGraphicsRootController needs to be applied to "Graphics").

## Components

Based on the hierarchy from before, we can say the "Core" is divided into two parts:

1. Character components.
2. Graphics components.

### Character components

These components are **mandatory**! There are two main components:

|                |                                                                                                                                       |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| CharacterBody  | This component represents the body of the character. It takes care of the Collider and Rigidbody component.                           |
| CharacterActor | This components handles all the interactions of the character with the environment. This is considered as the "Character Controller". |

### Graphics components

These components are much more focused towards an specific task (not as complex as the CharacterActor) and most of them are optional. The most important (and usually one component you'll always want to add to your character) is the **CharacterGraphicsRootController**. It is called "root" controller because it is supposed to be applied to the root of all graphic objects, in this case the "Graphics" object (see the hierarchy).
