# Character brain

The character brain is a component responsible to handle all the character actions. These actions can be triggered either from a human player or the AI.

All the available actions are predefined in a structure and updated by the _CharacterBrain_ component at runtime. This approach create a level of abstraction between the inputs \(GetKey, GetButton, etc.\) and the character actions themselves \(jump, move forward, etc.\).

![Representation of the Human, the AI and the brain.](../../.gitbook/assets/characterbrain.png)

To select one mode or the other simply click on the buttons in the inspector. It should look like this:

![Brain modes in the inspector.](../../.gitbook/assets/brainmodes.png)

## Action

An action is a set of data \(usually booleans and vectors\) that simulate buttons and axes actions.

## Brain types

### Human brain

Basically in a human brain the actions are updated using input devices \(keyboard, mouse, joystick, UI, etc\). Regardless of the input detection method used, all the actions must be previously defined using an _input data asset_ \(a ScriptableObject\).

In order to update these actions an _input handler_ is needed. This is a simple abstract component that needs to the implemented in order to process inputs. It has the most common input functionalities, such as _GetButton_, _GetButtonDown_, _GetButtonUp_ and _GetAxis_. Each input handler should implement these methods in its own way.

The package contains two default input handler components, one for the classic _Unity's Input Manager_ and another for the _Unity's UI_ system \(used in mobile\). Additionally it supports a custom input handler mode, useful if you want to create your own handler.

These modes can be selected in the brain using the _Human Input Type_ field.

![Available human input types.](../../.gitbook/assets/humaninputtype.png)

|  |  |
| :--- | :--- |
| Unity Input Manager | This input handler reads inputs from the Unity's Input manager. Make sure the actions names \(input data\) and the axes from the input manager match exactly. |
| UI\_Mobile | This input handler reads all the mobile inputs components in the scene. This components are assigned to the UI elements responsible for converting UI Events into input values. |
| Custom | A custom implementation of an input handler. |

### AI brain

In an AI brain the actions are determined by a script, based on the current behaviour type. There are two types of AI behaviours:

|  |  |
| :--- | :--- |
| Sequence behaviour | Set of predefined actions stored as a \textit{ScriptableObject}. Basically this behaviour tries to imitate a human player with scripted actions. The AI character will not be \`\`smart'' in any way. |
| Follow behaviour | This behaviour does a path calculation between the character an a target. **In order to use this behaviour a** _**NavMesh**_ **must be generated previously**. |

