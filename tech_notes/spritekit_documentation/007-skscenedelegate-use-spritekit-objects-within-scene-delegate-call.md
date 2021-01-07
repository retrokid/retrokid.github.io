# Use SpriteKit Objects within Scene Delegate Callbacks

----------------------

Follow threading guidelines to keep your SpriteKit app thread safe.

### Overview

SpriteKit is largely a single threaded game engine and as such the API provides developers with callbacks to implement your custom game logic. The primary callback for your game logic is `update(_:for:)`. Modifying SpriteKit objects outside of the scene delegate callbacks (such as in a background queue or anything else not running on the main thread) can result in concurrency related problems. Even dispatching work on the main thread asynchronously or at a later time is risky because the closure is likely to be done outside of the timeframe SpriteKit expects. If you're experiencing a segmentation fault or other type of crash occurring deep within the SpriteKit framework, there's a good chance your code is modifying a SpriteKit object outside of the scene delegate callbacks.

> __Note:__
> To check at runtime if a particular block of code is running on the main thread, inspect `NSThread isMainThread`.

------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/007-skscenedelegate-use-spritekit-objects-within-scene-delegate-call.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/007-skscenedelegate-use-spritekit-objects-within-scene-delegate-call.md.pdf)

[back to SpriteKit documentation](./spritekit-documentation)