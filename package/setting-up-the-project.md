# Setting up the project

The main content of **Character Controller Pro does NOT require customized project settings, it is not hard-coded in any way or form**. However, if you need to test the demo scenes that comes with the asset you'll find a problem. This is why you need to set up the project first.

{% hint style="warning" %}
Setting the project is not the same as adding a full character in the scene.
{% endhint %}

## Importing the package

Once the package has been imported, your project view should look like this:

![Project hierarchy.](../.gitbook/assets/project_hierarchy.png)

{% hint style="danger" %}
If you open a scene from the asset and click play you might get several errors and warnings. This is because the demo content requires a few customize settings from the project \(**tags** and **inputs**\).
{% endhint %}

A big welcome screen should appear right after clicking the import button. This screen contains some useful links and more importantly, the setup instructions:

![](../.gitbook/assets/imagen%20%2865%29.png)

Luckily for you there are **presets** included in the package that will help you to configure your project by doing two or three clicks. For more information please see [this](https://docs.unity3d.com/Manual/Presets.html) link.

For example, in order to apply the input settings that come with the CCP:

Go to the InputManager, open the preset window \(top right, see the image\)

![](../.gitbook/assets/imagen%20%284%29.png)

Then select the preset by double clicking it:



![](../.gitbook/assets/imagen%20%2816%29%20%281%29.png)

Do, the same with the tags presets.

## Known issues \(Editor\)

This section contains known issues that escape the asset scope. **They are all related to the Unity editor** in some way.

<table>
  <thead>
    <tr>
      <th style="text-align:left">Issue</th>
      <th style="text-align:left">Description</th>
      <th style="text-align:left">Editor version</th>
      <th style="text-align:left">Fix</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Animation being ignored</td>
      <td style="text-align:left">The Animator does not recognize the NormalMovement runtime animation controller,
        even though it is correctly set up. This happens the <b>first time</b> the
        asset is imported.</td>
      <td style="text-align:left">2020.x.y</td>
      <td style="text-align:left">Restart the project</td>
    </tr>
    <tr>
      <td style="text-align:left">Invisible animation state inspector</td>
      <td style="text-align:left">The state (mecanim) inspector doesn&apos;t show when you click over the
        state.</td>
      <td style="text-align:left">2020.1.x</td>
      <td style="text-align:left">
        <p>Follow this <a href="https://answers.unity.com/questions/1736606/animation-state-of-controller-not-showing-in-inspe.html?childToView=1737595#answer-1737595">link </a>instructions.</p>
        <p></p>
        <p><a href="https://issuetracker.unity3d.com/issues/inspector-not-displaying-state-and-transition-properties-once-duplicated">Issue tracker link</a>
        </p>
      </td>
    </tr>
  </tbody>
</table>

