# Untitled



\section{Character information}

\subsection{Collision information} \label{collisionInfo}

A very import aspect of every character controller is the information this provides to the user. This information is really important to set your basic movement rules, like for example detect if the character is grounded or not, use the ground normal, gather the current ground information, etc.

CCP offers this information in form of public properties. In order to access them you need a reference to the \textit{CharacterActor} component and you are good to go.

For more information about the collision information see the API reference.

\subsection{Collision events}

A collision event is just a delegate event that is called whenever a particular situation happened \(in this case related exclusively to collisions\). When a specific condition is met, the related event will be called by the \textit{CharacterActor}, therefore calling any method subscribed to it.

The package include a number of collision events \(Core and Implementation as well\), if you want to look at them please refer to the API reference. All the events names start with the word \`\`On''.

If you want to see all these events in action, or simply see a code example please check the \textit{CharacterDebug.cs} script. It contains a few methods subscribed to all of the available events. You will notice that every delegate event has its own signature, this is because they are passing information along when the event is called.

For example when the \textit{OnHeadHit} event is called a copy of the \textit{CollisionInfo} structure is passed as an argument, so you can get info from the collision itself \(for example the \textit{contactNormal}\).

\section{Rigidbodies interaction}

\subsection{Push}

The character can push other dynamic rigidbodies by colliding with them. The resulting movement will be determine by the interaction and the rigidbodies parameters \(relative velocity, mass, drag, etc\). This means that the character will push more easily lighter rigidbodies. Since the velocity of the rigidbody is managed by script, in order to increase \(or decrease\) the push force you must increase \(or decrease\) the character rigidbody mass.

It is important to assign the corresponding rigidbodies layers to the \textit{CharacterActor} layer mask in order to produce faithful results. The character must ignore these bodies when detecting collisions, otherwise the interactions will not be correct.

\subsection{Weight}

If the character is standing over a dynamic rigidbody this will apply a force to it \(at the contact point\) proportional to the rigidbody mass.

\subsection{Collision response}

If another dynamic rigidbody hits the character, this will receive a `contact velocity'' due to the collision. Since the velocity is fully scripted, the script involved in the movement will need to know when and how the collision happened in order to react to it. This is handle by an event that is triggered every time a collision happens, passing the`contact velocity'' as an argument.

This allowed rigidbodies to create this type of contact need to be tagged properly. See the \textit{contactRigidbodiesTag} field.

\section{Character graphics} \label{graphics}

Any character in a real-game scenario can be separated into two parts, a physics component and a graphics component, both working together to produce the result we want. The physics component is referred as the \textit{Character Body} \(or simply the \`\`character''\), and the graphics component as the \textit{Character Graphics}.

\parbox{0.9\linewidth} { \paragraph{Character body} This is the actual \`\`character'', it does calculate everything in order to detect collisions, set flags, trigger collision events, and so on. This object is the one with the \textit{CharacterBody} component in it. }

\parbox{0.9\linewidth} { \paragraph{Character graphics} It corresponds to what you actually see on the screen. It includes all the extra components that don't relate directly to the collision body, things like renderers, animations, particles effects, etc. This object is the one with the \textit{CharacterGraphics} component in it \(See \autoref{graphics} for more info\).\

}

\begin{figure} \centering \includegraphics\[width=0.6\linewidth\]{Image/graphics\_A\_B} \caption{} \label{fig:graphicsab} \end{figure}

Decoupling the graphics from the collision body can be very advantageous, since we can handle the position and rotation independently from the actual character object. For instance we can produce any rotation we want \(a common example is the Yaw motion\).

The \textit{CharacterGraphics} component is assigned to a \textit{graphics object} \(hence its name\), taking care of its transform properties, such as position, rotation and scale changes. If you notice the \textit{CharacterGraphics} does not do any graphics related tasks, such as managing animations, renderering, shaders, etc. Instead \ul{it is used to define what is graphics} inside the character hierarchy. This means that the \textit{graphics object} doesn't have to necessarily include all the graphics components directly in it \(for instance these elements can be added to its children instead\).

Think of the \`\`graphics object'' as the root of every graphics related object of your character. If it does graphics it must be placed as a child of this root object.

The \textit{graphics object} is treated as a separated object from the character. Once the game is running \(play mode\), the graphics object and the character object will be separated from each other.

% %\begin{figure}\[H\] % \centering % \begin{subfigure}\[b\]{0.415\linewidth} % \includegraphics\[width=\linewidth\]{Image/graphics\_B} % \caption{Collision body.} % \end{subfigure} % \hspace{1cm} % \begin{subfigure}\[b\]{0.4\linewidth} % \includegraphics\[width=\linewidth\]{Image/graphics\_A} % \caption{Graphics.} % \end{subfigure} % \caption{Character collision body and graphics.} %\end{figure}

\section{Setup of a basic character}

\subsection{Manually} \subsubsection{Adding a character to the scene}

Adding and setting up your own character from zero is really simple, follow these steps:

\begin{enumerate}

```text
\item Add an empty \textit{GameObject} to the scene. This will be the character GameObject, so let's call it ``Character''.

\item Add a \textit{CharacterBody} component to the character.

\item Adjust the body size (see figure \ref{fig:tutocharacter}), physics type, mass, etc.

\item Add a \textit{CharacterActor} component to the character.     
```

\end{enumerate}

\subsubsection{Adding graphics}

\begin{enumerate}

```text
\item Create a child empty object for ``Character''. Since this corresponds to the graphics part let's call it ``Graphics''.

\item Add a \textit{CharacterGraphics} component to it.    

\item Add your animated model object as a child of ``Graphics''. This object will contains the actual renderers, animation components, animation scripts, etc.
```

\end{enumerate}

\subsubsection{Adding a scene controller}

\begin{enumerate}

```text
\item Create an empty object, let's call it ``Scene controller''.    

\item Add a \textit{SceneController} component to it.
```

\end{enumerate}

\subsection{Using prefabs}

Another way to adds character and a scene controller into the scene \(and skip all the previous steps\) is by simply using a prefab. These prefabs are placed at \textit{\`\`Assets/Character Controller Pro/Core/Prefabs''}. A new character hierarchy should look like figure \ref{fig:characterhierarchy}.

\begin{figure} \centering \includegraphics\[width=0.5\linewidth\]{Image/character\_hierarchy} \caption{Automatic template for a character.} \label{fig:characterhierarchy} \end{figure}

\section{Implementing the core}

The one thing to do next is to use these concepts in a practical way. Usually a character controller\footnote{High level component that interacts with the low level character components in order to produce movement.} is needed to produce some basic moments. In order to create this type of component first you need to know all about the public fields and methods the CharacterActor offers to you \(see the API reference for more detail\). Once you are familiarized with it you can start to create your own scripts around this. These scripts must hold a reference to the core components \(or at least the ones you're going to use\). Once this is done the way is clear for you to define \(within the scope of CCP\) your own vision for your character.

The implementation contained within the package is one big example of this working \(and much more\). If you want know all about the implementation please read \autoref{imple}.

