[back to main](https://github.com/kwan22/consistency/blob/main/README.md)

# The science of consistency

The following discusses some common patterns that I use in my own speedruns. The discussion will be highly technical, including frame data, pixel/speed values, inner game mechanics, etc. to justify the logic. That said, the recurring themes are 
1. maximizing use of the game's leniency mechanics,
2. making small time sacrifices to relax precision and/or simplify inputs.

- [Leniency](#leniency)

## Leniency

Leniency is a fundamental property of speedrunning and is commonly expressed in terms of a window: the range of timings or spacings you can perform an action and get the desired outcome. It is essentially a measure of your allowed margin for error. In Celeste speedrunning, frame windows are more prelevant than pixel windows, and many pixel windows are just translated into frame windows via speed. Not all frame windows of equal value are of the same difficulty. Context plays a major role in the perceived difficulty of a frame window. For example, extension timing is one of the easiest 5f windows to learn because the jump timing is anchored by the dash input. You are the one pressing dash, and then you learn the rhythm to press jump. However, hitting a random, unpracticed 5f window is quite difficult. 

More generally, a frame window becomes easier to learn if it is **normalized** by an anchor. For extension timing, the dash input is the normalization anchor. Other useful normalized timings might be max height and 12f jump. Visual cues are also a common anchor to tie down a frame window to something more tangible. With enough experience, you can project Madeline's motion to develop an intuition for when Madeline will reach a visual cue to guide your timing. Both visual cues and muscle memory can be combined as well. Transition buffering is a fundamental timing that is based on a visual cue of the screen scroll coming to a stop. Some might also just "feel out" the visual motion of the screen scroll as well. [Habits level 3](https://github.com/kwan22/habits/blob/main/level3.md) showcases several examples that uses basic leniency and normalization techniques to enable movement options. 

Some frame windows can be frustrating to deal with if not all frames within the window are equal. 5a archimedes is a classic example: there are 4 viable updash frames, but each one requires a different response. Frame windows are much nicer if they give the same outcome. I define some concepts about actions in general here:
- Convergent: small changes converge to the same outcome
- Divergent: small changes diverge into different outcomes

### Convergence and divergence
Normalization is a common way to approach convergence, and the two often go hand-in-hand. Transitions are the perhaps the best example, setting Madeline's position to exactly on the boundary and rounding off subpixels on both position and speed. Small differences in crossing a transition can converge onto the exact same game state. The normalizing properties of transitions enable many setups that would otherwise be nearly impossible to make consistent. Bubbles also behave similarly, normalizing both x and y position and speed.

Case study: hypering before transition (discretized hyper trajectory, 2a downright cb, 3b start 2, 6b falling super diags, 6b reprieve, 7a 500m cornerslip, 7a 2500m gem)

Convergence can still be achieved without a true normalization process, depending on the scope. Broadly, most continuous frame windows lends themselves to convergence, where each frame might be slightly different but sufficiently similar to make progress to the next sequence. Cornercorrection and floorsnapping often give sufficiently similar game states for many scenarios, but some exceptions exist due to particular geometries or subpixels. For example, cornercorrection is required to extend a 2-tile horizontal dash, while floorsnapping will fail to extend. Cornercorrection also does not round off subpixels, occasionally leading to some niche scenarios such as the 3a shaft demo in ARB. 

Buffering is another common way to add convergence: inputs of different timings generate the exact same result. While chains of consecutive buffers can quickly become complicated, a few isolated buffers showcase the concept of convergence quite well.

DashCD setups: 7a 2500m arb, 6a hollows, 8a hotm-h, 5b

wavedash for height setup: 5a heart, 8a itc hyper cb

Half-gravity can expand convergence by extending the duration Madeline exists at a given y-position. This is typically used for line-ups with max-height jumps, e.g. 3a shaft demo and various other demos out of a max height hyper. On the other hand, half-gravity can be detrimental sometimes, by introducing deadframes on some strats, or more fundamentally, adding unnecessary airtime. [Avoiding half-gravity can also be convergent on jumps and wallbounces,](https://www.youtube.com/watch?v=82gpR9rozdE), where releasing jump on different frames gives the exact same vertical trajectory. A good deal of RTA movement optimization comes from putting yourself in a position to enjoy the luxury of a convergent jump release timing. 

Divergence is frequently avoided but sometimes manageable, such as the aforementioned 5a archimedes. High-speed (grounded ultra) coyote often lends itself to divergence: the strat requires high-speed to enable longer-distance coyote, but the high speed inherently spreads out your possible trajectories (2a start under). In some cases, the different trajectories are reactable (5a rescue). Releasing forward to slow down to create a larger framewindow for a wallbounce (or other similar actions) can be divergent: releasing forward at different times ends up with different viable timings for the updash. 

Case study: 5a start forward wave

Normalizing the trajectory to slow down to enlarge a frame window can be done in many other ways. 

1a zkad route wave?

4a granny ultra

3a hub2

3a towels wallkick

3a final transition hyper

6b multiboost: convergent jump release on dash crystal freeze frame

Dash attack leniency

3a shaft

7a flag 1

## Variable reduction
