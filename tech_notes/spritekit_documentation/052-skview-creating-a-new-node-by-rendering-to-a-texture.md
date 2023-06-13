# Creating a New Node By Rendering To a Texture

------------------------------

Render a portion of the node tree into a new texture.

### Overview

You can create a texture from some portion of on-screen content with `texture(from:)`, or its variation, `texture(from:crop:)`. Both of these functions are available for scenes rendered by `SKView` or `WKInterfaceSKScene`.

There are a couple reasons you might want to do this, for example:

- Creating a new sprite node whose texture reflects prior shading done with `SKShader`
- Flattening a hierarchy of nodes into a texture, either for performance, or to apply some effect. Note that this can also be done using `SKEffectNode` and setting `shouldRasterize` to true.
- Breaking appart an existing node into separate nodes, for example, for an explosion effect.

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/052-skview-creating-a-new-node-by-rendering-to-a-texture.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/052-skview-creating-a-new-node-by-rendering-to-a-texture.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
