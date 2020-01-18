# Implementing the core

The one thing to do next is to use these concepts in a practical way. Usually a character controller\footnote{High level component that interacts with the low level character components in order to produce movement.} is needed to produce some basic moments. In order to create this type of component first you need to know all about the public fields and methods the CharacterActor offers to you \(see the API reference for more detail\). Once you are familiarized with it you can start to create your own scripts around this. These scripts must hold a reference to the core components \(or at least the ones you're going to use\). Once this is done the way is clear for you to define \(within the scope of CCP\) your own vision for your character.

The implementation contained within the package is one big example of this working \(and much more\). If you want know all about the implementation please read \autoref{imple}.

