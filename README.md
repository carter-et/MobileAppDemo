# ARCore Demo

## Introduction
Welcome to my ARCore demo and introduction. I've included the sample code that you'll need, 
as well as a finished version of what we've got by the end of this. ARCore has A LOT of stuff 
packed into it. For this demo, we're just taking a look at the depth and instant placement
features. 

_We will be focusing on using Java for this Demo, instead of Kotlin._

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
    ``` private static final String objRef = "models/violin/Violin.obj"; ```
    ``` private static final String textureRef = "models/textures/white.jpg"; ```
1. The previous textures that were being loaded in were specific to the AR Pawn. We we'll want to replace those. 
    ``` //replace the old textures around line 400 with this```
    ``` Texture virtualObjectPlainTexture =
          Texture.createFromAsset(
              render,
              "models/white.jpg",
              Texture.WrapMode.CLAMP_TO_EDGE,
              Texture.ColorFormat.LINEAR);
        virtualObjectMesh = Mesh.createFromAsset(render, textureRef); ```