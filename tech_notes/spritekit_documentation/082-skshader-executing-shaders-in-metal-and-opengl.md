# Executing Shaders in Metal and OpenGL

----------------------

Toggle between renderers to make sure your shader code compiles in both the Metal and OpenGL environments.

### Overview

On devices that support it, the GLSL code you provide to SKShader is automatically converted to Metal shading language and run on a Metal renderer. On older devices, shader code is run in OpenGL. It's important to be mindful of this for debugging purposes because some issues may appear in one renderer but not the other.

You can specify which renderer your device uses—for example, forcing a Metal-enabled device to use SpriteKit's OpenGL renderer for debugging purposes—by adding a PrefersOpenGL to your app's Info.plist key with a value of true. 

> __Important:__
> To ensure compatibility across all devices, test your shader code with and without the PrefersOpenGL key, to be certain it compiles in both environments.

--------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/082-skshader-executing-shaders-in-metal-and-opengl.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/082-skshader-executing-shaders-in-metal-and-opengl.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
