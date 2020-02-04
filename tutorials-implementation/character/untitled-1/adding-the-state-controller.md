# Adding the state controller

As it was mentioned before in the "fundamentals" section of this documentation, the **state controller** is the main interface between the character _implementation_ and the _core_ side. 

The logic thing to do is to add this component to our blank character, so let's do it:

![](../../../.gitbook/assets/imagen%20%2830%29.png)

As you probably noticed, a _CharacterBrain_ component was added too. This is because the state controller requires a "brain" component to work. Later on we are going to see this in action \(ignore it for now\).

## Inspector parameters

### The starting state

By assigning a state to the _CurrentState_ field you can determine which state will be the **starting state.**

Of course, this state controller will not be very useful for us without states to work with. For now we can add some of the states that comes with the package \(later on we are going to create our own states\).

{% hint style="warning" %}
**For the sake of this section** we are going to add the _**NormalMovement**_ state, and use it as our current state.

In the next sections we will be using our custom states.
{% endhint %}

![](../../../.gitbook/assets/imagen%20%282%29.png)

### Materials

The state controller needs a _MaterialProperties_ asset in order to update some internal values frame by frame. CCP includes a default _MaterialProperties_ asset you can use if you want.

{% hint style="info" %}
You can define your own materials if you want.
{% endhint %}

In this case, let's use the default materials:

![](../../../.gitbook/assets/imagen%20%284%29.png)

### Movement reference

Make sure to check the [Character state controller](../../../fundamentals/implementation/character-state-controller.md#movement-reference) section to know more about the movement reference.

In this case, we are going to leave it like that, that is, we are going to use "World" as out movement reference.

## Result

if we hit the play button the character should move using the NormalMovement state behaviour.

Ok, let's remove that component and create our own! Go to the next section.

