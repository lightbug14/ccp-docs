# Change the size of the character

As mentioned in the [Character body](../../fundamentals/untitled/characterbody.md#scale) section, **the local scale of the character should be Vector3.one**. So, changing the local scale is not allowed.

The scale is represented directly by the character body size, so you need to modify the body size. To do this you can call `SetBodySize` from the CharacterActor.

```csharp
bool validSize = CharacterActor.SetBodySize( new Vector2( width , height ) );
```

The character will automatically check if the new size is valid or not (depending on the surrounding geometry).
