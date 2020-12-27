# Create a basic character

Putting a character inside the scene can be achieved by:

1. Creating a character from zero \(starting from an empty object\)...or
2. Instantiating a prefab. 

## Creating the character

### 1. The character Gameobject

Add a new GameObject in the scene and give it a name. Make sure its local scale is$$<1,1,1>$$.

### 2. Add the components

A character consist of two important components:

1. CharacterBody
2. CharacterActor

![](../../.gitbook/assets/imagen%20%283%29.png)

{% hint style="info" %}
There is no need to add a **Collider** and/or **Rigidbody** to the object. The CharacterBody and CharacterActor will do this for you \(**ColliderComponent** and **RigidbodyComponent** components will be added in Awake\).
{% endhint %}

{% hint style="success" %}
Done! 😃 

This is the more boring invisble character you can create, **it does absolutely nothing**. In order to give it some life you need to implement some logic in another component.
{% endhint %}

### 3. Setting up the components

Finally, you need to configure these two components \(body and actor\) in order to customize your character. These components contain tooltips, please read them if you want to know in more depth what their fields do.

## Using a prefab

Another way is to simply add a prefab into the scene. You can use the basic "Blank Character" \(invisible\) or the "Capsule Blank Character" \(using a Capsule 3D Mesh\).

![&quot;Capsule Blank Character&quot; pregab](../../.gitbook/assets/imagen%20%2825%29.png)

