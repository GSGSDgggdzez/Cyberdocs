# APK Structure

- `AndroidManifest.xml` : the manifest configuration file in binary XML format.

- `META-INF/` : folder containing the `MANIFEST.MF` file, which stores metadata about the JAR content. which will sometimes be stored in a folder named original. The APK signature is also stored in this folder.

- `Assets/`: optional folder containing application assets, which can be retrieved by AssetManager.

- `resources.arsc` : file containing precompiled application resources, in binary XML.

- `lib/` : optional folder containing compiled code - i.e. native code libraries.

- `classes.dex` : application code compiled in dex format.

- `res/`: folder containing resources not compiled in resources.arsc
