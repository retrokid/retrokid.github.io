# Using Base Nodes to Lay Out SpriteKit Content

------------------

Use nonvisual nodes to define the layout of a scene.

### Overview

Each onscreen element in SpriteKit is referred to as a node. Nodes are either visual elements or containers of other nodes. You set up the appearance of a SpriteKit scene by adding nodes alongside and on top of each other in a hierarchical form. Collectively, this structure is referred to as the node tree or the node hierarchy.


These are the basic nonvisual nodes in SpriteKit:

- `SKNode` is a container node. It doesn't render any content of its own, but works as a layout tool for its child nodes.
- `SKReferenceNode` doesn't define content of its own, but refers to another node or archived file that does.
- `SKCameraNode` defines point of view within a scene. Its inverse scale is applied to all nodes in the hierarchy except for its children. Use the children of SKCameraNode for UI elements that should be unaffected by zoom level.

---------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/010-nodesforscenebuilding-using-base-nodes-to-lay-out-spritekit-content.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/010-nodesforscenebuilding-using-base-nodes-to-lay-out-spritekit-content.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
