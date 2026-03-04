[back to main](https://github.com/kwan22/consistency/blob/main/README.md)

# The science of consistency

The following discusses some common patterns that I use in my own speedruns. The discussion will be highly technical, including frame data, pixel/speed values, inner game mechanics, etc. to justify the logic. That said, the recurring theme is making small time sacrifices to relax precision and/or simplify inputs and timings. Understanding the underlying technical details is not required to see this principle.

To set the tone, let's start with a basic, "spherical-cow" type of example. Suppose you want move horizontally past a ceiling for a wallbounce. How lenient is the updash? <br>
<img src="./media/science/7a_1500m_wallbounce.png" width="480"/> <br>
The faster you move, the faster you get there, but the less time you spend close enough to the wall such that a wallbounce is possible. Below shows the approximate relationship between speed and leniency of the wallbounce. <br>
<img src="./media/science/generic_wallbounce.png" width="480"/> <br>
The colored boxes indicate nominal speed ranges that you would typically have from different movement options. For reference, a 5f window is the leniency of extension and buffer timing. You can see that any appreciable amount of speed quickly makes the wallbounce difficult to line up properly. 

Every RTA setup for a strat relies on creating some leniency in precision that is almost always obtained by sacrificing a small amount of time. Think 3a shaft demo: we spend time to line up (either manually or using certain movement combos) on a certain pixel on the wall such that a max height climbjump gives a reasonable window for the demo. The following showcases ideas and examples on ways I play the fundamental tradeoff between speed and precision.

- [Convergence and divergence]

## Convergence and divergence

Leniency is commonly expressed in terms of a frame window, but not all frame windows of equal value are the same difficulty. Context plays a major role in the perceived difficulty of a frame window. For example, extension timing is one of the easiest 5f windows to learn because the jump timing is anchored by the dash input. You are the one pressing dash, and then you learn the rhythm to press jump. However, hitting a random, unpracticed 5f window is quite difficult. Try this with a stopwatch: start and stop based on extension timing muscle memory and see how often you stop between 0.17 and 0.25s: I find this pretty consistent. Now try a randomly selected 80ms window, say, between 0.70-0.78, or 1.51-1.59. The numbers don't matter, just pick something arbitrary and unpracticed. I found this to be quite difficult without practicing, but much more approachable after a few tries of the same timing by finding a rhythm for the timing. 

More generally, a frame window becomes easier to learn if it is **normalized** by an anchor. For extension timing, the dash input is the normalization anchor. Other useful normalized timings might be max height and 12f jump. Visual cues are also a common anchor to tie down a frame window to something more tangible. With enough experience, you can develop an intuition for when Madeline will reach a visual cue to guide your timing. Both visual cues and muscle memory can be combined as well. Transition buffering is a fundamental timing that is based on a visual cue of the screen scroll coming to a stop. Some might also just "feel out" the visual motion of the screen scroll as well.

## Variable reduction
