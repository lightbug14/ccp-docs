# Introduction

![](../../.gitbook/assets/keyimage_cover.png)

### Description

Character Controller Pro \(CCP for short\) is a 2D/3D Dynamic Character Controller that allows you to handle the movement, rotation and size of your character \(among other things\) in a precise way.

The main highlights of the package are listed below:

* **Hybrid approach:** This character controller is Dynamic by nature, this means that the character uses a collider and a dynamic rigidbody to detect collisions and to do movement. However, almost all of its actions are predicted/calculated in a \`\`kinematic way''. This was intended that way in order to combine the best of both worlds, that is, the preciseness of a kinematic character and the collision detection/rigidbodies interaction of a dynamic character.
* Capsule body shape: The character is modelled as a 2D/3D upright capsule.

2D and 3D Physics

```text
This package supports 2D and 3D Physics, meaning that your character will detect and interact with 2D and 3D Colliders as well.
```

2D and 3D Movement: Every component available in the package was created with 2D/3D movement in mind. No behaviour is specific neither to 2D nor 3D space.

Rigidbodies interaction: Since the character is dynamic it can interact with other rigidbodies, push them, get pushed by them, and gather information from the interaction.

Technical level: This character controller not only gives you good results, but also technical information about the world the character is interacting with.

\section{Content}

\textit{Character Controller Pro} is organized in three parts:

\parbox{0.9\linewidth} { \paragraph{Core}

```text
The main part of the package, it does the heavy lifting regarding collision detection, character information, movement, etc. If you want to extend the package or maybe you don't like the current implementation, you should use the core, it will give all the necessary tools to create your character on top.
```

}

\parbox{0.9\linewidth} {  
\paragraph{Implementation}

```text
Consist of a bunch of components that implement the functionality of the \textit{Core}. These components cover many aspects and intend to create a ``character ecosystem'' around the \textit{Core}. This part of the package can be customize and/or extended if needed.
```

}

\parbox{0.9\linewidth} { \paragraph{Demo}

```text
Basically all the assets used for the making of the demo scenes, from materials and sprites, to pure data containers.\\
```

}

\noindent Although the implementation is encapsulated within the package, if you you need to handle things in a specific manner you can implement it all by yourself on top of the \textit{Core}. This is why the \textit{Core} and the \textit{Implementation} are separated. Both have its own directories and are defined within its own namespace \(see the API reference\).

\section{Asset version}

The versioning scheme used for CCP is the following:

\begin{center} \mbox { {\large Major.Feature.Minor}

} \end{center}

\parbox{0.9\linewidth} {

```text
\paragraph{Minor} Basically bug fixes, small changes, code improvements, etc. This update is always recommended, no risk at all.

\paragraph{Feature} New features, small updates, a new fancy component, etc. Beware! It might break some things.

\paragraph{Major} This update will break almost everything for sure, this means a new fresh start, new systems, new components, an overall change.
```

}

\section{Unity version}

CCP is developed and uploaded using Unity 2018.3.2, since this version presents a nice balance between modern features, comfort and usability. The package is compatible with \ul{2018.3.2 or higher}. \textbf{If you notice some incompatibility with a newer version of Unity, please let me know}.

\section{Setting up the project}

\subsection{Importing the package}

Once the package has been imported your project view should look similar to what is shown in figure \ref{PHierar}.

\begin{figure} \centering \includegraphics\[width=0.5\linewidth\]{Image/project\_hierarchy} \caption{Project hierarchy right after importing the asset.} \label{PHierar} \end{figure}

The first thing to do is to open the folder \textit{\`\`OPEN ME''}. In there you will find all the necessary material to put this package to work. In order to make CCP fully functional \(at least for demo purposes\) you need to adjust some Unity's settings.

The imported package contains a few presets\footnote{Predefined settings to use \(and reuse\) in a specific window type.}, these are related mainly to `Layers'' and`Inputs''. Apply these presets to your project, after doing this you will now visualize all the layers with their appropriate names, and the inputs buttons will be registered in the input manager.

The layers and inputs settings are necessary initially for demo purposes only. If you want to use CCP in your own project you can redefine these settings to your liking.

\subsection{Using the package}

The recommended way to use this package \(and every package out there, really\) is by working on a separated path \(outside the \textit{\`\`Character Controller Pro''} folder\). This is useful if you need to use and/or extend the asset in any way.

\subsection{Updating the package}

To update the package \(regardless of the version\) is recommended to delete the \textit{\`\`Character Controller Pro''} folder in its entirely, then import the updated version. Remember always to put your own work outside this folder.

