# Creating a basic character

## 1. The Gameobject

Add a new GameObject in the scene and give it a name. Let's call it "Character".

#### Position 

Whatever value you want

#### Rotation 

Any value will do. However, please use $$<0,0,0>$$\(reset value\).

#### Scale

As mentioned in the fundamentals section, we **must** use a local scale = $$<1,1,1>$$.

## 2. CharacterBody

Add a character body component to the character:

![](../../.gitbook/assets/imagen%20%2813%29.png)

Set the parameters you want, really simple.

## 3. CharacterActor

Next, add a CharacterActor component.

{% hint style="info" %}
By adding a _CharacterActor_ component a _CharacterBody_ component will be added automatically if there is not one yet. This is because the _CharacterActor_ requires a _CharacterBody_ component.
{% endhint %}

![](../../.gitbook/assets/imagen%20%284%29.png)

{% hint style="warning" %}
Make sure to add a _TagsAndLayers_ profile to the character. Otherwise nothing is going t work
{% endhint %}

![](../../.gitbook/assets/imagen%20%2828%29.png)

{% hint style="success" %}
Done! 😃 This is the more boring basic character you can create, It does absolutely nothing. In order to give it some life we need to create a "controller" on top \(it's just a script with a cool name\).
{% endhint %}

{% hint style="info" %}
Another way is to simply add a prefab to the scene \(basically the same we did in this section\). Use the basic "Capsule Blank Character". 

This character includes a **graphics element** which allows you to actually see the character in the game view \(with the forward direction represented with an arrow\).
{% endhint %}



