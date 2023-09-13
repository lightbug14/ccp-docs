# Character brain

`CharacterBrain` is a component responsible for handling all character actions, regardless of whether they come from the player or not.

![Representation of the Human, the AI and the brain.](../../.gitbook/assets/characterBrain.png)

If you are familiar with the Unity's "new" input system, you probably know what an action is. An **action** is just a link between an input signal (e.g. press the jump button) and an output result at the gameplay level (e.g. jump).

All the available actions are predefined in a structure and then updated by the _CharacterBrain_ component at runtime. This approach create a level of abstraction between the inputs (GetKey, GetButton, etc.) and the character actions themselves (jump, move forward, etc.).

## Actions

### Types

CCP's Implementation supports three types of actions

| Action type   | Description                                              |
| ------------- | -------------------------------------------------------- |
| BoolAction    | A toggle, this action can be pressed or not pressed.     |
| FloatAction   | A 1D Value from -1 to 1 (similar to `GetAxis`from Unity) |
| Vector2Action | A 2D Value from, basically a combination of two axis.    |

{% hint style="info" %}
Note that the BoolAction value is true or false (a bool). If you need to know if that action was "started" or "canceled" (e.g. was the jump button pressed?), you need to get the **Started** or **Canceled** property respectively.
{% endhint %}

### Character actions struct

These actions are predefined and grouped together inside a struct. Each public field represents a particular action.

```csharp
public struct CharacterActions 
{
	// Bool actions
	public BoolAction @jump;
	public BoolAction @run;
	public BoolAction @interact;
	public BoolAction @jetPack;
	public BoolAction @dash;
	public BoolAction @crouch;
    
  //...
}
```

{% hint style="info" %}
You can visualize the actions values in runtime in the inspector (Human or AI).
{% endhint %}

![](<../../.gitbook/assets/imagen (58).png>)

{% hint style="info" %}
CCP includes a _ScriptableObject_ asset whose only job is to modify this _CharacterAction_ struct. The actions included by default were generated using the **Default Character Actions** asset.
{% endhint %}

{% hint style="danger" %}
Have in mind that adding/removing actions might affect the scripts from the Demo content since these scripts are using the default CCP actions.
{% endhint %}

## Brain types

![Brain modes in the inspector.](../../.gitbook/assets/BrainModes.png)

### Human brain

If the brain is set to _Human_, actions will get updated based on input devices (keyboard, mouse, joystick, UI, etc). The component responsible for this is called `InputHandler`, and it must be implemented specifically for each input system needed.

By default, the brain allows the user to use two input handlers that come with the asset, or a custom one.

![Available human input types.](../../.gitbook/assets/humanInputType.png)

| Human input type    | Description                                                                                                                                                           |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unity Input Manager | It reads input data directly from Unity's Input manager (old system).                                                                                                 |
| UI\_Mobile          | It looks for all UI-based input components in the scene (`InputAxes` and `InputButton`). These components are responsible for converting UI events into input values. |
| Custom              | An `InputHandler` custom implementation.                                                                                                                              |

### AI brain

In this mode, the brain defines actions through code by using a `AIBehaviour`.&#x20;

![Example: AI behaviour using a sequence behaviour (Demo content).](<../../.gitbook/assets/imagen (57).png>)
