# Applying Shaders to a Sprite

----------------------

Write custom GLSL code that modifies the look of your sprite.

### Overview

You can use the `shader` property of a sprite node to change the appearance of a texture with a custom OpenGL ES fragment shader embedded within a `SKShader` object. Custom shaders offer almost limitless possibilities, from adding blurs and color treatments to textures to generating imagery such as random noise.

The following code shows a small custom shader which inverts the color of a texture while leaving the alpha or transparency unaffected:

```swift
let negativeShader = SKShader(source: "void main() { " +
    "    gl_FragColor = vec4(1.0 - SKDefaultShading().rgb, SKDefaultShading().a); " +
    "}")
rocket.shader = negativeShader
```

The following figure illustrates the effect of the shader. The original image, on the left, has its colors inverted by the shader:

![applying-shaders-to-a-sprite-001](/images/031-skspritenode-applying-shaders-to-a-sprite-001.png)

-----------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/031-skspritenode-applying-shaders-to-a-sprite.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/031-skspritenode-applying-shaders-to-a-sprite.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
