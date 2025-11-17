
# The algorithm

![[Pasted image 20230717155437.png]]

# Particle Attributes

1. Mass (m)
2. Position (x)
3. Velocity (v)

Represent a dynamic object by a set of N vertices and M constraints.

---
# The Solver

## Pre-Solve

### Euler step

$$x_{n+1}= x_n + ΔtV_n$$
$$V_n+_1 = V_n + (Δt/m)f_n$$

#### Semi - implicit Euler's method (Energy preserving)

$$x_{n+1} = x_n + ΔtV_{n+1}$$

## Solve

### The iterative solver (***manipulates the position*** of the particle in order to satisfy the constraints)

The problem that need to be solved comprises of a set of M equations for the 3N unknown position component.

Each constraint is solved individually using a ***nonlinear Gauss-Seidel solver***.

#### Gauss-Seidel solver

The Gauss-Seidel method is used to solve a system of linear equations.

$$ Ax = b $$

#### Each constraint equation will be solved individually and the result of one will immediately get involved in the computation of the other.

![[Pasted image 20230717144824.png]]

***Iteratively update p to satisfy constraints***

![[Pasted image 20230717144840.png]]

To find the displacement of the particle Δp, we will use a process based on **the Newton-Raphson method**.

#### Newton-Raphson method 

The goal of the Newton—Raphson method is to iteratively determine the roots of an arbitrary, nonlinear function. In other words, we minimize this function (assume a function f(x)) by finding the value of x which will make f(x)=0.

Follow the Newton-Raphson method in order to linearize the constraint functions.

$$ C(x+Δx)≈C(x)+∇C(x)⋅Δx=0 $$
$$ −C(x)=∇C(x)⋅Δx $$


$$ Δx=λM_{−1}∇Cx^T $$

Lagrange multiplier ***λ*** 
$$ λ=C(x)/∇C(x)M^{−1}∇C(x)^T $$
$$ λ=C(x)​/∣∇C(x)∣^2M^{−1} $$


$$ p_{new} = p + Δp $$
To maintain the linear and angular momentum, we restrict Δp to be in the direction of ∇C:

$$ Δp=λM_{−1}∇Cp^T $$
where M is the masses of the particles

## Post-Solve

After satisfying the constraints and moving the particle back to the wire, we need to ***solve for the new velocity***.

Update the position _and the velocity_ of each particle using an integration method called **Verlet integration**

$$ vi_​= p_i​−xi​​/Δt $$
$$ x_i = p_i $$

With **Verlet’s integration** - instead of storing each particle’s position and velocity, we store its new position pi​ and its previous position xi​.

Then calculate the new velocity!

---
# Constraints

Each constraints ***j*** consists of 
1. A cardinality $n_j$
2. A function $C_j : R^{3_{n_j}} → R$
3. a set of indices {i1,...$i_{n_j}$ }, $i_k$ ∈ [1,...N]
4. A stiffness parameter $k_j$ ∈ [0...1] and
5. A type of either equality or inequality.

Constraint $j$ with type ***equality*** is satisfied if $C_j(x_{i_1} ,...,x_{i_{n_j}} ) = 0$.

If its type is ***inequality*** then it is satisfied if $C_j(x_{i_1} ,...,x_{i_{n_j}} ) ≥ 0$.

The stiffness parameter $k_j$ defines the strength of the constraint in a range from zero to one

Distance Constraints (tentacle example: https://www.youtube.com/watch?v=vYaHl5bf4ww&t=1820s):

Rest distance $l_0$
Current distance $l$
Mass $m_i$
Inverse masses $w_i = 1/m_1$

$$ Δx_1 = (w_1/(w_1 + w_2))(l-l_0)(x_2-x_1)/|x_2-x_1|$$
$$Δx_1 = -(w_1/(w_1 + w_2))(l-l_0)(x_2-x_1)/|x_2-x_1|$$

2. One volume conservation constraint per tetrahedron.

$$C = 6(V - V_{rest})$$
$$V = (1/6)dot(((x_2 - x_1)  (x_3 - x_1)),(x_4 - x_1))$$



### **Further Reading**
1. [Position Based Dynamics | PBD](https://carmencincotti.com/2022-07-11/position-based-dynamics/)
2. [The PBD Simulation Loop | PBD](https://carmencincotti.com/2022-08-01/the-pbd-simulation-loop/)
3. [Position Based Dynamics | Muller's Original Paper](https://matthias-research.github.io/pages/publications/posBasedDyn.pdf)
4. [A Survey on Position Based Dynamics, 2017](http://mmacklin.com/2017-EG-CourseNotes.pdf)
5. [Soft Body Sim](https://www.youtube.com/watch?v=uCaHXkS2cUg&t=487s)
6. [Vector Math for Simulations](https://www.youtube.com/watch?v=hRz3sh7QQ6w)
7. [XPBD](https://www.youtube.com/watch?v=jrociOAYqxA)
8. [Pendulum](https://www.youtube.com/watch?v=XPZEeS70zzU&t=154s)
9. [Render Target Fake Soft Body](https://heyyocg.link/en/niagara-easy-soft-body-simulation/)
