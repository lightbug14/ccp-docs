# Character particles

The particles controller founded in the package is responsible for managing and triggering all the particles you see on screen, coming from the character. A particle prefab is specified as the main particle \(its parameters will be modified by the controller\).

All the particles are managed using a _ParticleSystem_ pooler. This is a class that manages the visibility or activation of the objects it contains in a smart way. This is used to avoid the runtime instantiation of the objects \(usually a prefab\), thus improving performance.

These particles are triggered in response to events. There are two types of events that the particles can listen to, animation events and _CharacterActor_ events.

## Footsteps

To show the footsteps particles effects the _CharacterParticles_ component uses animation events. This type of events are defined in the animation import settings. 

![Footsteps animation events \(import settings\).](../../.gitbook/assets/footsteps.png)

The advantage of using Animation events is that the event can be placed exactly at a certain time along the clip timeline.

In the script we can add a public method and the animation system will call this methods for us. It's super important that the method name and the field \textit{Function} from the animator settings match exactly. Otherwise the method will not be named at all.

\subsection{\textit{OnGroundedStateEnter} particles}

If the character hits the ground it will produces some particles, whose velocity will vary depending on the falling speed at the moment of impact. To make this effect a \textit{CharacterActor} event was used, this event was the \textit{OnGroundedStateEnter}. When this event is called the local vertical velocity is passed along as a parameter, which is great for this.

The magnitude obtained from the y component of the local vertical velocity is evaluated using a custom \textit{AnimationCurve} \(horizontal axis\). The output of this curve \(vertical axis\) is used as the \`\`start speed'' of the \textit{ParticleSystem} triggered.

