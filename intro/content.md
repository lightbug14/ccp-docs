# Content

_Character Controller Pro_ is organized in three parts:

### Core

The main part of the package, it does the heavy lifting regarding collision detection, character information, movement, etc. If you want to extend the package or maybe you don't like the current implementation, you should use the core, it will give all the necessary tools to create your character on top.

### Implementation

Consist of a bunch of components that implement the functionality of the \textit{Core}. These components cover many aspects and intend to create a \`\`character ecosystem'' around the \textit{Core}. This part of the package can be customize and/or extended if needed.

### Demo

Basically all the assets used for the making of the demo scenes, from materials and sprites, to pure data containers.

Although the implementation is encapsulated within the package, if you you need to handle things in a specific manner you can implement it all by yourself on top of the \textit{Core}. This is why the _Core_ and the _Implementation_ are separated. Both have its own directories and are defined within its own namespace \(see the API reference\).

