# About SpriteKit Coordinate Systems

---------------------

Learn how a node conforms to its coordinate systems.

### Overview

When a node is placed in the node tree, its `position` property places it within a coordinate system provided by its parent. SpriteKit uses the same coordinate system on both iOS and macOS.

### Points as Position Units

When a node is placed in the node tree, its `position` property places it within a coordinate system provided by its parent. SpriteKit uses the same coordinate system on both iOS and macOS. Figure 1 shows the SpriteKit coordinate system. Coordinate values are measured in points, as in `UIKit` or `AppKit`; where necessary, points are converted to pixels when the scene is rendered. A positive x coordinate goes to the right and a positive y coordinate goes up the screen.

###### Figure 1 SpriteKit coordinate system

![about-spritekit-coordinate-systems-001](/images/013-sknode-about-spritekit-coordinate-systems-001.png)

### Polar Coordinate Rotation

SpriteKit also has a standard rotation convention. shows the polar coordinate convention. An angle of 0 radians specifies the positive x axis. A positive angle is in the counterclockwise direction.

###### Figure 2 Polar coordinate conventions (rotation)

![about-spritekit-coordinate-systems-002](/images/013-sknode-about-spritekit-coordinate-systems-002.png)

Nodes are rotated by setting their `zRotation` property to the required angle in radians. If you prefer to work in degrees, the following code shows how you can write an extension to `CGFloat` that converts between the two. The example in Listing 1 rotates spriteNode by 30 degrees counterclockwise.

```swift
extension CGFloat {
    func degreesToRadians() -> CGFloat {
        return self * CGFloat.pi / 180
    }
}

let rabbitTexture = SKTexture(imageNamed: "rabbit.png")

let spriteNode = SKSpriteNode(texture: rabbitTexture)

spriteNode.zRotation = CGFloat(30).degreesToRadians()
```

--------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/013-sknode-about-spritekit-coordinate-systems.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/013-sknode-about-spritekit-coordinate-systems.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
