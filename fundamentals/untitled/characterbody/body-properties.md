# Body properties

### Foot position

The foot position is considered as the origin, a point of reference for everything. As is normally for character controllers, the origin is assumed to be the bottom most point of the character body. In this case is the bottom point of the capsule.

### Orientation

The character is modeled as an upright capsule. This means that the capsule height vector\footnote{Vector defined from the bottom sphere to the top sphere} and the up vector of the character transform will have always the same direction vector.

![](../../../.gitbook/assets/capsuleupright.png)

This capsule is not visible, any real character will need a graphics element with a renderer to show the mesh or sprite on screen.

### Size

Since this is a capsule-based character we need only to define the radius and the height to fully describe the size of the character. The \textit{CharacterActor} will consider the character dimensions as:

$$
Width = 2 \times Collider.Radius
$$

$$
Height = Collider.Height
$$

The Width and Height values are represented with the _body size_ \(a _Vector2_\).

![](../../../.gitbook/assets/capsulebodydimensions.png)

{% hint style="info" %}
In play mode the collider offset will be automatically adjusted.
{% endhint %}

### Scale

This is an important topic, the \textit{CharacterBody} component defines the character size using an absolute value based on a _Vector2_ field. The _CharacterActor_ component reads this value in order to perform all the necessary physics queries \(mainly for collision detection\).

#### So, What happens if the _localScale_ is not _Vector3.one_? 

Even though the collider will be scaled just fine, the internal "physics size'' will not. So, **it is not recommend to scale the character using the** _**Transform**_ **component**.

\textbf{What if i want to scale my character?} Well, in that case you should scale the graphics object, not the character itself. After that, the body size should be modified to fit the graphics.

\noindent \fbox{ \begin{minipage}\[t\]{\textwidth} In other words: the character \textit{localScale} should always be $ &lt; 1, 1 , 1 &gt; $.  
\end{minipage} }

\subsection{Collision shape}

Even though this is a dynamic character controller, the \textit{CharacterActor} is still doing physics queries to detect collisions. Because of this an effective collision shape was defined \(different from the character body shape\) using the width, height and skin width \(See figure \ref{fig:Tuto\_character\_SW}\).

\begin{figure} \centering \includegraphics\[width=0.3\linewidth\]{Image/collisionShape} \caption{The collision shape of the character.} \label{fig:Tuto\_character\_SW} \end{figure}

\section{CharacterActor} \label{Core}

The \textit{CharacterActor} component follows a few simple rules that needs to be understood in order to use it. These rules are related to teleportation, size, position and rotation. All the actions required from the \textit{CharacterActor} have a deferred nature, this means that they are not executed immediately. All the changes are applied when the \textit{CharacterActor} needs to.

\begin{figure} \centering \includegraphics\[width=0.3\linewidth\]{Image/core\_internal.png} \caption{\textit{CharacterActor} internal actions.} \label{fig:core\_internal} \end{figure}

The main properties to look for are shown in figure \ref{fig:core\_flow}. The \textit{CharacterActor} offers a few public methods and properties that allow you to define these properties.

\begin{figure} \centering \includegraphics\[width=0.4\linewidth\]{Image/core\_flow} \caption{\textit{CharacterActor} internal actions.} \label{fig:core\_flow} \end{figure}

The following sections explain how all these individual elements work internally.

\subsection{Teleportation}

If the character needs to change instantly its position and/or rotation \(ignoring the collision detection algorithm\) then the Teleportation method should be used.

\subsection{Size}

Internally the size of the character is stored in a Vector2 variable called \texttt{bodySize}. The x component represents the width and the y component represents the height. The initial size will be assigned based on the capsule collider parameters and some internal constants.

The size can be modified externally by a script \(using the  
\texttt{SetBodySize} method\), passing any value possible as the desired size. Since the character may or may not fit in a given space, the size must be internally checked beforehand by the \textit{CharacterActor}, thus defining the final character size.

\subsection{Orientation}

The orientation is completely managed by the \textit{CharacterActor} component. Any external change to the character rotation will be overwritten. There are two ways to describe a normal character rotation:

\parbox{0.9\linewidth} { \paragraph{ Gravity } The current gravity direction will define the character up vector as its opposite.

```text
\paragraph{ Yaw } This is the rotation motion around the local up axis.
\\
```

}

The character is capable of changing its rotation values by using the gravity information. This is possible by using the gravity direction and graviy modes from the CharacterActor component. For example, in figure \ref{fig:gravity} the character is align itself using the gravity vector.

\begin{figure} \centering \includegraphics\[width=0.4\linewidth\]{Image/gravity} \caption{The character orientation being changed in a gravity shifting scenario \(a planet in this case\).} \label{fig:gravity} \end{figure}

On the other hand, \ul{the character cannot do yaw rotation at all}, instead it has a \textit{forward direction} vector, which can be defined and used for the user at will \(see figure \ref{fig:lookingDir}\). This vector will be properly rotated internally by the \textit{CharacterActor} \(gravity shifting scenarios and dynamic ground motion\).

