# Core

\section{Setup of a basic character}

## Manually 

### Adding a character to the scene

Adding and setting up your own character from zero is really simple, follow these steps:

1. Add an empty \textit{GameObject} to the scene. This will be the character GameObject, so let's call it \`\`Character''.
2. Add a \textit{CharacterBody} component to the character.
3. Adjust the body size \(see figure \ref{fig:tutocharacter}\), physics type, mass, etc.
4. Add a \textit{CharacterActor} component to the character.     

### Adding graphics

1. Create a child empty object for \`\`Character''. Since this corresponds to the graphics part let's call it \`\`Graphics''.
2. Add a \textit{CharacterGraphics} component to it.
3. Add your animated model object as a child of \`\`Graphics''. This object will contains the actual renderers, animation components, animation scripts, etc.

### Adding a scene controller

1. Create an empty object, let's call it \`\`Scene controller''.
2. Add a \textit{SceneController} component to it.

## Using prefabs

Another way to adds character and a scene controller into the scene \(and skip all the previous steps\) is by simply using a prefab. These prefabs are placed at \textit{\`\`Assets/Character Controller Pro/Core/Prefabs''}. A new character hierarchy should look like figure \ref{fig:characterhierarchy}.

\begin{figure} \centering \includegraphics\[width=0.5\linewidth\]{Image/character\_hierarchy} \caption{Automatic template for a character.} \label{fig:characterhierarchy} \end{figure}



