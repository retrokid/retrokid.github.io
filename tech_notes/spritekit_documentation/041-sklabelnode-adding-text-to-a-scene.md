# Adding Text to a Scene

----------------------------

Draw text in your scene, such as a health indicator or a "Game Over" banner, by using a label node.

### Overview

Most apps need to display text at some point, and implementing it correctly yourself can take a significant amount of work. But the `SKLabelNode` class does all of the work necessary to load fonts and create text for display.

Create a new label node by calling the `labelNodeWithFontNamed:` class method. Then configure the other label properties, especially the `text` property. The size of a label node is determined implicitly by its `fontName`, `fontSize`, and `text` properties.

By default, the text label is centered horizontally on the label node’s origin, with the font’s baseline passing through the origin. The `verticalAlignmentMode` and `horizontalAlignmentMode` properties can be used to adjust the label’s position relative to the origin. The following code demonstrates how to create a new text label.

```swift
let winner = SKLabelNode(fontNamed: "Chalkduster")
winner.text = "You Win!"
winner.fontSize = 65
winner.fontColor = SKColor.green
winner.position = CGPoint(x: frame.midX, y: frame.midY)
   
addChild(winner)
```

Whenever you change the label node’s properties, the label node is automatically updated the next time the scene is rendered.

--------------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/041-sklabelnode-adding-text-to-a-scene.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/041-sklabelnode-adding-text-to-a-scene.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
