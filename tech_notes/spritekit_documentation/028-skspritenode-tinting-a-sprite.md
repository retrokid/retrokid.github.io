# Tinting a Sprite

-------------------

Provide a color and blend factor to additively color your sprite.

### Overview

You can use the `color` and `colorBlendFactor` properties to colorize the texture applied to a sprite node. The color blend factor defaults to 0.0, which indicates that the texture should be used unmodified. As you increase this number, more of the texture color is replaced with the blended color. For example, when a monster in your game takes damage, you might want to add a red tint to the character. The following code shows how you would apply a tint to the sprite.

```swift
monsterSprite.color = .red
monsterSprite.colorBlendFactor = 0.5
```

![tinting-a-sprite-001](/images/028-skspritenode-tinting-a-sprite-001.png)

You can also animate the color and color blend factors using actions. The following code shows how to briefly tint the sprite and then return it to normal.

```swift
let pulsedRed = SKAction.sequence([
    SKAction.colorize(with: .red, colorBlendFactor: 1.0, duration: 0.15),
    SKAction.wait(forDuration: 0.1),
    SKAction.colorize(withColorBlendFactor: 0.0, duration: 0.15)])
spaceship.run(pulsedRed)
```

----------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/002-skscene-creating-a-scene-from-a-file.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/002-skscene-creating-a-scene-from-a-file.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
