# Getting Started with Particle Shaders

----------------------------

Provide custom shader code to alter a particle's look.

### Overview

Use the shader property of an emitter node to change the appearance of a texture with a custom OpenGL ES fragment shader embedded within an `SKShader`. Custom shaders offer almost limitless possibilities, from adding blurs and color treatments to textures, to generating imagery such as random noise.

The following code shows a custom shader that renders particles with a radial gradient. The center of each particle is opaque white and the edges are transparent black.

```swift
let emitter = SKEmitterNode()
    
let radialGradientShader = SKShader(source: "void main() {" +
    "    vec2 coord = (v_tex_coord - 0.5) * 2.0;" +
    "    gl_FragColor = vec4(1.0 - length(coord));" +
    "}")  
      
emitter.shader = radialGradientShader
```

------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/039-skemitternode-getting-started-with-particle-shaders.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/039-skemitternode-getting-started-with-particle-shaders.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
