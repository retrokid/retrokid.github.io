# Aseprite Help

Aseprite lets you create 2D animations for videogames. From sprites, to pixel-art, retro style graphics, and whatever you like about the 8-bit and 16-bit era.

Here you will find some help, tutorials, and little tips to use Aseprite and start getting the best from it from the very beginning. If you have some questions you can start looking at the Frequently Asked Questions.

To get started, you can print the Quick Reference. It contains several keyboard shortcuts, so it could be handy to have it at your side.

### Table of content:

- Basics: General concepts, elements in the window, expected workflow, etc.
	- Workspace
	- Workflow
	- Sprite
- Image & Sprite:
	- Create a new Sprite or Open an existing one
	- Resize Sprite
	- Color Mode & Color Profile
	- Save Your Work
- Animation: How to create animations & manipulate frames
	- Onion Skinning
- Layers: How to handle several layers to compose images
- Selecting: How to select
- Drawing: How to start drawing
	- Zoom
- Transformations:
	- Flip
	- Canvas
	- Resize
	- Rotate
- Exporting:
	- Sprite Sheets
	- Command Line Interface (CLI)
- Customization
	- Preferences
	- Extensions
	- Scripting
- Troubleshooting:
	- Data Recovery
	- Reset Preferences
	- Debug Option

## Basics

Here you can learn the basic principles behind Aseprite.

In Aseprite, a sprite consists of a sequence of frames and a stack of layers. The intersection of frames and layers creates an array of editable graphic cels with images/pixels that can be edited with the sprite editor. Layers, frames, and cels are visible in the timeline:

![sprite-components-png](sprite-components.png)

###  Basic Elements of a Sprite 

A frame is a single still image in a sprite. Adding and altering frames creates a sequence of images called an animation. The details of how Aseprite cycles through frames is described in greater detail in the animation section. Frames are represented horizontally in the timeline, from left to right.

Each frame's image is produced from a stack of one or more layers, represented in order from bottom to top on the timeline. Layers at the bottom of the timeline are drawn first, and every subsequent layer is added over top of it. Layers assist you by dividing a single complex image into separate graphic component parts.

Each frame-layer intersection is called a cel. The contents of any specific cel may be moved, edited, and deleted without affecting the contents of other cels, which make them ideal for isolating and editing specific elements of a graphic while preserving parts that do not change.

###  Workflow 

The basic workflow is:

- Create a new sprite from File > New menu.
- Draw with pencil tool ![pencil-tool-png](pencil-tool.png) using `Left click` or `Right click`, and pick colors from the color bar using those same buttons.
- Save your work from File > Save menu as an `.ase` file to preserve all your image information (layers, frames, etc.. Also stores certain workspace preferences.).
- Export your sprite as a `.gif` file to publish your image on a website, as a numbered sequence of individual `.png` files (one file per frame), or as a single `.png` file with all frames arranged in a single row or column, or as a 2-D sprite sheet.

See the workspace to learn more about the elements of the window. See the workflow section for more details.

### A hand on the keyboard 

You should put your left hand on the keyboard (or your right hand if you are left-handed). As there are some handy keyboard shortcuts, you can use them from the very beginning to make better use of Aseprite:

- Keys `1`, `2`, `3`, `4`, `5`, and `6` can be used to change the zoom (you can use the Mouse Wheel to change zoom too).
- `B` key is the Pencil tool, and `M` the rectangular marquee, maybe the most common tools that you will use.
- `Alt+Right click` samples the Background Color.
- The `Ctrl` key (or `⌘` on macOS) can be used to select the Move tool ![move-tool-png](move-tool.png). With it you can easily select or move layers.
- The `Tab` key hides and reveals the timeline. If your timeline is ever missing, this is the fastest way to reveal it!
- Holding `Spacebar` as you `Left click+Drag` will pan your view of the sprite you are currently editing. This is useful when you're working on large graphics or are zoomed-in.

### Alternative functions for right-click 

By default, `Right click` paints with the Background Color, but you can change this configuration from Edit > Preferences > Editor.


























