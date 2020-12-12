# ARCore Demo

## Introduction
Welcome to my ARCore demo and introduction. I've included the sample code that you'll need, 
as well as a finished version of what we've got by the end of this. ARCore has A LOT of stuff 
packed into it. For this demo, we're just taking a look at the depth and instant placement
features. 

_We will be focusing on using Java for this Demo, instead of Kotlin._

## Disclaimers
This is a pretty underwhelming tutorial. As of October, [sceneform became deprecated](https://developers.google.com/sceneform/develop/getting-started) which was the main way that you would manage 
object files in your project. This means there are nearly no relevant examples or documentation with 
the new changes. Something to do with maven not being stable... Eitherway, after almost 20 hours of running demos and scavenging the web, I've put together a bit of what I've learned. 

## Building the project
To build the project, you can follow [this guide](https://developers.google.com/ar/develop/java/quickstart).
It'll tell you to clone this repo: 

`git clone https://github.com/google-ar/arcore-android-sdk.git`.

## Run the project
It's important to run the demo project to make sure it's all working, before we start making modifications.
I highly reccomend pluging your phone into your computer and 
[enabling developer mode](https://www.howtogeek.com/129728/how-to-access-the-developer-options-menu-and-enable-usb-debugging-on-android-4.2/). 
However, you can still use and AVD for this. The Pixel 3 XL is on the list of supported devices, so you 
should be fine with that. 

Congrats! Welcome to ARCore.

## Change your model
Running the demo is all well and good, but what if you wanted to load up a different model? No problem.
First, let's download some assets. If you don't feel like doing that, I've included a file with some of 
my own. When looking for files, you'll need a .obj filetype that is smaller than 2.56MB. There is an
internal limit currently that caps the size of .obj files that can be rendered.

1. Copy your assets to `app/assets/models`.
1. In `HelloArActivity.java` add this at the top of the class. 

    ```
    //change this to wherever you keep your obj and textures. The root for this is you assets folder. 
    private String objRef = "models/violin/Violin.obj";
    private String textureRef = "models/white.jpg";
    ```

1. Let's pivot really quick and update the `AndroidManifest.xml` and `src/build.grade`.
    Add this permission to the manifest:
    ```
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    ```

1. The previous textures that were being loaded in were specific to the AR Pawn. We'll want to replace those. 

    ``` 
    //replace the old textures around line 400 with this
    Texture virtualObjectPlainTexture =
          Texture.createFromAsset(
              render,
              textureRef,
              Texture.WrapMode.CLAMP_TO_EDGE,
              Texture.ColorFormat.LINEAR); 
    ```
1. Next we're going to change the Mesh that's defines our object. 

    ```
    //replace the old object mesh 
    virtualObjectMesh = Mesh.createFromAsset(render, objRef); 
    ```
1. Lastly, the next shader method is adding these textures to your object. Let's remove these lines and
set the texture to the one we just made.
    ```
    //replace the object shader with this
    virtualObjectShader =
          Shader.createFromAssets(
                  render,
                  "shaders/environmental_hdr.vert",
                  "shaders/environmental_hdr.frag",
                  null)
              .setTexture("u_AlbedoTexture", virtualObjectPlainTexture);
    ```

Great, that should be all the changes we need for now, give it a run and see how your custom objects look!

## TBD
This section has yet to be completed, but it would allow us to choose new object files from within the app. 

## Resources
A list of resources used to help me put this together
- https://codelabs.developers.google.com/codelabs/augimg-intro/#0
- https://developers.google.com/ar/develop/java/quickstart

