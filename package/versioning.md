# Versions and updates

You should always update to a newer version of the package, unless the **risk **of doing so is high enough for your particular project (in some cases it is best to keep using an old version).

## Versioning scheme

The version number indicates the **risk **involved when updating the asset. By "risk" i mean things that can cause issues all of kind, such as console errors, API incompatibilities, new features replacing older ones, deprecation of some specific functionalities, an overall design change, etc.

This is the versioning scheme used:

####                                                                    Major.Feature.Minor

| Update                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| <p></p><p>Minor</p>   | <p></p><p>Basically bug fixes<strong>,</strong> code improvements, etc. Sometimes, new minor features will be introduced, as long as they don't interfiere with the rest of the package.</p><p></p><p>This update is <strong>always recommended</strong>, it should not give you any issues. That being said, it is also recommended to check the release notes before attempting to update the package.</p><p></p><p>Risk: <strong>Zero </strong><span data-gb-custom-inline data-tag="emoji" data-code="2705">✅</span></p> |
| <p></p><p>Feature</p> | <p></p><p>This update <strong>usually </strong>involves one or more new relevant features, thus the name. </p><p>Sometimes improving an existing feature may require an overall re-design of the code, such changes could end up causing API incompatibilities. If that's the case, the update will be labeled as a "feature" update, even though there will be no new features available.</p><p></p><p>Risk: <strong>Low to medium </strong><span data-gb-custom-inline data-tag="emoji" data-code="26a0">⚠</span> </p>     |
| <p></p><p>Major</p>   | <p></p><p>A major update is used as an opportunity to re-design the core of the asset. By doing so it's expected to create some sorts of components and API incompatibilities.</p><p></p><p>This type of update could involve a new upgrade (a.k.a new asset package). By doing so, you will have access to the old package every time you want.</p><p></p><p>Risk: <strong>Maximum </strong><span data-gb-custom-inline data-tag="emoji" data-code="2622">☢</span></p>                                                      |

{% hint style="danger" %}
The demo content is not represented by the scheme presented above. This basically means this content might change a lot from version to version, or not.
{% endhint %}

## Support

Let me make this clear:** I will always put all my effort in the latest version of the package**. In my own eyes, that's the best this package can get, and i will always recommend you to get that version.  This obviously doesn't mean you won't receive support if you are using an older version.

## How to update

To update the package (regardless of the version) is recommended to **delete the **_**Character Controller Pro**_** folder **and then import the new version. 

{% hint style="warning" %}
Remember always to put your own work outside this folder.
{% endhint %}
