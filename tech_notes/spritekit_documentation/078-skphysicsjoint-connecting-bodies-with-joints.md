# Disconnecting Bodies from Joints

-----------------------

Disconnect joints from nodes in your scene.

### Overview

You can use the `SKPhysicsWorld` method `remove(_:)` to remove joints from a simulation. By making use of the `update(_:for:)` method of the `SKSceneDelegate`, you can interrogate joint properties, such as the distance between the two connected bodies.

The following code shows an example. Each time a new spring joint is created, it is also added to an array named springs of type [SKPhysicsJointSpring]. With each simulation step, every spring is evaluated. If the distance between the two connected bodies is greater than maxSpringDistance, the spring is removed from both the physics world and the array.

```swift
var springs: [SKPhysicsJointSpring] = []
let maxSpringDistance: CGFloat = 31

// Each `scene.physicsWorld.add(spring)` is accompanied by `springs.append(spring)`

func update(_ currentTime: TimeInterval, for scene: SKScene) {
	for spring in springs {
		if let bodyAPosition = spring.bodyA.node?.position,
		let bodyBPosition = spring.bodyB.node?.position {
		let distance = hypot(bodyAPosition.x - bodyBPosition.x,
			bodyAPosition.y - bodyBPosition.y)
		if distance > maxSpringDistance {
			scene.physicsWorld.remove(spring)
			if let index = springs.index(of: spring) {
				springs.remove(at: index)
			}
		}
	}
}}
```

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/078-skphysicsjoint-connecting-bodies-with-joints.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/078-skphysicsjoint-connecting-bodies-with-joints.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
