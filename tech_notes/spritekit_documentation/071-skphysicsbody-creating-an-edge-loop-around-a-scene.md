# Creating an Edge Loop Around a Scene

-----------------------------

Border your scene with an obstacle that physics bodies cannot penetrate.

### Overview

When you want to confine your in-app objects to a specific region, use an edge-based physics body to define the area. In an app that models a pool table, for example, the balls are the in-app objects, and the table edges collectively create an edge loop. The following code demonstrates creating an edge loop to implement an impenetrable boundary that extends from edge to edge in the scene.

```swift
func createSceneContents() {
    self.backgroundColor = .black
    self.scaleMode = .aspectFit
    self.physicsBody = SKPhysicsBody(edgeLoopFrom: self.frame)
}
```

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/002-skscene-creating-a-scene-from-a-file.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/002-skscene-creating-a-scene-from-a-file.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
