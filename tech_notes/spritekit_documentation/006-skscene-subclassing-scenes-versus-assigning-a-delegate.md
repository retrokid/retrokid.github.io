# Subclassing Scenes Versus Assigning a Delegate

-------------------

Use a scene delegate to share app logic across various scenes.

### Overview

Often, your app subclasses `SKScene` to deliver gameplay. Your subclass usually:

- Lays out initial scene content
- Defines app logic that runs every frame
- Implements responder methods to handle keyboard, mouse, or touch events

An alternative pattern is to assign a `delegate` that handles `Responding to Frame-Cycle Events` instead. For example, if you make the view controller the delegate for your scene, it can use multiple scenes that share the same `SKSceneDelegate` implementations. The view controller participates in event handling and so it can respond to user input also.

> __Important:__
> On macOS, you need to set the window's `nextResponder` to your app's view controller because by default, the view is the first responder to user input events

----------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/006-skscene-subclassing-scenes-versus-assigning-a-delegate.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/006-skscene-subclassing-scenes-versus-assigning-a-delegate.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
