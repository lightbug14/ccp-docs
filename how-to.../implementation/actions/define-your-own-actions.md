# Define your own actions

Actions are part of the **CharacterActions C# structure** (_CharacterActions.cs_). In order to define your own actions, you would need to modify the structure internal fields in some way. **Luckily for you, there is no need to manually do that**. The recommended way to modify actions is by using a `CharacterActionsAsset `asset.

{% hint style="info" %}
Individual assets don't matter, they are just pure data containers. The whole creation process will end up affecting one C# structure.
{% endhint %}

## Creating a CharacterActionsAsset asset

1. Right click over the project view.
2. Go to: _Create/Character Controller Pro/Implementation/Inpus/Character Actions Asset._
3. Fill the lists with your data (name and type).
4. Click the "Create Actions" button.

At the end, the CharacterActions structure will be updated with your data.

## Default actions (Demo)

By default (after importing the asset), the character actions structure will contain the data used in the Demo (movement, jump, run, dash, etc). All the actions were created using the _Default Character Actions_ asset included with the package:

!["Default Character Actions" asset  ](<../../../.gitbook/assets/imagen (96).png>)

{% hint style="info" %}
If you don't want to start the process from scratch, then duplicate this asset (and put it outside CCP workspace). Once you have the copy, then you can start to add new actions (or remove existing ones) to your liking.
{% endhint %}

{% hint style="warning" %}
The Demo states use all the default actions from this asset file (jump, dash, run, and so on). This means that modifying these actions while using the demo content (e.g. NormalMovement) can end up causing compilation errors (depending on which action you remove).

Extending the default set of actions (by copy+pasting the default asset) is the safest way to work with actions.
{% endhint %}
