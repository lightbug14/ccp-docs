# Character state

## State behaviour

A state is the main piece of code that the state machine executes. Every state presents its own behaviour, and can be implemented through its abstracts and virtual methods. The state controller will call them when they are needed, so don't worry about the execution order \(see the API reference to know what methods are available\).

You need to override the method you want to define a specific behaviour. For instance, if you want to create your own exit behaviour you can do something like this:

```csharp
// YourCustomState.cs
public override void ExitBehaviour(float dt)
{
    // Your code ...
}
```

## State creation

If you want to create your own states you can do so manually by creating your own class. It's mandatory that it derives from the \textit{CharacterState} class.

Another way is by simply right clicking on the project view \(choose the path of your choice\), then go to \textit{\`\`Create/Character Controller Pro/Implementation/Character State''}. This will create a template with the basics already included.

### Transitions

This is an important concept to understand. A transition is evaluated in two places, in the "from state" and the "to state":

|  |  |
| :--- | :--- |
| From state | State where the transition originates. |
| To state | State where the transition ends. |

These transitions are called Exit transition and Enter transition.

|  |  |
| :--- | :--- |
| Exit transition | This is the part of the transition that is evaluated first, when trying to exit the current state \(hence its name\). |
| Enter transition | This is the part of the transition that is evaluated secondly, when trying to enter the next state \(hence its name\). |

#### Why do transitions using this approach? 

Well, sometimes the information needed to decide if a transition is successful or not is shared between two or more states, but sometimes it doesn't. Since we can't be sure that one state has the total control over one particular transition, dividing the condition test sounds like the right thing to do.

> ### Example
>
> Let's say you want to implement a transition to a _JetPack_ state.
>
> In the _Normal_ state, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever \(and it shouldn't\). For the _JetPack_ state is another story. 
>
> The _JetPack_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure that the fuel is enough.

\section{Character brain}

The character brain is a component responsible to handle all the character actions. These actions can be triggered either from a human player or the AI.

All the available actions are predefined in a structure and updated by the \`\`Brain'' component at runtime. This approach create a level of abstraction between the inputs \(GetKey, GetButton, etc.\) and the character actions themselves \(jump, move forward, etc.\). This is represented in figure \ref{fig:characterbrain}.

\begin{figure} \centering \includegraphics\[width=0.4\linewidth\]{Image/characterBrain} \caption{Representation of the Human, the AI and the brain.} \label{fig:characterbrain} \end{figure}

To select one mode or the other simply click on the buttons in the inspector. It should look like figure \ref{fig:BrainModes}.

\begin{figure} \centering \includegraphics\[width=0.8\linewidth\]{Image/BrainModes} \caption{Brain modes in the inspector.} \label{fig:BrainModes} \end{figure}

\subsection{Action}

An action is a set of data \(usually booleans and vectors\) that simulate buttons and axes actions.

\subsection{Human brain}

Basically in a human brain the actions are updated using input devices \(keyboard, mouse, joystick, UI, etc\). Regardless of the input detection method used, all the actions must be previously defined using an \textit{input data asset} \(a ScriptableObject\).

In order to update these actions an \textit{input handler} is needed. This is a simple abstract component that needs to the implemented. It has the basic input functionalities used, such as \textit{GetButton}, \textit{GetButtonDown}, \textit{GetButtonUp} and \textit{GetAxis}. Each input handler should implement these methods in its own way.

The package contains two default input handler components, one for the classic \textit{Unity's Input Manager} and another for the \textit{Unity's UI} system \(used in mobile\). Additionally it supports a custom input handler mode, useful if you want to create your own handler.

These modes can be selected in the brain using the \textit{Human Input Type} field.

\begin{figure} \centering \includegraphics\[width=0.7\linewidth\]{Image/humanInputType.png} \caption{Available human input types.} \label{fig:humanInputType} \end{figure}

\parbox{0.9\linewidth} { \paragraph{ Unity Input Manager } This input handler reads inputs from the Unity's Input manager. Make sure the actions names \(input data\) and the axes from the input manager match exactly. }

\parbox{0.9\linewidth} { \paragraph{ UI\_Mobile } This input handler reads all the mobile inputs components in the scene. This components are assigned to the UI elements responsible for converting UI Events into input values. }

\parbox{0.9\linewidth} { \paragraph{ Custom } A custom implementation of an input handler. }

\subsection{AI brain}

In an AI brain the actions are determined by a script, based on the current behaviour type. There are two types of AI behaviours:

\parbox{0.9\linewidth} { \subsubsection{ Sequence behaviour } Set of predefined actions stored as a \textit{ScriptableObject}. Basically this behaviour tries to imitate a human player with scripted actions. The AI character will not be \`\`smart'' in any way.

```text
\subsubsection{ Follow behaviour }
This behaviour does a path calculation between the character an a target. In order to use this behaviour a \textit{NavMesh} must be generated previously.
```

}

\section{Character animation}

A simple animation component that triggers animation clips based on the \textit{CharacterActor} state. It's compatible with the `Animator'' controller, but it can be extended to other systems (for example the`Legacy'' animation system\) by deriving from this component class.

This component is probably the one that you will want to fully customize, since there is not a correct animation scheme or tool for the job. The package might include more tools in the future.

\subsection{Blend trees}

Blend trees allow us to blend between animation clips, simple as that. This is used in this implementation in two cases. The first one is when the character grounded and stable. The second one is when the character is not grounded.

If you open the Animator controller included in the package, you will see something similar to figure \ref{fig:animator}. \textit{NotGrounded} and \textit{Grounded} are blend trees, the rest are simple \textit{Animator} states with one clip in it.

\begin{figure} \centering \includegraphics\[width=0.9\linewidth\]{Image/Animator} \caption{Character animator controller \(base layer\).} \label{fig:animator} \end{figure}

A blend tree reads a specific variable to decide which clip of the tree it should play. This variable is fed to the blend tree by the \textit{CharacterAnimation} component. Its name can be modified in the inspector.

For instance, in the \textit{Grounded} blend tree the variable passed through is the current velocity magnitude. In figure \ref{fig:blendTree} the blend tree structure is shown. We can see there are three clips in it: \textit{Idle}, \textit{Walk} and \textit{Run}. The result will depend on the variable value, and the chosen threshold values as well.

\begin{figure} \centering \includegraphics\[width=0.9\linewidth\]{Image/blendTree} \caption{\textit{Grounded} blend tree.} \label{fig:blendTree} \end{figure}

\subsection{IK foot placement}

Although the character included with the package is not perfectly suited to work with IK foot placement \(due to its proportions and the fact that it wasn't design for this task very well\), the \textit{CharacterAnimation} offers some basic functionality in this regard.

\begin{figure} \centering \includegraphics\[width=0.7\linewidth\]{Image/IK} \caption{The demo character using IK foot placement.} \label{fig:ik} \end{figure}

To make a character work with IK you'll need to:

\begin{enumerate}

```text
\item Import an animated model using the \textit{Humanoid} rig.

\item Configure its avatar (choose the left and right foot)

\item Configure the weight curves in the animated model (1 is full weight, 0 is no weight). Make sure the curves names match with the weight curves names from the \textit{CharacterAnimation} component

\item Activate the \textit{IK pass} in the Animator layer settings.

\item Activate the \textit{IK Foot Placement} toggle in the \textit{CharacterAnimation} component.    
```

\end{enumerate}

The IK function will cast a sphere towards the ground \(for each foot\) to determine where the foot needs to be placed at. It will also take into account the rotation as well, so the foot will be correctly rotated using the hit normal.

\section{Character particles}

The particles controller founded in the package is responsible for managing and triggering all the particles you see on screen, coming from the character. A particle prefab is specified as the main particle \(its parameters will be modified by the controller\).

All the particles are managed using a \textit{ParticleSystem} pooler\footnote{A class that manages the visibility or activation of the objects it contains in a smart way. This is used to avoid the runtime instantiation of the objects \(usually a prefab\), thus improving performance.}.

These particles are triggered in response to events. There are two types of events that the particles can listen to, animation events and \textit{CharacterActor} events.

\subsection{Footsteps}

For footstep animation events \(defined in the animation import settings\) are used, this is because they can be placed exactly at a certain time along the clip timeline. Figure \ref{fig:footsteps} shows two animation events, for the \textit{Walk} animation clip.

In the script we can add a public method and the animation system will call this methods for us. It's super important that the method name and the field \textit{Function} from the animator settings match exactly. Otherwise the method will not be named at all.

\begin{figure} \centering \includegraphics\[width=0.7\linewidth\]{Image/footsteps} \caption{Footsteps animation events \(import settings\).} \label{fig:footsteps} \end{figure}

\subsection{\textit{OnGroundedStateEnter} particles}

If the character hits the ground it will produces some particles, whose velocity will vary depending on the falling speed at the moment of impact. To make this effect a \textit{CharacterActor} event was used, this event was the \textit{OnGroundedStateEnter}. When this event is called the local vertical velocity is passed along as a parameter, which is great for this.

The magnitude obtained from the y component of the local vertical velocity is evaluated using a custom \textit{AnimationCurve} \(horizontal axis\). The output of this curve \(vertical axis\) is used as the \`\`start speed'' of the \textit{ParticleSystem} triggered.

\section{Kinematic actors}

Just like character actors, a kinematic actor is another fundamental part of the scene. These objects can be platforms or cameras.

\section{Kinematic platforms}

The package includes components that allow to script the movement of a platform in a particular way \(depending on the component\).

All the moving/rotating platforms components are child classes from the \textit{KinematicPlatform} class. Currently there are two types of kinematic platforms:

\parbox{0.9\linewidth} { \paragraph{ Node Based } These platforms movement and rotation are purely based on nodes. Use this component to create platforms that moves and rotate precisely following a predefined path. }

\parbox{0.9\linewidth} { \paragraph{ Action Based } These platforms movement and rotation are defined by a single action for movement and rotation. Use this component if you want to create platforms with a pendulous nature, or infinite duration actions \(for instance, if the platform should rotate forever\). }

\parbox{0.9\linewidth} { \paragraph{ Animated } These platforms are completely handled by an external component, for example an animation clip \(using the Animate Physics mode\).\ }

\section{Kinematic cameras}

A kinematic camera is just a classic camera \(using the \textit{Camera} component\) that's being moved and rotated by the physics engine \(\textit{Rigidbody} or \textit{Rigidbody2D} component\).

This implementation comes with two kinematic cameras, a \textit{KinematicCamera2D} and a \textit{KinematicCamera3D}.

\subsection{Kinematic Camera 2D}

This camera behaves like a classic 2D platformer camera. Basically it moves along the XY plane following a character. The camera 2D:

\begin{itemize}

```text
\item Works fine with any orientation.

\item Can do interpolated movement (position and rotation).

\item Moves based on predefined bounds (AABB\footnote{Axis Aligned Bounding Box.}). If the character goes beyond the bounds the camera will move).

\item Moves based on a single reference point.

\item Look ahead, predicting the horizontal and vertical movement.
```

\end{itemize}

\subsection{Kinematic Camera 3D}

This camera behaves like a classic third person camera. Basically it orbits around a character. It can:

\begin{itemize} \item Do yaw motion \(it can be disabled\).

```text
\item Do pitch motion (it can be disabled).

\item Zoom in and out using the mouse scroll wheel.

\item Detect any geometry as an obstacle (via LayerMask).

\item Works fine with any orientation.

\item Do interpolated movement (position and rotation).
```

\end{itemize}

%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%% %%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%

\section{Example : \textit{NormalMovement} state}

It is not necessary to create many states and transitions between them for creating a good playable character \(the \textit{NormalMovement} state is a good example of this\). The \textit{NormalMovement} state was created as a multi purpose state, it is responsible for basic grounded and not movement, gravity, walking and running, crouching, jumping, and so on.

This section is explained as a mini tutorial, basically justifying why was the \textit{NormalMovement} state created that way. So you can extend from it, create your own version of it, or simply know more about the process behind.

If you want to know more in detail about this state please see the \textit{\`\`NormalMovement.cs''} script.

\subsection{State controller}

Since this is a state we must derive from the \textit{CharacterState} class, implementing its abstract and virtual methods to define the behaviour we want \(the same way you implement Unity's messages, like Start, Update, FixedUpdate, etc\).

\subsection{Basic state structure}

In our vision we want to make the character move around and crouch, so we need to set its linear velocity and size properly to fit our needs. This need to be done in a frame by frame basis, so we proceed to write the update behaviour like this:

\begin{minipage}{\linewidth} \begin{lstlisting} public override void UpdateBehaviour\( float dt \) { HandleSize\( dt \); HandleMovement\( dt \); } \end{lstlisting} \end{minipage}

\textit{HandleSize} and \textit{HandleMovement} will handle the size and movement respectively. The parameter \`\`dt'' is equals to \textit{Time.deltaTime}.

\subsection{Input handling}

The more elemental thing to do is to read brain actions from the character \(human or AI\). This is accomplished by reading the \textit{CharacterAction} struct directly.

For example to check if the \textit{Jump} action was initiated \(button pressed down\):

\noindent \begin{minipage}{\linewidth}

\begin{lstlisting} if\( characterBrain.CharacterAction.jumpPressed \) { // Define the jump velocity vector ... }

\end{lstlisting} \end{minipage}

\subsection{Size handling}

Regarding the size, the only dimension that matters \(in this case\) is the height, so we define the \textit{targetHeight} and implement the \textit{HandleSize} method. Inside this method a targetSize is defined and passed to the \textit{SetTargetBodySize} method.

\noindent \begin{minipage}{\linewidth} \begin{lstlisting} void HandleSize\( float dt \) {  
// Define the targetHeight...

```text
Vector3 targetSize = new Vector2( CharacterActor.DefaultBodySize.x , targetHeight );

CharacterActor.SetTargetBodySize( targetSize );
```

} \end{lstlisting} \end{minipage}

By doing this the character actor will check if the size is valid. If so, the character size will change when the \textit{CharacterActor} handle the size property. If not nothing is going to happen, the character size will remain the same.

\subsection{Movement handling}

One of the most important properties to set is the linear velocity in order to make the character move. So, calling the \textit{CharacterActor} \textit{SetLinearVelocity} method would be a good place to start.

The final velocity will be the sum of three separated velocities. These are:

\parbox{0.9\linewidth} { \paragraph{Controlled velocity} Used for handling 100\% controlled movement such as walk, run and not grounded controlled movement. }

\parbox{0.9\linewidth} { \paragraph{Vertical velocity} Used for gravity-based movement such as jumping and gravity. }

\parbox{0.9\linewidth} { \paragraph{External velocity} Used for handling external movement caused by rigidbodies impacts.\ }

\noindent Now we need to implement the HandleMovement method:

\noindent \begin{minipage}{\linewidth} \begin{lstlisting} void HandleMovement\( float dt \) { // Set the values for all the velocities

```text
Vector3 velocity = controlledVelocity + verticalVelocity + externalVelocity;
CharacterActor.SetLinearVelocity( velocity );
```

}  
\end{lstlisting} \end{minipage}

\subsection{Entering the state}

By only implementing the \textit{UpdateBehaviour} method we are reading a bunch of custom velocities \(from the \textit{NormalMovement} state exclusively\) and combining them to obtain a final velocity vector. All these operations are done without previously knowing of the \textit{CharacterActor} linear velocity. If suddenly we are leaving another state and entering the \textit{NormalMovement} state the result will be inconsistent, since the velocities values \(the ones that define the new velocity\) are not aware of the character linear velocity in that particular moment.

To fix this we can override the \textit{EnterBehaviour} method, use it to read the current linear velocity vector and update our custom velocities properly.

\noindent \begin{minipage}{\linewidth} \begin{lstlisting} public override void EnterBehaviour\(float dt\) { verticalVelocity = Vector3.Project\( CharacterActor.LinearVelocity , transform.up \); controlledVelocity = Vector3.ProjectOnPlane\( CharacterActor.LinearVelocity , transform.up \);  
externalVelocity = Vector3.zero;

}

\end{lstlisting} \end{minipage}

\subsection{Collision events}

We can take advantage of the character events to modify whatever parameter we want. In this case we need to convert the collision response into the \textit{externalVelocity} vector.

Another thing to do is to make zero our vertical velocity when the character hits something with its head. We achieve this by \`\`listening'' to the \textit{OnHeadHit} and \textit{OnContactHit} events, using the \textit{OnHeadHit} and \textit{OnContactHit} methods respectively. This is the code used:

\noindent \begin{minipage}{\linewidth} \begin{lstlisting} void OnEnable\(\) { CharacterActor.OnHeadHit += OnHeadHit; CharacterActor.OnContactHit += OnContactHit; }

void OnDisable\(\) { CharacterActor.OnHeadHit -= OnHeadHit; CharacterActor.OnContactHit -= OnContactHit; }

void OnHeadHit\( CollisionInfo collisionInfo \) { verticalVelocity = Vector3.zero; }

void OnContactHit\( Vector3 impulse \) { if\( !rigidbodyResponseParameters.reactToRigidbodies \) return;

```text
externalVelocity = impulse * rigidbodyResponseParameters.impulseMultiplier;
```

} \end{lstlisting} \end{minipage}

