# Change the size of the character

As mentioned in the [Character body](../../fundamentals/untitled/characterbody.md#scale) section, **the local scale of the character should be Vector3.one**. This means that **changing the local scale is not allowed** :red\_circle:. The body dimentions are represented directly by the character body size.&#x20;

In order to do modify the size (width or height) of the character you can use the following CharacterActor public method:

```csharp
// Sets the size directly without checking
CharacterActor.SetSize(size, sizeReferenceType);

// Check if the character fits
CharacterActor.CheckSize(position, size, in filter);
CharacterActor.CheckSize(size, in filter);
CharacterActor.CheckSize(size);

// Checks first, if the the result is valid then sets the size
CharacterActor.CheckAndSetSize(size);
CharacterActor.CheckAndSetSize(size, sizeReferenceType);
```

Sometimes you have to be able to smoothly change from one size value to another (e.g. while crouching/standing up). This can be achieved easily via interpolation (_Lerp_ in this case).

The actor can Check and interpolate size:

```csharp
CharacterActor.CheckAndInterpolateSize(targetSize, lerpFactor, sizeReferenceType);

// Only for height
CharacterActor.CheckAndInterpolateHeight(targetHeight, lerpFactor, sizeReferenceType);
```