\begin{figure} \centering \includegraphics\[width=0.8\linewidth\]{Image/lookingDir} \caption{The graphics doing yaw motion towards the forward direction vector. The character rotation is not modified whatsoever.} \label{fig:lookingDir} \end{figure}

It is important to mention that the forward direction vector will always be projected onto the plane formed by the character up direction. If a random vector is defined as forward direction, this will be projected onto this plane.

\subsection{Position}

The change in position related to a \textit{LinearVelocity} field. The necessary displacement is calculated based on the current linear velocity value. This movement will take into account collision detection. The \textit{LinearVelocity} vector needs to be set externally by a script.

The movement algorithm is based on the classic \textit{Collide \& Slide} algorithm. Although is not necessary to do a bunch of collision test in order to avoid the character to pass through other colliders \(since this is a rigidbody based character controller\), these test are still performed. This is because the character gathers information from the environment \(see \autoref{collisionInfo}\) and also can predict its movement before hand, which is really useful.

\subsubsection{Grounded state}

The movement can be classified in \textit{Grounded} and \textit{Not Grounded}, depending on the current grounded state. Both type of motion have its differences, the not grounded movement only performs the basic collide and slide action, while the grounded movement does the same but also includes all the available features \(step detection, edge detection, edge compensation, etc\).

\parbox{0.9\linewidth} { \paragraph{\textit{Grounded} to \textit{Not Grounded}} To make the transition you must call the \textit{ForceNotGrounded} method. If you are using gravity in your script remember to apply a positive vertical velocity \(towards the character up vector\), otherwise this will return to the grounded state the next frame.

}

\parbox{0.9\linewidth} {

\paragraph{\textit{Not Grounded} to \textit{Grounded}} In this case you must apply a negative vertical velocity \(towards the character up vector\)

}

\subsubsection{Stability}

A character is stable when it is grounded and the \textit{stable slope angle} \(see the API reference\) is less than or equal to the \textit{slope limit} value.

\noindent \begin{minipage}{\linewidth} \begin{lstlisting} stable = IsGrounded && \( stableSlopeAngle &lt;= slopeLimit \); \end{lstlisting} \end{minipage}

This angle should not be confused with the \textit{slope contact angle}, obtained directly from the collision test \(See figure \ref{fig:contactvsstable}\).

\begin{figure} \centering \includegraphics\[width=0.4\linewidth\]{Image/contactVsStable} \caption{\textit{Stable normal} vs \textit{contact normal}.} \label{fig:contactvsstable} \end{figure}

The concept of stability is used internally by the \textit{CharacterActor} to detect steps, edges, do ground probing, and so on. By itself it will not produce any type of movement, but it can be used for creating custom behaviours. For example, in the included implementation, a grounded and unstable character will slide down from the slope it is currently standing on. For example, referring back to figure \ref{fig:contactvsstable}, the character will not fall since the stable slope angle \(from the stable normal\) is allowed.

\subsubsection{Velocity Projection}

The \textit{LinearVelocity} vector provides the information needed to move the character from point A to point B. However, this vector is not used directly to calculate the actual displacement, since it may not follow the \textit{CharacterActor} internal movement rules. This can be a problem only when the character is grounded.

In order to use a valid displacement vector, the linear velocity must be projected onto the current slope plane. The \textit{CharacterActor} will take the linear velocity field and do the projection \ul{maintaining its magnitude}. This can be seen much more clearly in figure \ref{fig:velocityproj}.

\textbf{Important:} the displacement vector will be created maintaining its initial magnitude. This basically means that the character will always move at its input velocity magnitude, regardless of the slope angle. This can be seen in figure \ref{fig:velocityproj}.

\begin{figure} \centering \includegraphics\[width=0.4\linewidth\]{Image/VelocityProj} \caption{The \textit{LinearVelocity} projected onto a stable slope.} \label{fig:velocityproj} \end{figure}

\subsubsection{Slopes handling}

The character can walk onto any slopes whose angle is less than the slope limit value. Prior to the movement calculation a displacement vector is created \(based on the linear velocity\) and subsequently modified in the process. The collide and slide algorithm will iterate over and over until the displacement magnitude is less that the minimum movement amount constant, or the number of iterations performed exceeds the maximum number of slide iterations.

If the encountered slope is allowed the character will walk onto it, modifying the displacement vector. if not the slope will be considered as an invisible wall. See figure \ref{fig:slopes} and figure \ref{fig:Slopes\_Allowed} for more detail.

\begin{figure} \centering \includegraphics\[width=0.6\linewidth\]{Image/Slopes} \caption{The character climbing up a slope.} \label{fig:slopes} \end{figure}

\begin{figure}\[H\] \centering

```text
\begin{subfigure}{0.45\linewidth}
    \includegraphics[width=\linewidth]{Image/Slopes_3D.png}
    \caption{Unallowed slopes.}        
\end{subfigure}
\hspace*{\fill}
\begin{subfigure}{0.45\linewidth}
    \includegraphics[width=\linewidth]{Image/Slopes_3D_allowed.png}
    \caption{Allowed slopes.}
\end{subfigure}

\caption{Deflection of the displacement vector.}
\label{fig:Slopes_Allowed}
```

\end{figure}

