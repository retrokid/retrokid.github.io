# Configuring Whether Animations Play During the Transition

-----------------------------

### Overview

The `pausesIncomingScene` and `pausesOutgoingScene` properties on the transition object define which animations are played during the transition. By default, both scenes are paused during the transition. However, you might want to enable animation on either scene during the transition.

Figure 1 illustrates which frames of the incoming and outgoing scenes are displayed on screen during a three frame transition with different permutations of `pausesIncomingScene` and `pausesOutgoingScene`.

###### Figure 1 Frame progression during transitions

![051-sktransition-configuring-whether-animations-play-during-the-transition-001](/images/051-sktransition-configuring-whether-animations-play-during-the-transition-001.png)

For example, consider the code again in . Because the button is going to run an action, this code expects the outgoing scene to be animated. But perhaps the incoming scene should not animate its content until the transition completes. Adding the code in Listing 1 has the desired effect.

###### Listing 1 Pausing frame processing during a transition

```swift
reveal.pausesOutgoingScene = true;
reveal.pausesIncomingScene = false;
```

----------------------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/spritekit_documentation/051-sktransition-configuring-whether-animations-play-during-the-transition.md)

[download this page as .pdf](https://github.com/retrokid/retrokid.github.io/raw/master/tech_notes/spritekit_documentation/051-sktransition-configuring-whether-animations-play-during-the-transition.pdf)

[back to SpriteKit documentation](./spritekit-documentation)
