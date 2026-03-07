[back to main](https://github.com/kwan22/consistency/blob/main/README.md)

# The science of consistency

<img src="./media/science/7b_1500m_1.png" width="960"/>

The following discusses some common patterns that I use in my own speedruns. The discussion will be highly technical, including frame data, pixel/speed values, inner game mechanics, etc. to justify the logic. That said, the recurring themes are 
1. maximizing use of the game's leniency mechanics,
2. making small time sacrifices to relax precision and/or simplify inputs.

- [Leniency](#leniency)

## Leniency

Leniency is a fundamental property of speedrunning and is commonly expressed in terms of a window: the range of timings or spacings you can perform an action and get the desired outcome. It is essentially a measure of your allowed margin for error. In Celeste speedrunning, frame windows are more prelevant than pixel windows, and many pixel windows are just translated into frame windows via speed. Not all frame windows of equal value are of the same difficulty. Context plays a major role in the perceived difficulty of a frame window. For example, extension timing is one of the easiest 5f windows to learn because the jump timing is anchored by the dash input. You are the one pressing dash, and then you learn the rhythm to press jump. However, hitting a random, unpracticed 5f window is quite difficult. 

More generally, a frame window becomes easier to learn if it is **normalized** by an anchor. For extension timing, the dash input is the normalization anchor. Other useful normalized timings might be max height and 12f jump. Visual cues are also a common anchor to tie down a frame window to something more tangible. With enough experience, you can project Madeline's motion to develop an intuition for when Madeline will reach a visual cue to guide your timing. Both visual cues and muscle memory can be combined as well. Transition buffering is a fundamental timing that is based on a visual cue of the screen scroll coming to a stop. Some might also just "feel out" the visual motion of the screen scroll as well. [Habits level 3](https://github.com/kwan22/habits/blob/main/level3.md#basic-leniency-and-normalization) showcases several examples that uses basic leniency and normalization techniques to enable movement options. Besides buffering, the game offers many other leniency mechanics, including coyote, cornercorrection/floorsnap, liftboost timer, to name a few. Without these, Celeste would be a much less forgiving game to play. These leniency mechanics frequently come into play in prescribing an RTA-viable frame window for many actions.

Some frame windows can be frustrating to deal with if not all frames within the window are equal. 5a archimedes is a classic example: there are 4 viable updash frames, but each one requires a different response. Frame windows are much nicer if every frame within gives the same outcome. I define some concepts about actions in general here:
- Convergent: small changes in the action result in the same outcome
- Divergent: small changes in the action propagate into different outcomes
  
Changes in action generally refer to differences in timing or spacing. These are essentially expressions of sensitivity: convergence means the outcome is insensitive to small changes in the action. This describes a more general concept of a frame window: the window defines how small those "small changes" need to be. Outside of the frame window, the outcome diverges into different possibilities. What makes Celeste movement so interesting in this regard is that  leniency mechanics combined with the discretization of the game physics may enable absolute convergence: different actions can converge onto the exact same game state. This enables some movement that may seem ridiculously precise to become RTA-viable. For this reason, I elected to use the term "convergence" over "sensitivity".

## Convergence
Normalization is a common way to approach convergence, and the two often go hand-in-hand. Transitions are the perhaps the best example, setting Madeline's position to exactly on the boundary and rounding off subpixels on both position and speed. Small differences in crossing a transition can converge onto the exact same game state. The normalizing properties of transitions enable many setups that would otherwise be difficult to make consistent. Bubbles also behave similarly, normalizing both x and y position and speed.

Convergence can still be achieved without a true normalization process, depending on the scope. Broadly, most continuous frame windows lend themselves to convergence, where each frame might be slightly different but sufficiently similar to make progress to the next sequence. Cornercorrection and floorsnapping often give sufficiently similar game states for many scenarios, but some exceptions exist due to particular geometries or subpixels. For example, cornercorrection is required to extend a 2-tile horizontal dash, while floorsnapping will fail to extend. Cornercorrection also does not round off subpixels, occasionally leading to some niche scenarios such as the 3a shaft demo in ARB. 

### Buffering
Buffering is perhaps the epitome of convergence: inputs of different timings generate the exact same result. While chains of consecutive buffers can quickly become complicated and arguably divergent, isolated buffers showcase the concept of convergence quite well.

wavedash for height setup: 5a heart, 8a itc hyper cb, wave vs hyper meme

### The pre-transition hyper

Hypering just before a transition is highly convergent across different starting x-positions because of the structure of the hyper trajectory and the properties of transitions. Some seemingly pixel-perfect or subpixel-precise strats involving a hyper before transition frequently have a pixel range that are a multiple of ~5 in which they work because this convergence.

<details>
  <summary>Some numbers about hypers</summary>
  <img src="./media/science/hyper_angle.png" width="360"/>
  
  The hyper has a factor ~6 difference in horizontal vs vertical speed during the 12f of jump timer. The hyper moves about 5 px/frame horizontally, and air friction is small at the startup, decrementing the horizontal speed by about 1.5% per frame in the first several frames. On the other hand, the hyper moves less than 1 px/frame vertically (with no loss to gravity during jump timer). The consequence of this is that the hyper stays at the nearly the same x-speed and y-position over a large x-range. Horizontal transitions set Madeline to an exact x-position, and round off decimals (in px and px/s units) on y-position and both components of speed. The possible trajectories of a hyper upon transition are thus discretized and can be (almost) exactly prescribed based on horizontal distance from said transition. The discretization happens in steps of about every 5 pixels because hyper x-speed is ~5 px/frame. Increments in x-speed and y-pos are small, so adjacent hyper trajectories are frequently sufficiently similar to execute a strat. 
</details>

The plot below shows the possible hyper trajectories, y-position and x-speed (u), upon a horizontal transition as a function of distance from transition. Each step represents a frame, and all positions up to the next step converge to the exact same trajectory. This is the essence of sensitivity analysis. In this case, the outcomes (y, u) are weakly sensitive to the changes in action (x). In math speak, the sensitivity coefficients dy/dx and du/dx are small. 

  <img src="./media/science/pretrans_hyper.png" width="480"/>

  > In-game TAS tools can usually measure the hyper trajectory by seeing the DashCD or Jump timer values during transition as there is a 1-1 correspondence.

Many strats call for a jump release upon transition, which automatically converges y-speeds. Even for strats that do not release jump on transition, the y-speed will still be the same as long as jump timer is active until the next action. One caveat on the y-position is the possibility of y-subpixel offsets causing rounding differences, which shows up occasionally on a few strats but can be controlled with deliberate movement. 

  <img src="./media/science/2a_drcb.png" width="960"/> <br>
  The movement to set up the downright cb in 2a-Intervention can be convergent across initial starting hyper positions. 10 px window implies 2 viable hyper trajectories. Incidentally, one of the hyper trajectories is more forgiving than the other, but both are sufficient to set up the rest of the strat with reasonable leniency. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1162859316479537265). 
  
  <img src="./media/science/3b_start2_labeled.png" width="480"/> <br>
  The first cb in 3b Start-2 has a 25 pixel range to get a good cb because of this convergence. There are 5 possible hypers to cross the transition (blue) and get a good cb, spread out across 25 pixels of initial x-pos (x0, red). For the outcome of "good first cb", the pre-transition hyper is highly convergent across different initial starting positions. That said, the following upright cb being successful has some divergence from x0 because of the slightly different speeds mattering. In general, the longer a sequence is, the more opportunities there are for divergence to arise, as small differences in intial conditions propagate to increasingly larger outcomes with each segment. Thankfully, Celeste provides many anchors for normalization, making chaining many short sequences amenable to convergence. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1232274832390098974).
  
  <img src="./media/science/6b_reprieve_3_entry.webp" width="480"/> <br>
  Fastfalling directly into the 1st bumper in 6b Reprieve-3 seems absolutely insane without the right setup. Fortunately, we have our friend, the convergent pre-transition hyper, to help us out. Incidentally, optimal movement at the end of Reprieve-2 sets this up perfectly: buffered right dash out of Badeline recoil sets us up on the left edge of the 5 pixel window of the winning hyper trajectory. That said, because the landing is on the left edge, there is some room to the right of the optimal landing that is still viable. For example, sliding forward slightly on landing via being late on buffering instant hyper (up to 3f) still gives the exact same hyper trajectory. Not that a speedrunner should be aiming for this, it is just a leniency that exists. The more speedrunner-relevant consequence is that differences in Badeline recoil between entry and death can be resolved by simply not fastfalling after the right dash, as not fastfalling lands us slightly further to the right but still within the 5px window. [Link to stratpost](https://discord.com/channels/403698615446536203/1137847274609848463/1137847278363738233). 

  <img src="./media/science/7a_500m_cornerslip.webp" width="480"/> <br>
  A personal variation I haven't seen anyone else do: I find a pre-transition hyper to be much more consistent in setting up the cornerslip than transition hyper. While transition hypers are well-known for their normalization properties, a major variable in using a transition hyper here is the jump release timing. Pre-transition hyper shifts the variance from jump release timing to hyper positioning, which as we've been saying, is highly convergent. More speed loss to air friction also may mean a larger window for the cornerslip itself. All this may be at the cost of a few frames compared to the transition hyper. In general, the transition hyper is amazing on horizontal convergence, but less so on vertical for short hypers, as each frame of jump release gives a different outcome (e.g. the landing position for the bhop on this strat). The pre-transition hyper suffers a small loss of horizontal convergence, but is far more vertically convergent for short hypers. The rest of the strat still has its difficulties, but I find this variation more accessible.

<details>
  <summary>Sensitivity comparison between hypers and supers (warning: calculus)</summary>

  In general, the sensitivity coefficient is expressed as a derivative of the outcome with respect to the input (action). With the power of calculus, we can quickly do this sensitivity analysis of the hyper trajectory (y and u) to initial starting position (x) without jumping through all the hoops of graphs and long-winded explanations. Let v = y-speed = dy/dt, u = x-speed = dx/dt

  dy/dx = dy/dt  * dt/dx <br>
  dy/dt = v, dt/dx = 1/u <br>
  dy/dx = v/u

  du/dx = du/dt * dt/dx <br>
  du/dt is just air friction, which is a constant <br>
  du/dx ~ 1/u

  Comparing hypers and supers, hypers have lower v and higher u, so it can be easily seen that dy/dx and du/dx are larger for supers compared to hypers, thus one can expect pre-transition supers to be more sensitive (less convergent) on starting x-position. The main missing piece of this analysis is the rounding and discretization that happens on transition that enables certain strats. There are a few spots where pre-transition supers enable certain strats, though these are less common than their hyper counterparts.

  <img src="./media/science/6b_falling_super_diags.webp" width="480"/>
  <img src="./media/science/7a_1500m_super.webp" width="480"/>
  
</details>

### Half-gravity

  <img src="./media/science/7b_heart_demo_crop.png" width="480"/>

Half-gravity can expand convergence by extending the duration Madeline exists at a given y-position. This typically manifests in line-ups with max-height jumps, e.g. 3a shaft demo and a whole class of demos out of a max height hyper. Fundamentally, half-gravity can improve frame-windows by keeping us in the same y-position for an extended period of time. On the other hand, half-gravity can be detrimental sometimes, by introducing deadframes on some strats, or more fundamentally, adding unnecessary airtime. [Avoiding half-gravity can also be convergent on jumps and wallbounces,](https://www.youtube.com/watch?v=82gpR9rozdE), where releasing jump on different frames gives the exact same vertical trajectory. A good deal of RTA movement optimization comes from putting yourself in a position to enjoy the luxury of a convergent jump release timing. For a speedrunner's perspective, the main takeaway is "just hold jump" to use half-gravity, or "find the 6f jump release window" to avoid half-gravity with convergence. 

## Divergence

Divergence is often difficult to deal with, but is sometimes manageable, such as the aforementioned 5a archimedes. High-speed (grounded ultra) coyote often lends itself to divergence: the strat requires high-speed to enable longer-distance coyote, but the high speed inherently spreads out your possible trajectories (2a start under). In some cases, the different trajectories are reactable (5a rescue). In general, high-speed movement inherently lends itself quickly to divergence because each subsequent frame leads to a large change in game state by definition of high speed.

In the name of consistency, the general goal is to mitigate divergence as much as possible, usually by a setup that costs a small bit of time. One way to mitigate divergence is to slow down to expand a frame window. Releasing forward to slow down to create a larger framewindow for a wallbounce (or other similar actions) can itself be divergent though: releasing forward at different times ends up with different viable timings for the updash. However, there are many ways to normalize a trajectory to slow down for different objectives, thereby increasing a frame window. Many buffer setups work this way, though buffering is not the only means to this end.

Case study: 5a start forward wave

5a eyeball dashcd speed manip

DashCD setups: 7a 2500m arb, 6a hollows, 8a hotm-h, 5b heart

1a zkad route wave?

4a granny ultra

3a hub2

3a towels wallkick

3a final transition hyper

6b multiboost: convergent jump release on dash crystal freeze frame

Dash attack leniency

3a shaft

7a flag 1

Buffer chains, 7arb 1500m triple demo, yujene depths final spam

## Variable reduction
