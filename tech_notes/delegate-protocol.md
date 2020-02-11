**GameScene**

```swift
import Foundation
import SpriteKit

class GameScene : SKScene, PlayerControllerDelegate
{
	// MARK:- PROPERTIES
	var playerController : PlayerController = PlayerController()

	// MARK:- INIT
	override func didMove(to view: SKView)
    {
        self.playerController.delegate = self
    }

 	// MARK:- DELEGATE FUNCTIONS
    func playerDidAttack()
    {
    	print("player did attack")
    }
}
```

**Player**

```swift
import SpriteKit

class Player : SKSpriteNode
{
    func attack() 
    {
        print("player attacks")
    }
}
```

**PlayerController**

```swift
import Foundation

class PlayerController : NSObject
{
    var player : Player = Player() // create player object
    var delegate : PlayerControllerDelegate? // create delegate object
    func attackKeyPressed()
    {
        player.attack() // tell player object to attack
        delegate?.playerDidAttack // tell delegate to tell scene to run playerDidAttack
    }
}

protocol PlayerControllerDelegate
{
    func playerDidAttack()
}
```

