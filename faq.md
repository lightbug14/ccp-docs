# FAQ

## What is "Character Controller Pro"?

Character Controller Pro \(CCP for short\) is a **2D & 3D Dynamic Character Controller** that allows you to handle the movement, rotation and size of your character \(among other things\) in a precise way.

## What is a Character Controller?

A character controller is a script \(or set of scripts\) that handles all of your character requierements \(being the movement the most obvious one\). Due to the vast variety of games out there, it is not possible to determine a unique general solution for everyone. CCP was \(and will be\) designed to work as a multi purpose character controller, trying to cover as much ground as possible.

## What type of character does CCP support?

Currently it only supports an **upright capsule** based character. This basically means that the vertical direction of the capsule will always be _transform.up_. 

## Can i used this asset with my 2D scenes as well?

Yes, CCP supports **2D and 3D Physics,** as well as **2D and 3D movement**.

## What do you mean by a "dynamic" character?

In the simulated physics world \(especially with Character Controllers\),  there are kinematic and dynamic rigidbodies \(each one having its own advantages and disadvantages\). CCP uses a dynamic approach to physics, this means that the character is built upon a dynamic rigidbody working with Unity's Physics. The movement is performed **by modifying the velocity of the rigidbody directly**.

## What type of games can i make with CCP?

Any game that requires a physics based capsule shaped character. A RTS game, a 2D platformer, a horror game, a first person shoter, etc.

## Why the package is divided in "Core" and "Implementation"?

The reason behind this decision is extensibility. **The full package is defined as Core + implementation**. The implementation is built upon the core, so, if you want to re-implement this part, or removing it for complete, you just need to delete one folder and you are good to go. It also serves as a good way to define the scope of each part.

## My character consists of a big alien spider that has a weird shape \(a composition of colliders\), each leg must be procedurally animated and should react to the environment in a particular way. Can this asset handle that?

It won't \(like 99.9% sure\). If that was the case this asset would be called "Super Alien Spider Controller Pro". This package is oriented to what most developers need, the capsule character being the most common case, vastly used for a humanoid character \(or whatever you want to put inside\).

## Can i get an older version of the package?

Yes! I keep a backup with all the released versions of CCP. For me to send you the required version **I will need your invoice number** first \(no exception\).

## I downloaded the last version of Unity, and your asset doesn't work. Could you please do something about it?

Of course! before you go and write a 1 star review please let me know about your specific problem \(include all the related errors/warnings in the message\). Unity is adding and deprecating stuff like crazy, if something doesn't work with the new stuff let me know about it and i will fix it. It will help you, me and others.

That said, I always test my assets on new **official versions** of the Unity editor, just to be 100% sure.

## So, Why should I consider to buy this asset?

There are a couple of reasons why, here are some:

* You require a capsule based character that mimics the good stuff from the Unity's Character Controller component, but also works in a Physics environment.
* You want to create characters for your 2D and/or 3D game and only pay for one unified asset \(otherwise you will probably have to buy two different assets with no connection between them whatsoever\).
* You need a character controller solution for your project but don't want to waste so much time and money in the process \(believe me, this type of asset requires time and research ... a programmer will charge you a lot for it\).
* You want a serious, always growing asset that will be maintained and supported for life.

## So, Why should I consider not to buy this asset?

If you have in mind a very specific character \(e.g. the alien spider\), or are you trying to experiment with the character physics in a strange/unique way to create you unique game \(maybe this is what you need, who knows\), in this case i can't guarantee this package is for you. **If you want to be 100% percent sure please contact with me, i will tell you honestly is this is for you or not.**

## Spanish is my primary language, not english, What can i do to contact with you?

Don't worry, spanish is also my primary language... En ese caso, por supuesto que puedes enviarme tus preguntas en español \(será más fácil para los dos\). Paralelo al hilo oficial \(creado en Unity Forums\), he creado un hilo en español acerca de CCP en el sitio [Unity Spain](http://www.unityspain.com/), una comunidad de habla hispana dedicada a Unity. Te recomiendo que te unas si deseas preguntarme algo por allí, o simplemente para participar en el foro.



