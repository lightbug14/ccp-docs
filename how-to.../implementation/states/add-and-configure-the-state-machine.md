# Add and configure the state machine

## CharacterStateController component

The main component of the state machine is the **CharacterStateController**. You'll need to add this component anywhere within the character hierarchy (read the [Organize the character hierarchy](../organize-the-character-hierarchy.md) section for more information).

![](<../../../.gitbook/assets/imagen (72).png>)

## Initial state

The state machine needs a **state** to work with, this is referred as the **current state** in the inspector. You'll need to add **at least one state** to the character, and assign that state as the _current state_ reference.

![](<../../../.gitbook/assets/imagen (75).png>)

## Movement reference

Set up the **movement reference** (see the [Character state controller](../../../fundamentals/implementation/character-state-controller.md#movement-reference) section).&#x20;

{% hint style="info" %}
If the character is going to follow a camera direction (common case) choose "External" and assign the camera as the _External Reference_.
{% endhint %}
