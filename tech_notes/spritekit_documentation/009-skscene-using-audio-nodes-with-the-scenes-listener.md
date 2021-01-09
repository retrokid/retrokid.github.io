# Using Audio Nodes with the Scene's Listener

---------------------

Add audio to your scene, and optionally give it 2D-positional mixing characteristics.

### Overview

The simplest way to add audio to a SpriteKit scene is to add a child `SKAudioNode` to it:


```
let audio = SKAudioNode(fileNamed: "drums.mp3")

spriteKitViewController.scene.addChild(audio)
```

However, if you define the presented scene's `listener`, its audio nodes are played back with positional sound mixing. For example, if you set the scene's listener to be the scene's camera and then add audio nodes as children to various parent nodes in the scene, the further away the parent nodes are from the center of the screen, the quieter their audio will be played.

----------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/009-skscene-using-audio-nodes-with-the-scenes-listener.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/009-skscene-using-audio-nodes-with-the-scenes-listener.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
