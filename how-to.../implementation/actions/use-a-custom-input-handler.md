# Use a custom Input Handler

The brain offers three human input modes:

* Unity's Input Manager (old)
* UI
* Custom

The `custom` mode, as the name implies, allows you to use a custom input handler. For this, you will need to:

1. Create a custom class that derives from the _InputHandler_ abstract class.
2. Implement its abstract methods using the input system API.
3. Add the component created (1.) somewhere in the scene.
4. Go to CharacterBrain and change the Human input type to "Custom".
5. Drag & drop the input handler component (3.) into the input handler field (CharacterBrain).

## Creating the class

Plain and simple C#.

{% code fullWidth="false" %}
```csharp
public class CustomInputHandler : InputHandler
{
		public override bool GetBool(string actionName)
		{
				return SomeInputSystem.GetButton(actionName);
		}
		
		public override float GetFloat(string actionName)
		{
				return SomeInputSystem.GetAxis(actionName);	
		}

		public override Vector2 GetVector2(string actionName)
		{
				return SomeInputSystem.GetVector2(actionName);	
		}
}
```
{% endcode %}

For example, this is the default _UnityInputHandler_ (Unity's Input Manager) that comes with the asset.&#x20;

```csharp
public class UnityInputHandler : InputHandler
{
		public override bool GetBool(string actionName)
		{
				return Input.GetButton(actionName);
		}
		
		public override float GetFloat(string actionName)
		{
				return Input.GetAxis(actionName);		
		}
		
		public override Vector2 GetVector2(string actionName)
		{
				// Not officially supported by Unity	
  				return new Vector2( 
  						Input.GetAxis( actionName + " X" ) ,
  						Input.GetAxis( actionName + " Y" ) 
  				);	
		}
}
```



