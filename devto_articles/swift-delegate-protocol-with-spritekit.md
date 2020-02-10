This is an example of delegation with SpriteKit.
SpriteKit is Apple's 2D Game Framework.
What i will show you is the how/when i use delegation.

I have 3 classes.

#### 1- GameScene 

This is the current scene of game. This is where all the object are interacting with each others.

*GameScene.swift*

```swift
import Foundation
import SpriteKit

class GameScene : SKScene
{
	// MARK:- PROPERTIES

	var playerController : PlayerController = PlayerController()

	// MARK:- INIT

	override func didMove(to view: SKView)
    {
        // GameScene loaded
    }

}
```

#### Player 

This is my player sprite. This object holds all player animations.(move,attack,jump etc.)

*Player.swift*

```swift
import SpriteKit

class Player : SKSpriteNode
{
	func attack() 
 	{
		// attack animation here
	}
}
```
#### PlayerController 

This object is responsible for receiving user inputs and show some animations regarding of those user inputs.

*PlayerController.swift*

```swift
import Foundation

class PlayerController
{
	var player : Player = Player() // create player object

	func attackKeyPressed()
	{
		player.attack() // tell player object to run animation
	}
}

```

Let's say, user pressed the attack button.
This means *PlayerController* will call attack animation in *Player* object.
But now *GameScene* must know that an attack action happened because *Player* might hit something with that attack and other objects must change their values according to that action.

This is done by **delegation**.
To do it change *PlayerController* object to this:

```swift
import Foundation

class PlayerController
{
	var player : Player = Player() // create player object
	var delegate : PlayerControllerDelegate? // create delegate object

	func attackKeyPressed()
	{
		player.attack() // tell player object to attack
		delegate?.playerDidAttack // GameScene will hear this
	}
}

protocol PlayerControllerDelegate
{
    func playerDidAttack() // delegate function
}
```

And change *GameScene* object to this:

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
        self.playerController.delegate = self // set delegate
    }

 	// MARK:- DELEGATE FUNCTIONS

    func playerDidAttack()
    {
    	print("player did attack")
        // do something when player attacks
        
    }
}
```

Now whenever an attack input entered by user. *PlayerController* will run *Player* object's attack animation and also tell *GameScene* that an attack happened. Then *GameScene* can tell other objects what they should do.

You can also download my prototype game **Retrokid** below.
(Use your keyboard *w,a,s,d* to walk and attack with *k* button.)

[Retrokid App](https://github.com/retrokid/retrokid/releases/download/v0.1.1-alpha/retrokid.app.zip)
[Retrokid Source Code (.zip)](https://github.com/retrokid/retrokid/archive/v0.1.1-alpha.zip)
[Retrokid Source Code (.tar.gz)](https://github.com/retrokid/retrokid/archive/v0.1.1-alpha.tar.gz)