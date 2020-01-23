# Creating a basic character

## 1. The Gameobject

Add a new GameObject in the scene and give it a name. Let's call it "Character".

Choose its **position** and **rotation**.

#### Really? A tutorial about creating a GameObject? 🤔 

Yes! notice that we didn't modify the scale at all. This is because **we want the default local scale value =** $$<1,1,1>$$.

## 2. CharacterBody

Add a character body component to the character:

![](../../.gitbook/assets/imagen%20%287%29.png)

Set the parameters you want, really simple.

## 3. CharacterActor

Next, add a CharacterActor component.

{% hint style="info" %}
By adding a _CharacterActor_ component a _CharacterBody_ component will be added automatically if there is not one yet. This is because the _CharacterActor_ requires a _CharacterBody_ component.
{% endhint %}

![](../../.gitbook/assets/imagen%20%283%29.png)

{% hint style="warning" %}
Make sure to add a _TagsAndLayers_ profile to the character. Otherwise nothing is going t work
{% endhint %}

![](../../.gitbook/assets/imagen%20%2813%29.png)

Done! 😃 This is the more boring basic character you can create. It does absolutely nothing. In order to give it life go we need to create a "controller" on top \(it's just a script with a cool name\).



