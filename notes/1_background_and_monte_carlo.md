# Simulation and modeling of natural processes
The goal of this course is to understand the field of simulation and translate it into Julia.

## Objectives and background
Modeling is used to abstract a system in order to understand it or make predictions 
Subjects that use modeling range from physics to economics
Modeling and simulation is a field of computational science resulting from large amounts of data and the need to integrate many processes together.

## Modeling and simulation
Why a model?
- Describe, understand, predict, control.
What is a good model?
- Generalizable, based in reality, useful, practical
- Depends on the question and _level of abstraction_ or _level of reality_.
    - The same system can be described on different scales.
Fluids can be described with PDEs to answer questions.
- They can also be simulated many times in a computer model.
Modeling methods:
- N-body systems/molecular dynamics
- ODEs, PDEs
- Monte-Carlo methods
- Cellular automata
- Multi-agent systems
- Discrete events simulations
- Complex networks
Skills needed to create simulations:
- programming/software engineering
- algorithms/data structures
- parallel programming/GPUs
- code optimization
- data analysis
Simulations need to be validated
## Modeling space and time
Spatially extended dynamical systems
Time evolution: differential equations or discrete time states
- Discrete-event-simulation (DES): the evolution of the system is broken up according to the events.

Time evolution:
1. Mathematical models
t0---------------------tf
2. Time intervals
t0--•--•--•--•--•--•--•tf
3. Discrete-event-simulation (DES)
t0-•-----•-•-----••--•-tf

Modeling space: Eularian approach
- the observer sits at a fixed position
- attach a property of the system at each spatial location:
    - local atmospheric pressure
    - rate of cars passing by
- space can be continuous or discrete
-------------------------------------
|•| | | | | | |•| | | | | | | | |•| |   
-------------------------------------
| | | |•| | | | | | | | | |•| | | | |   
-------------------------------------
| | |•| | | | |•| | | | | | | |•| | |   
-------------------------------------

Modeling space: Lagrangian approach
- the observer takes the point of view of the moving objects
- position of all the objects of interest as a function of time
    - the movement of the moon is described by its trajectory x(t)
-------------------------------------
|    •                •          •  |   
|       •      •             •      |   
|  •                  •    •        |   
-------------------------------------

Beyond the physical space: complex networks
- spatial relationships are represented as graphs
- the spatial positions of the components don't matter
    - the interaction of the components are what matter
    - social systems
    - graph edges can change over time __dynamical__
- quantities of graph topology:
    - degree distribution
    - clustering coefficient
    - centrality measures

## Example of biomedical modeling
Thrombosis in cerebral aneurysms
- the evolution of aneurysms depends on blood flow, biomechanics, and biology
    - they are treated with stents/flow diverter -> induces clots in eneurysm
- red blood cells and platelets are deformable suspensions in fluid

## Monte-carlo methods 1
Background
- Sampling of a process in order to determine statistical properties
- Coin toss example
- Mathematics solution
    - P(3 heads) = 4C3 * (0.5)^3 * (1 - 0.5) = 0.25
- Monte-Carlo solution
    - coin-monte-carlo.py

## Monte-carlo methods 2
What is p(x) and rho(x)?
Markov-Chain Monte-Carlo (MCMC)
- a stochastic process whose goal is to explore the state space of a system of interest
- x is a point in state space. It jumps around to location x' with probability $W_{x->x'}$
- MCMC samples from a distribution p(t, x) describing the probability of being at point x at time t
How to choose $W_{x->x'}$?
Sampling the diffusion equation in 1D
- p(t + 1, x) = sum(p.(t, x') .• W)
- I don't understand this section. This is similar to the Random Walk code I wrote for the statistical mechanics book
- In 1D, the particle can diffuse to the left W-, right W+, or stay still W0
- p(t + 1, x) = p.(t, x - 1) .• W- + p.(t, x) .• W0 + p.(t, x + 1) .• W+
Diffusion equation
- it can be discretized
- Discretization of the diffusion equation looks complicated
Monte-Carlo simulation of Diffusion
- a random walk samples a density that obeys the diffusion equation
- random walks have advantages over diffeq because you can add obstacles
Master equation
- at steady state W- == W+
Metropolis rule
- Questions from quiz:
    1. Does it obey the detailed balance?
    2. What is the probability of a particle moving from location x to x'?
    3. How is an experiment accepted?
    4. When the temperature is high, what is the likelihood of accepting a move?
- a physical system at equilibrium whose probability to be in x is given by the __Maxwell-Boltzmann distribution__.
Glauber rule

## Monte-Carlo methods 3
Kinetic/dynamic Monte-Carlo
_How can I solve this with pen and paper? What about in Julia? Catalyst.jl?_
Analytical solution
Monte-Carlo simulation
- Find the steady state concentrations of two reagents
1. Define a small time step dt such that k1dt and k2dt < 1. They are the probabilities that A -> B or B -> A
2. Choose a random particle A if rand(0, 1) < A/(A+B) else B
3. then simulate according to the probability of reaction:
    - if A then (A -> B if rand(0, 1) < k1dt else A) else (B -> A if rand(0, 1) < k2dt else B)
4. Repeat (2) and (3) N times then increment t by dt and repeat
Gillespie's algorithm


# Algorithms covered in this lesson

