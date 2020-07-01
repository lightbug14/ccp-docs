# Use a custom Input Handler

By default these are the available modes for human inputs:

* Unity's Input Manager \(old\)
* UI
* Custom

If you want to include a particular input system solution, you need to implement a custom input handler. This is something really easy to do:

1. Create a custom class that derives from the _InputHandler_ abstract class.
2. Implement the abstract methods
3. Add the component created soemwhere in the scene
4. Drag & drop the component into the input handler \(CharacterBrain\).

## Creating the class

Plain and simple C\#.

```csharp
public class CustomInputHandler : InputHandler
{
		public override bool GetBool( string actionName )
		{
				return SomeInputSystem.GetButton( actionName );
		}
		
		public override float GetFloat( string actionName )
		{
				return SomeInputSystem.GetAxis( actionName );	
		}
		
		public override Vector2 GetVector2( string actionName )
		{
				return SomeInputSystem.GetVector2( actionName );	
		}
}
```

As you can see, each abstract method needs to return the value, based on the input system used.

This is the default _UnityInputHandler_ \(Unity's Input Manager\) that comes with the asset.

```csharp
public class UnityInputHandler : InputHandler
{
		public override bool GetBool( string actionName )
		{
				return Input.GetButton( actionName );
		}
		
		public override float GetFloat( string actionName )
		{
				return Input.GetAxis( actionName );		
		}
		
		public override Vector2 GetVector2( string actionName )
		{
				// Not officially supported	
			  return new Vector2( Input.GetAxis( actionName + " X" ) , 	Input.GetAxis( actionName + " Y" ) );	
		}
}
```





