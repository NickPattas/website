
## Particle System Dynamics

Particles are objects that have **mass, position, velocity** and **respond** to forces, but that gave no spatial extent.

Forces can be grouped into three categories:
1. ***Unary forces***, such as gravity and drag, that act independently on each particle, either exerting a constant force, or one that depends on one or more of particle position, particle velocity, and time.
2. ***$n$-ary forces***, such as springs, that apply forces to a fixed set of particles.
3. ***Forces of spatial interaction***, such as attraction and repulsion, that may act on any or all pairs of particles, depending on their positions.

### Unary forces

#### Gravity

The gravitational force on each particle is: $$ f = mg $$
$m$ mass of the particle.
$g$ constant vector (presumably pointing down) whose magnitude is the gravitational constant.

#### Viscous Drag

Ideal viscous drag has the form: $$ f = -k_dv $$

The constant $k_d$ is called ***coefficient of drag***.

The effect of drag is to resist motion, making a particle gradually come to rest in the absence of other influences.

***Each highly recommended that at least a small amount of drag be applied to each particle, if only to enhance numerical stability.***


### $n$-ary forces

Our canonical example of a binary force is a Hook's law spring.

The spring forces between a pair of particles at positions **a** and **b** are: $$fa = − [ks(|l| − r) + kd(j · l)/|l|](l/|l|),       fb = −fa,$$

Where $f_a$ and $f_b$ are the forces on **a** and **b**, respectively,
$l=a-b$,
$r$ is the rest length,
$k_s$ is a spring constant,
and $k_d$ is a damping constant.
$j$ the time derivative of $l$, is just $v_a - v_b$, the difference between the two particle's velocities.


### Spatial Interaction Forces

Spatial interaction forces may act on any pair (or $n$-tuple) of particles.

For local interaction forces, particles begin to interact when they come close and stop when they move apart.

Spatially interaction particles have been used as approximate models for fluid behavior, and large-scale particle simulations are widely used physics.

A complication in large-scale spatial interaction simulations is that the force calculation is $O$($n^2$) in the number of particles.

If the interactions are local, efficiency may be improves through the use of spatial buckets.

