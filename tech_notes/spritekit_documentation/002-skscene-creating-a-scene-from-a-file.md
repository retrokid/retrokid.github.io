# Creating a Scene from a File

----------------------

Load a scene that you configure in Xcode's scene editor.


### Overview

The most common way to load an `SKScene` is through an .sks file configured in Xcode's scene editor. Making your base changes in the editor is faster than writing equivalent initialization code, and it avoids repeating code if you create a scene in multiple places.

### Create a New Scene File

First, add a new scene file to your project through Xcode's File menu > New... > File > (choose your platform tab) > SpriteKit Scene.

###### Figure 1 Creating a new SpriteKit Scene file

![creating-a-scene-from-a-file-001](/images/002-skscene-creating-a-scene-from-a-file-001.png)

### Configure the Scene Using the Editor

You configure your scene in the scene editor by clicking on the .sks file in Xcode's file navigator pane, then adjusting properties in the Utility pane. For example, to set your scene's background color, follow the steps highlighted in Figure 2:

1. Select the .sks file in the file navigator pane.
2. Open the Utilities pane.
3. Choose the Attributes inspector.
4. Define a color under Scene.

###### Figure 2 Setting the background color in the scene editor

![002-skscene-creating-a-scene-from-a-file-002](/images/002-skscene-creating-a-scene-from-a-file-002.png)

### Load the Scene in Code

Load the newly configured scene file in code using `init(fileNamed:)`.

```swift
let scene = SKScene(fileNamed: "MyScene")
        
// Now present the scene in a view.
skView.presentScene(scene)
```

> __Note__:
> The .sks file extension is left out of the String name argument to `init(fileNamed:)`.

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/002-skscene-creating-a-scene-from-a-file.md)

[download this page as .pdf]()

[back to SpriteKit documentation](./spritekit-documentation)
