# Table of contents

* [Introduction](README.md)

## The package <a href="#package" id="package"></a>

* [Content](package/content.md)
* [Versions and updates](package/versioning.md)
* [Setting up the project](package/setting-up-the-project.md)
* [Using the package](package/using-the-package.md)
* [Known issues](package/known-issues.md)

## Fundamentals

* [Core](fundamentals/untitled/README.md)
  * [Character](fundamentals/untitled/character-hierarchy.md)
  * [Character body](fundamentals/untitled/characterbody.md)
  * [Character actor](fundamentals/untitled/character-actor/README.md)
    * [States](fundamentals/untitled/character-actor/stability.md)
    * [Stable movement features](fundamentals/untitled/character-actor/stable-movement-features.md)
    * [Velocity](fundamentals/untitled/character-actor/velocity.md)
    * [Rotation](fundamentals/untitled/character-actor/rotation.md)
    * [Size](fundamentals/untitled/character-actor/size.md)
    * [Collision properties](fundamentals/untitled/character-actor/collision-properties.md)
* [Implementation](fundamentals/implementation/README.md)
  * [Character state controller](fundamentals/implementation/character-state-controller.md)
  * [Character state](fundamentals/implementation/character-state.md)
  * [Character brain](fundamentals/implementation/character-brain.md)

## How to...

* [Core](how-to.../core/README.md)
  * [Create a basic character](how-to.../core/the-most-basic-character.md)
  * [Add logic to your character](how-to.../core/add-logic-to-your-character.md)
  * [Move the character](how-to.../core/move-the-character.md)
  * [Rotate the character](how-to.../core/rotate-the-character.md)
  * [Leave grounded state (e.g. jump)](how-to.../core/leave-grounded-state-e.g.-jump.md)
  * [Change the size of the character](how-to.../core/scale-the-character.md)
  * [Disable collisions between A and B](how-to.../core/disable-collisions-ghost-character.md)
  * [Use the character information (with examples)](how-to.../core/use-the-character-information.md)
  * [Use root motion](how-to.../core/use-root-motion.md)
  * [Detect a character using a "detector"](how-to.../core/detect-a-character-using-a-detector.md)
  * [Add a static one way platform](how-to.../core/add-a-static-one-way-platform.md)
  * [Add a dynamic one way platform](how-to.../core/add-a-dynamic-one-way-platform.md)
* [Implementation](how-to.../implementation/README.md)
  * [Organize the character hierarchy](how-to.../implementation/organize-the-character-hierarchy.md)
  * [States](how-to.../implementation/states/README.md)
    * [Add and configure the state machine](how-to.../implementation/states/add-and-configure-the-state-machine.md)
    * [Create a state](how-to.../implementation/states/create-a-state.md)
    * [Transition from one state to another](how-to.../implementation/states/transition-from-one-state-to-another.md)
    * [Add animation to a state](how-to.../implementation/states/add-animation-to-a-state.md)
    * [Modify an IK (inverse kinematics) element](how-to.../implementation/states/modify-an-ik-element.md)
  * [Actions](how-to.../implementation/actions/README.md)
    * [Define your own actions](how-to.../implementation/actions/define-your-own-actions.md)
    * [Use the character actions](how-to.../implementation/actions/use-the-character-actions.md)
    * [Use a custom Input Handler](how-to.../implementation/actions/use-a-custom-input-handler.md)
    * [Use the new input system](how-to.../implementation/actions/use-the-new-input-system.md)
    * [Create your own AI movement logic](how-to.../implementation/actions/create-your-own-ai-logic.md)
