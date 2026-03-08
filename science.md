[back to main](https://github.com/kwan22/consistency/blob/main/README.md)

# The science of consistency

<img src="./media/science/7b_1500m_1.png" width="480"/>

The following discusses some common patterns that I use in my own speedruns. The discussion will be highly technical, including frame data, pixel/speed values, inner game mechanics, etc. to justify the logic. That said, the recurring themes are 
1. Maximizing use of the game's leniency mechanics.
2. Understanding the variables that your objective is most sensitive to.
3. Eliminating variables to reduce input complexity and remove failure modes.
4. Making small time sacrifices to relax precision and simplify inputs.

Many examples are provided and discussed in great technical detail. These details are provided to illustrate the kinds of patterns I like to look for and apply to my own gameplay.

- [Leniency and convergence](#leniency-and-convergence)
- [Buffering and DashCD](#buffering-and-dashcd)
- [Pre-transition hyper](#Pre-transition-hyper)
- [Half gravity](#half-gravity)
- [Mitigating divergence](#mitigating-divergence)

## Leniency and convergence

Leniency is a fundamental property of speedrunning and is commonly expressed in terms of a window: the range of timings or spacings you can perform an action and get the desired outcome. It is essentially a measure of your allowed margin for error. In Celeste speedrunning, frame windows are more prelevant than pixel windows, and many pixel windows are just translated into frame windows via speed. Not all frame windows of equal value are of the same difficulty. Context plays a major role in the perceived difficulty of a frame window. For example, extension timing is one of the easiest 5f windows to learn because the jump timing is anchored by the dash input. You are the one pressing dash, and then you learn the rhythm to press jump. However, hitting a random, unpracticed 5f window is quite difficult. 

More generally, a frame window becomes easier to learn if it is **normalized** by an anchor. For extension timing, the dash input is the normalization anchor. Other useful normalized timings might be max height and 12f jump. Visual cues are also a common anchor to tie down a frame window to something more tangible. With enough experience, you can project Madeline's motion to develop an intuition for when Madeline will reach a visual cue to guide your timing. Both visual cues and muscle memory can be combined as well. Transition buffering is a fundamental timing that is based on a visual cue of the screen scroll coming to a stop. Some might also just "feel out" the visual motion of the screen scroll as well. [Habits level 3](https://github.com/kwan22/habits/blob/main/level3.md#basic-leniency-and-normalization) showcases several examples that uses basic leniency and normalization techniques to enable movement options. Besides buffering, the game offers many other leniency mechanics, including coyote, cornercorrection/floorsnap, liftboost timer, to name a few. Without these, Celeste would be a much less forgiving game to play. These leniency mechanics frequently come into play in prescribing an RTA-viable frame window for many actions.

Some frame windows can be frustrating to deal with if not all frames within the window are equal. Frame windows are much nicer if every frame within gives the same outcome. I define some concepts about actions in general here:
- Convergent: small changes in the action result in the same outcome
- Divergent: small changes in the action propagate into different outcomes <br>
  
Changes in action generally refer to differences in timing or spacing. These are essentially expressions of sensitivity: convergence means the outcome is insensitive to small changes in the action. This describes a more general concept of a frame window: the window defines how small those "small changes" need to be. Outside of the frame window, the outcome diverges into different possibilities. What makes Celeste movement so interesting in this regard is that leniency mechanics combined with the discretization of the game physics may enable absolute convergence: different actions can converge onto the exact same game state. This enables some movement that may seem ridiculously precise to become RTA-viable. For this reason, I elected to use the term "convergence" over "sensitivity".

  <img src="./media/science/5a_archimedes_crop.png" width="480"/> 

>5a "Archimedes": the updash is a 4f window, but each frame requires a different follow-up.

Normalization is a common way to approach convergence, and the two often go hand-in-hand. Transitions are the perhaps the best example, setting Madeline's position to exactly on the boundary and rounding off subpixels on both position and speed. Small differences in crossing a transition can converge onto the exact same game state. The normalizing properties of transitions enable many setups that would otherwise be difficult to make consistent. Bubbles also behave similarly, normalizing position and speed and having a well-determined trajectory.

Convergence can still be achieved without a true normalization process, depending on the scope. Broadly, most continuous frame windows lend themselves to convergence, where each frame might be slightly different but sufficiently similar to make progress to the next sequence. Cornercorrection and floorsnapping often give sufficiently similar game states for many scenarios, but some exceptions exist due to particular geometries or subpixels. For example, cornercorrection is required to extend a 2-tile horizontal dash, while floorsnapping will fail to extend. Cornercorrection also does not round off subpixels, occasionally leading to some niche scenarios such as the 3a shaft demo in ARB. 

## Buffering and DashCD
Buffering is perhaps the epitome of convergence: inputs of different timings generate the exact same result. While chains of consecutive buffers can quickly become complicated and arguably divergent, sparse buffers showcase the concept of convergence quite well. Common, visually obvious examples include transition buffers, cb and cornerkick setups, and pause-buffering. 

DashCD is one of the less visually obvious mechanics but has incredible potential in creating buffer setups. Besides the strats that essentially require it, a lot of leniency on otherwise hard strats can be gained by putting yourself in a position to buffer out of DashCD. Setting up the positioning may cost a small amount of time, opening an avenue to play the speed vs precision tradeoff game. Below are some examples where understanding DashCD is useful.

---

  Normally with a neutral transition super, the updash on this wallbounce in the berry route of 2500m is a 3f window. By carefully positioning the rightdash in the previous room, this updash can instead be transformed into a buffer (5f). Furthermore, there is a 1-1 correspondence between each of the possible updashes and the rightdashes upon transition (blue bar). With dash speed moving at 4 px/frame and 3 possible rightdashes (DashCD frames upon transition), there are thus 4 px/frame x 3 frames = 12 pixels from which the rightdash can be started and the updash is bufferable. The pixel window can be converted into a frame window assuming we are walking thru the window: with walking speed at 1.5 px/frame, it's an 8f window to time the rightdash. <br>
  <img src="./media/science/7arb_2500m_dashcd.webp" width="480"/> <img src="./media/science/7arb_2500m_dashcd_labeled.png" width="480"/> 
  
  Each of the colored red/green/yellow boxes corresponds to a rightdash+buffered updash pair. Dashing in the leftside red box means the buffered updash comes out on the rightside red box, etc. By starting the rightdash in the 12px window, we remove the failure mode of updashing too early. The updash itself is bufferable, but depending on where the rightdash is, the updash may have extra leniency frames. For example, if rightdashing from the left red box, the updash may be from the right red box (5f buffer), or it can also be slightly late: 1f late updashes on the right green box, 2f late updashes on the right yellow box. Rightdashing from the left yellow box has no added leniency frames beyond the buffer, as the 1st possible updash is also the last one. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1086837734607441931).

---

Coincidentally, the ultra off the coreblock in 8a-HOTM-H has almost exactly the same structure as the 2500m ARB example above. It's a 3f window to downright after a buffered transition hyper to avoid negative liftboost. That 3f can then be transformed into a buffer out of DashCD by carefully starting the demo in a 12px window. I won't rehash all the details as it's similar to above, but I will mention some nuances. The failure mode of not properly buffering the transition hyper is more relevant here compared to the 2500m ARB example above. The choice of demo vs downright also matters from a leniency perspective. Horizontal dashes move 4 px/frame, and a downright moves ~3.4 px/frame. The higher speed from a horizontal dash effectively expands the pixel range over which this concept works, i.e. the dash timing upon transition is less sensitive to starting position when the dash speed is faster (see sensitivity analysis below for a more generalized form of this). [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1380229565674164317). <br>
  <img src="./media/science/8a_hotmh_ultra.webp" width="480"/> 

<img src="./media/science/5b_mm_final.webp" width="480"/> <img src="./media/science/6a_hollows_kevinslide.webp" width="480"/> 

> The same principle applies to other dash tech. These downrights can be made much more lenient by starting the instant hyper before transition from the right spot.

---

Controlling DashCD is useful to control speed on a grounded ultra. A personal variation of mine is to use DashCD to control my speed at the start of the eyeball room of 5A. The most normalized entry for the eyeball room is to transition hyper and buffer a downright, but the speed of the buffered downright and ensuing Theo ultra depend on how much DashCD remains upon entering the room. Making the cycle requires good speed generation and preservation. Good speed generation means good Theo ultras, and good speed preservation, in practice, means fitting in has many bhops as possible. I particularly struggled with fitting in small bhops near the beginning, so instead I opted to line up my DashCD entering the eyeball room itself such that the first Theo ultra is as fast as possible given a buffered transition hyper into downright out of DashCD, and simplify the beginning of the room with just 1 big bhop instead of 2 small bhops that can easily go wrong. In terms of speed generation, dashing from as far away as possible (entering with the lowest DashCD) leads to the least loss to air friction and consequently the fastest ultra upon a buffered downright. However in this case, the lip at the start of the eyeball room presents some complications. If DashCD is too low when entering eyeball room, there is not enough height+distance covered to avoid the lip with a buffered hyper+downright, resulting in a grounded ultra on the upper platform before Theo (sometimes it still works but I wouldn't count on it). <br>
<img src="./media/science/5a_eyeball_dashcd.webp" width="480"/> <img src="./media/science/5a_eyeball_dashcd_labeled.png" width="480"/> 

I settled with aiming for DashCD(5) when entering eyeball room: DashCD(4) creates more speed and is easier to make the fast cycle, DashCD(3) is too far and runs into the grounded ultra issue, and DashCD(6) works but is just a tad more difficult. Incidentally, DashCD(4) and over are also allowed to be slightly late on buffering the transition hyper, adding a hair of leniency on that end. Recall that each dash timing corresponds to a 4px range of the starting demo because of the 4px/frame speed of the horizontal demo. To translate these numbers into something more practical: I aim to be near the left edge of the platform (red dashed line). A nice feedback cue is if I see the 2nd dash silhouette (indicated by the blue arrow) appear before transition: this indicates DashCD(5) or less. If I don't see the 2nd dash silhouette appear during transition, I am more mentally prepared to have less speed on the first Theo ultra. A critical side effect is that by aiming for a particular DashCD, I am reducing the possible initial trajectories I will have at the start of the eyeball room. 

## Pre-transition hyper

Hypering just before a transition is highly convergent across different starting x-positions because of the structure of the hyper trajectory and the properties of transitions. Some seemingly pixel-perfect or subpixel-precise strats involving a hyper before transition frequently have a pixel range that are a multiple of 5 in which they work because this convergence.

<img src="./media/science/hyper_angle.png" width="360"/>
  
  The hyper has a factor ~6 difference in horizontal vs vertical speed during the 12f of jump timer. The hyper moves about 5 px/frame horizontally, and air friction is small at the startup, decrementing the horizontal speed by about 1.5% per frame in the first several frames. On the other hand, the hyper moves less than 1 px/frame vertically (with no loss to gravity during jump timer). The consequence of this is that the hyper stays at the nearly the same x-speed and y-position over a large x-range. Horizontal transitions set Madeline to an exact x-position, and round off decimals (in px and px/s units) on y-position and both components of speed. The possible trajectories of a hyper upon transition are thus discretized and can be (almost) exactly prescribed based on horizontal distance from said transition. 

The plot below shows the possible hyper trajectories, y-position and x-speed (u), upon a horizontal transition as a function of distance from transition. Each step represents a frame, and all positions up to the next step converge to the exact same trajectory. The outcomes (y, u) are weakly sensitive to the changes in action (x). In math speak, the sensitivity coefficients dy/dx and du/dx are small. The consequence of this is that pre-transition hyper trajectories are discretized such that they increment every ~5 pixels away from transition. Because of the low sensitivity, adjacent hyper trajectories are often similar enough where many strats work across multiple 5-pixel windows. <br>
  <img src="./media/science/pretrans_hyper.png" width="480"/>

  > In-game TAS tools can usually measure the hyper trajectory by seeing the DashCD or Jump timer values during transition as there is a 1-1 correspondence.

Many strats call for a jump release upon transition, which automatically converges y-speeds. Even for strats that do not release jump on transition, the y-speed will still be the same as long as jump timer is active until the next action. One caveat on the y-position is the possibility of y-subpixel offsets causing rounding differences, which shows up occasionally on a few strats but can be controlled with deliberate movement. Below shows examples where such hypers are useful.

---

  The beginning movement to set up the downright cb in 2a-Intervention can be convergent across initial starting hyper positions. A 10 px window indicates that there are 2 viable hyper trajectories. Incidentally, one of the hyper trajectories is more forgiving than the other, but both are sufficient to set up the rest of the strat with reasonable leniency. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1162859316479537265). <br>
  <img src="./media/science/2a_drcb.png" width="960"/>

---

  The first cb in 3b Start-2 has a 25 pixel range (red box) to get a good cb because of this convergence. There are 5 possible hypers to cross the transition (blue) and get a good cb, spread out across 25 pixels of initial x-pos (x0, red). For the outcome of "good first cb", the pre-transition hyper is highly convergent across different initial starting positions. That said, the following upright cb being successful has some sensitivity to x0 because of the slightly different speeds mattering. In general, the longer a sequence is, the more opportunities there are for divergence to arise, as small differences in intial conditions propagate to increasingly larger changes in outcomes. Thankfully, Celeste provides many anchors for normalization, making chaining many short sequences amenable to convergence. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1232274832390098974). <br>
  <img src="./media/science/3b_start_cb.webp" width="480"/> <img src="./media/science/3b_start2_labeled.png" width="480"/>

---
  
  Fastfalling directly into the 1st bumper in 6b Reprieve-3 seems absolutely insane without the right setup. Fortunately, we have our friend, the convergent pre-transition hyper, to help us out. Incidentally, optimal movement at the end of Reprieve-2 sets this up perfectly: buffered rightdash out of Badeline recoil sets us up on the left edge of the 5 pixel window of the winning hyper trajectory. That said, because the landing is on the left edge, there is some room to the right of the optimal landing that is still viable. For example, sliding forward slightly on landing via being late on buffering instant hyper (up to 3f) still gives the exact same hyper trajectory. Not that a speedrunner should be aiming for this, it is just a leniency that exists. The more speedrunner-relevant consequence is that differences in Badeline recoil between entry and death can be resolved by simply not fastfalling after the rightdash, as slowfalling lands us slightly further to the right but still within the 5px window. [Link to stratpost](https://discord.com/channels/403698615446536203/1137847274609848463/1137847278363738233). <br>
  <img src="./media/science/6b_reprieve_3_entry.webp" width="480"/>

---

  I personally find a pre-transition hyper to be much more consistent in setting up the cornerslip than transition hyper. While transition hypers are well-known for their normalization properties, a major variable in using a transition hyper here is the jump release timing. Pre-transition hyper shifts the variance from jump release timing to hyper positioning, which as we've been saying, is highly convergent. More speed loss to air friction also may mean a larger window for the cornerslip itself. All this may be at the cost of a few frames compared to the transition hyper. In general, the transition hyper is amazing on horizontal convergence, but less so on vertical for short hypers, as each frame of jump release gives a different outcome (e.g. the landing position for the bhop on this strat). The pre-transition hyper suffers a small loss of horizontal convergence, but is far more vertically convergent for short hypers. The rest of the strat still has its difficulties, but I find this variation more accessible. <br>
  <img src="./media/science/7a_500m_cornerslip.webp" width="480"/> 

---

<details>
  <summary>Sensitivity analysis: a comparison between hypers and supers</summary>

  In general, the sensitivity coefficient is expressed as a derivative of the outcome with respect to the input (action). We can perform sensitivity analysis of the hyper trajectory (y and u) to initial starting position (x) without jumping through all the hoops of graphs and long-winded explanations. Let v = y-speed = dy/dt, u = x-speed = dx/dt

  dy/dx = dy/dt  * dt/dx <br>
  dy/dt = v, dt/dx = 1/u <br>
  dy/dx = v/u

  du/dx = du/dt * dt/dx <br>
  du/dt is air friction, which is a constant <br>
  du/dx ~ 1/u

  This is all just a concise, mathematical way of expressing all the numbers I was discussing earlier. Comparing hypers and supers, hypers have lower v and higher u, so it can be seen that dy/dx and du/dx are larger for supers compared to hypers. Thus, one can expect pre-transition supers to be more sensitive (less convergent) on starting x-position. The main missing piece of this analysis is the rounding and discretization that happens on transition that enables certain strats, but this reflects the overall trend. There are a few spots where pre-transition supers enable certain strats, though these are less common than their hyper counterparts, mainly due to level layouts generally being more conducive to hypers over supers. <br>
  <img src="./media/science/6b_falling_super_diags.webp" width="480"/> <img src="./media/science/7a_1500m_super.webp" width="480"/>
  
</details>

## Half-gravity

  <img src="./media/science/3a_demo.png" width="480"/>  <img src="./media/science/7b_heart_demo_crop.png" width="480"/> <br>
  > Half-gravity can be either helpful or harmful for precise vertical alignment: retaining it is usually simple but avoiding it can be convergent.

Half-gravity can expand convergence by extending the duration Madeline exists at a given y-position. This typically manifests in line-ups with max-height jumps, e.g. 3a shaft demo and a whole class of demos out of a max height hyper. Certain actions and interactions apply autojump as well, that act as if we are holding jump to give us half-grav whether we want to or not. Fundamentally, half-gravity can improve frame-windows by keeping us in the same y-position for an extended period of time. On the other hand, half-gravity can be detrimental sometimes, by introducing deadframes on some strats, or more fundamentally, adding unnecessary airtime. [Avoiding half-gravity can also be convergent](https://www.youtube.com/watch?v=82gpR9rozdE), where releasing jump on different frames gives the exact same trajectory if timed correctly. A good deal of RTA movement optimization comes from putting yourself in a position to enjoy the luxury of a convergent jump release timing. For a speedrunner's perspective, the main takeaway is "just hold jump" to use half-gravity, or "find the 6f+ jump release window" to avoid half-gravity. 

The movement in this 3b start room hinges heavily on convergence. The first downwards cb by the spinners is set up with a buffered wallkick that induces ForceMove (more on this later). The last climbjump by the spikes is set up in a normalized manner, with a wide window for jump release that includes an even more lenient version of the 6f jump release window to mitigate half gravity. [Link to stratpost](https://discord.com/channels/403698615446536203/617809769322774533/1380402607612231783) <br>
<img src="./media/science/3b_start_jumprelease.webp" width="480"/>

## ForceMove

3a start post triplat

7a updraft flag17

7b 0m spring

## Mitigating divergence

Divergence is often difficult to deal with. High-speed (grounded ultra) coyote often lends itself to divergence: the strat requires high-speed to enable longer-distance coyote, but the high speed inherently spreads out your possible trajectories. For the under strat in 2a-start, the grounded ultra travels at about 6.5 px/frame. In theory there are up to 3 possible coyote hyper frames that are viable for the under strat, but these are spread out over almost 20 pixels. The end result is that the frame window for the upright is directly dependent on which coyote frame was reached. The first possible coyote frame gives a 1f window for the upright, the 2nd a 2f, and the 3rd (last) frame a 3f window. <br>
  <img src="./media/science/2a_start_under_composite.png" width="480"/>

In some cases, the different trajectories are reactable. For this high-speed strat in 5a Rescue, there are 4 viable coyote jump frames, but frames 1-2 and 3-4 require different responses. The major challenge here is reacting to which set you get. While you have over half a second to decide (during transition), it is certainly not easy to tell, especially with Madeline moving so fast and the 2nd/3rd frame perhaps looking similar to each other. <br>
  <img src="./media/science/5a_rescue_fast1.webp" width="480"/>   <img src="./media/science/5a_rescue_fast1_labeled.png" width="480"/> <br>
  <img src="./media/science/5a_rescue_fast2.webp" width="480"/>   <img src="./media/science/5a_rescue_fast2_labeled.png" width="480"/>

In general, high-speed movement inherently lends itself quickly to divergence because each subsequent frame leads to a large change in game state by definition of high speed. In the name of consistency, the general goal is to mitigate divergence as much as possible, usually by a setup that costs a small bit of time. One way to mitigate divergence is to slow down to expand a frame window. Releasing forward to slow down to create a larger framewindow, say for a wallbounce, can itself be divergent though: releasing forward at different times ends up with different viable timings for the updash. However, there are many ways to slow down to increase a frame window without increasing divergence. Below are several examples that I use.

 <img src="./media/science/generic_wallbounce.png" width="480"/> <br>
 > Average frame window for an updash to wallbounce as a function of horizontal speed passing the wall. Colored regions indicate nominal speeds from different movement options.

---

  The spring skip sequence of Zkad route in 1a begins with an extended hyper into an unbuffered ultra. The leniency on the ultra is purely dependent on where the hyper is actually initiated (blue curve), and can be up to 3f. The fastest option is to demohyper after coming out of the hidden section, but this generally leaves getting a 3f ultra a 1f extension window (red points, assuming optimal demohyper). Because the downright is slower, it has a higher chance of staying in the 6px window that gives a 3f ultra for longer (and usually does). To put the plot below into words, for the 5f extension window, the nominal extension frame windows to get a 3f ultra are:
- Demo: 1/2/3/2/1
- Downright: 0/1/2/3/3

<img src="./media/science/1a_zkad_composite.png" width="960"/> 

> Leniency of the ultra as a function of hyper position (blue) and nominal trajectories of the 5 extension frames of a demo (red) or downright (green) leading into the hyper and their corresponding frame window.
  
That is to say, a demohyper has a 1f extension window to hit the 3f zone, and downright has a 2f extension window. In this particular case, it is just kind of unlucky that the demohyper does not get a 2f extension for the 3f ultra. If we were to start from a random position within range and aiming to hit an extension window within this arbitrary pixel window (~6), a demohyper would have a 74% chance of having a 2f extension window for the 3f ultra, and a downright hyper would have an 88% chance. The whole idea of slowing down is to improve our odds of getting good frame data, so to speak. In this case, the method to slow down is consistent, unlike the earlier example about releasing forward to line up a wallbounce. 

---

Case study: 5a start forward wave

3a final transition hyper

3a hub2

Dash attack leniency

3a shaft

7a flag 1

6b multiboost: convergent jump release on dash crystal freeze frame


Buffer chains, 7arb 1500m triple demo, yujene depths final spam
