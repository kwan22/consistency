[back to main](https://github.com/kwan22/consistency/blob/main/README.md)

# The science of consistency

The following discusses some common patterns that I use in my own speedruns. The discussion will be highly technical, including frame data, pixel/speed values, inner game mechanics, etc. to justify the logic. That said, the recurring theme is making small time sacrifices to relax precision and/or simplify inputs and timings. Understanding the underlying technical details is not required to see this principle.

To set the tone, let's start with a basic, "spherical-cow" type of example. Suppose you want move horizontally past a ceiling for a wallbounce. How precise is the updash? <br>
<img src="./media/science/7a_1500m_wallbounce.png" width="480"/> <br>
The faster you move, the less time you spend close enough to the wall such that a wallbounce is possible. Below shows the approximate relationship between speed and precision of the wallbounce. <br>
<img src="./media/science/generic_wallbounce.png" width="480"/> <br>
The colored boxes indicate nominal speed ranges that you would typically have from different movement options. For reference, a 5f window is the leniency of extension and buffer timing. You can see that any appreciable amount of speed quickly makes the wallbounce quite difficult to line up properly. Fundamentally, every RTA setup for a strat relies on creating some leniency in precision that is almost always obtained by sacrificing a small amount of time. Think 3a shaft demo: we spend time to line up (either manually or using certain movement combos) on a certain pixel on the wall such that a max height climbjump gives a reasonable window for the demo. The following showcases ideas and examples on ways I play the fundamental tradeoff between speed and precision.

- [Increasing leniency]

## Increasing leniency

For starters, here are some examples that I use

## Convergence and divergence

## Variable reduction
