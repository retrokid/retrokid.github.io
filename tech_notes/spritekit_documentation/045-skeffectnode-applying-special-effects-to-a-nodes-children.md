# Applying Special Effects to a Node's Children

Apply the Core Image suite of filters to child nodes of an effect node.

### Overview

In the example image below, the effect node’s children are two sprites that provide lighting information. The effect node accumulates the effects of these lights, applies a blur filter to soften the resulting image, and uses a multiply blend mode to apply this lighting to a texture.

> __Important:__
> Any Core Image filter that you use must be able to produce a single output image from a single input image.

![applying-special-effects-to-a-nodes-children-001](/images/045-skeffectnode-applying-special-effects-to-a-nodes-children-001.png)

Hereʼs how the scene generates this lighting effect:

1. The scene has two children. The first is a textured sprite that represents the ground. The second is an effect node to apply lighting.
2. The effect nodeʼs children are sprite nodes rendered using an additive blend mode.
3. The effect node includes a filter effect to soften the lighting.
4. The effect node uses a multiplication blend mode to apply its lighting effect to the sceneʼs framebuffer.

The following code demonstrates an implementation of this technique:

```swift
let lightingNode = SKEffectNode()

let light = SKSpriteNode(texture: lightTexture)
light.blendMode = .add
...
lightingNode.addChild(light)

let blurFilter = CIFilter(name: "CIBoxBlur",
withInputParameters: ["inputRadius": 20])

lightingNode.filter = blurFilter

lightingNode.blendMode = .multiply
```

-----------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/045-skeffectnode-applying-special-effects-to-a-nodes-children.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/045-skeffectnode-applying-special-effects-to-a-nodes-children.pdf)

[back to SpriteKit documentation](./spritekit-documentation)