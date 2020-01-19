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
> In the _**Normal**_ **state**, to activate the jet pack only a specific button press is needed. This state doesn't have any information about the _JetPack_ state whatsoever \(and it shouldn't\). For the _JetPack_ state is another story. 
>
> The _**JetPack**_ state must check if everything is ok, before allowing the transition to happen. For instance, if the character jet pack doesn't have any fuel, this should not be active. In the transition code, inside the _JetPack_ state we can make sure that the fuel is enough.









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

