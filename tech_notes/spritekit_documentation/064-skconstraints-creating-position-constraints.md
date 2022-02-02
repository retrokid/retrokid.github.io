# Creating Position Constraints

-------------------------

Create a position constraint and add it to a node.

### Overview

You lock a node at a specific coordinate with `positionX(_:y:)`. Constrain a node's horizontal position with `positionX(_:)`, or constrain its vertical position with `positionY(_:)`.

The following code shows how you can create a node with an attached physics body that is affected by a noise field. The node moves with the noise but is constrained to a rectangular region between 300 and 340 points on both the horizontal and vertical axes.

```swift
scene.physicsWorld.gravity = CGVector(dx: 0, dy: 0)
   
let noiseField = SKFieldNode.noiseField(withSmoothness: 1, animationSpeed: 0.1)
scene.addChild(noiseField)
     
let node = SKShapeNode(circleOfRadius: 10)
node.physicsBody = SKPhysicsBody(circleOfRadius: 10)
scene.addChild(node)
     
let range = SKRange(lowerLimit: 300, upperLimit: 340)

let lockToCenter = SKConstraint.positionX(range, y: range)

node.constraints = [ lockToCenter ]
```

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/064-skconstraints-creating-position-constraints.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/064-skconstraints-creating-position-constraints.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
