---
title: Project Elara 2024 research and development report
short_title: Project Elara 2024 Report
bibliography:
  - citations.bib
---

+++ { "part": "abstract" }
Project Elara is a nonprofit dedicated to being part of creating a future powered by plentiful space-based solar power. In this year, the Project developed its first proposal for a prototype solar capture, microwave conversion, and transmission (SCMCT) system. System design considerations for this system are described, and initial modeling of the SCMCT system with simulation results is shown. Furthermore, a strategy for prototype testing to validate and extend upon current research is outlined.
+++

:::{note}
This is the second edition of Project Elara's 2024 research report, which was originally released on October 21st, 2024. It is dedicated to the public domain and licensed under the [Unlicense](https://unlicense.org/).
:::

# Overview

The Sun is a star, a nuclear furnace with a power output[^1] of $3.828 \times 10^{26}  \text{ W}$ [@mamajek2015iau2015resolutionb3]. Meanwhile, Earth's global power consumption[^2] in 2019 was $2.61 \times 10^{12} \text{ W}$ [@ieareport], 14 orders of magnitude below the power output of the sun. Even the most powerful artificial fusion reactor could hardly match the 4.6 billion-year-old, 2 trillion-quadrillion-ton one at the center of the Solar System. However, Earth-based solar power, while highly successful, has not truly delivered on the full possibilities of harnessing the energy of the Sun.

The primary difficulties of space-based solar power are twofold. First, high upfront costs and the difficulties of launching space infrastructure present immense hurdles. Second, the technological capabilities that would allow the full realization of space-based power to the point it is worth the cost are not yet possible. Therefore, the ultimate goal of the present research is to contribute towards the development of a space-based power transmission system that provides:

- Sustained high-power, high-gain wireless transmission with very low power loss
- Precision long-distance transmission capability, up to interplanetary distances
- Autonomous operation capability with robust failure resistance, multiple layers of redundancy, and assured safety
- All-weather reliability, including maintaining constant reception of power regardless of space weather and varied conditions in Earth's atmosphere

It is without a doubt that the technologies involved in this system are far from reaching readiness. However, @abiri2022lightweightspacebasedsolarpower have already demonstrated small-scale versions of this technology in low-Earth orbit. This research intends to supplement present achievements in the field with further advances in realizing space-based power.

# Theoretical analysis and results

Due to the difficulties of practical testing, a theoretical model of wireless power capture and transmission was first developed for initial analysis. The conceptual system consists of mirrors and satellites situated in highly eccentric geosynchronous orbits. The individually-spaced mirrors form a composite parabolic solar collector, concentrating sunlight to a fixed point. A secondary mirror at the foci of the composite collector, segmented and also of parabolic design, directs the focused light into specialized transmitter satellites. These satellites then transmit the power to Earth in the form of microwaves. The system is planned to be only one of many, with the intent to build a space-based stellar power collection swarm around geosynchronous and eventually higher orbits which may one day be able to provide all the energy for the Earth. A simplified diagram of the system is shown in [](#fig1).

:::{figure} fig/orbital-diagram-filled.png
:label: fig1
:alt: An illustration of the proposed system, showing solar collectors placed in geosynchronous orbit facing the Sun
:align: center

An illustration of a portion of the conceptual SCMCT system
:::

For the theoretical modelling, the special case of Maxwell's equations in free space, namely the 3D electromagnetic wave equation, was used. The electromagnetic wave equation is given by:

$$
\frac{\partial^2}{\partial t^2} 
\left( 
\begin{array}{c}
\mathbf{E}\\
\mathbf{B}
\end{array} \right) = c^2 \nabla^2 \left(
\begin{array}{c}
\mathbf{E}\\
\mathbf{B}
\end{array} \right)
$$

The proposed power transmission system operates at a frequency of 1 GHz, which has been identified as a candidate frequency for microwave power transmission due to its low atmospheric attenuation [@itur676]. On initial testing, it was found that numerical simulations of the electromagnetic wave equation exhibited rapid temporal oscillations that resulted in numerical instabilities. Therefore, the time-independent variant of the electromagnetic wave equation was used instead. As is well-known, this is obtained by the separation of variables of the electromagnetic wave equation, upon the simplifying assumption that the time variation of the electric field follows $\mathbf{E} \sim \cos \omega t$. This results in the Helmholtz equation:

$$
\nabla^2 \mathbf{E} + k^2 \mathbf{E} = 0,
\quad \nabla^2 \mathbf{} \mathbf{B} + k^2 \mathbf{B} = 0
$$

From this point on, only the expressions for the electric field are written and it is implied that the same expressions are true for the magnetic field up to the replacement $\mathbf{E} \rightarrow \mathbf{B}$. The Helmholtz equation was prepared in variational form (weak form) for obtaining a numerical solution by the finite element method. By multiplication with a test function $\Phi (\mathbf{x})$, integrating over the simulation domain $\Omega$, and simplifying via the Divergence Theorem, one obtains the general variational form:

$$
\int_{\Omega} k^2 \Phi \cdot \mathbf{E} \hspace{0.17em}
      dV - \int_{\Omega}
\nabla_J \mathbf{E} : \nabla_J \Phi \hspace{0.17em}
      dV + \int_{\partial
\Omega} \Phi \cdot \nabla_J \mathbf{E}
      \hspace{0.17em} d \mathbf{A} = 0
$$

Where : is the double dot product (tensor contraction for matrices). 

The boundary conditions must then be incorporated for a meaningful solution. As a starting case, the boundary conditions are given as follows:

$$
\begin{align*}
  \frac{\partial \mathbf{E}}{\partial n} |_{\partial
      \Omega_P} =
  \frac{\partial \mathbf{E}}{\partial n} |_{\partial
      \Omega_W} = 0, & \Omega
  \in \mathbb{R}^3 & \\
  \lim_{r \rightarrow
      \infty}  \mathbf{E} = \epsilon &  & 
\end{align*}
$$

Where, respectively:

- The boundary $\partial \Omega_P$ of the (primary) parabolic reflector, which reflects (and thereby focuses) the waves, with the parabolic dish centered at position $\mathbf{r}_p$; the composite collector is modelled as an approximately solid parabolic dish with perfectly reflective (Neumann) boundaries.
- The boundary $\partial \Omega_B$ (&ldquo;box&rdquo;, referring to the rectangular simulation volume) of the 3D space surrounding the antenna, where waves can pass freely into and out of the region; $\epsilon$ is a small but nonzero value representing the decay of the waves as they propagate away to infinity. This boundary is not explicitly written out but is present in the _transformed_ boundary conditions mentioned later.
- The boundary $\partial \Omega_W$ of the secondary reflector, which reflects focused light to direct it to a central collection point through an opening in the back of the parabolic dish.
- The boundary $\partial \Omega_O$ which is the opening at the bottom of the parabolic dish, where the concentrated light is directed towards the transmitting satellites. This is also not explicitly written out as it is directly encoded into the geometry of the primary reflector. 

The open boundary condition $\partial \Omega_B$ is approximated by a technique described in @comsol, in which a coordinate transform $x \to \alpha \tanh x, y \rightarrow \beta \tanh y$ is applied to extend the domain out to infinity, where $\alpha$ and $\beta$ are respectively half the length and width of the domain bounding box. This approximately replicates an open boundary that allows outgoing electromagnetic waves to radiate outwards in all directions. Upon application of the boundary conditions, we obtain the weak form for our boundary-value problem, as given by:

$$
-\int_{\Omega} (\nabla_J \mathbf{x}' : \nabla_J \mathbf{x}') (\nabla \cdot \tilde{\mathbf{E}}) (\nabla \cdot \Phi) \hspace{0.17em} dA 
+ k^2 \int_{\Omega} \Phi \cdot \tilde{\mathbf{E}}\, d \mathbf{A} 
+ \int_{\partial \Omega} = 0
$$

The derivation of this is found in [](#appendix-A), which is separately available. Simulations were done with the FreeFEM++ software [@MR3043640] with a custom FreeFEM-based solver. This solver was written in the `FreeFEM` language and utilizes `FreeFEM++`'s built-in finite-element solver and mesh discretizer, but otherwise is completely custom and tailored to the specific simulation parameters. A solution in transformed $(x', y')$ coordinates was first obtained, before the built-in polynomial interpolation was used to transform the solution to $(x, y)$ coordinates, as shown in [](#fig2a) and [](#fig2b). The domain was discretized straightforwardly by assuming a simple geometry of the antenna as a perfect paraboloid, as shown in [](#appendix-B).

:::{figure} fig/solution-xyprimed.png
:label: fig2a
:align: center

FreeFEM numerical solution in transformed coordinates $(x', y')$.
:::

:::{figure} fig/solution-xy.png
:label: fig2b
:align: center

FreeFEM numerical solution in physical-space coordinates $(x, y)$.
:::

The simulation was intended as a proof-of-concept and thus it should be emphasized that the simulation results were not of specific significance and should not be intended as research data. However, several distinctive and possibly promising features did emerge out of the initial simulation. The electric field strength being highest approximately between the parabolics, and decaying quickly outside of the immediate vicinity, corresponds with the expected result. However, it should be noted that the rather weak field variation, in which the differences of the highest and lowest field strengths is merely $5 \times 10^{- 3}  \text{N/C}$, does not provide sufficient support for these claims. Thus these are merely deduction from observations and cannot be proven at present without further testing.

As a separate test of the fidelity of the results, a custom FreeFEM-based solver was tested against a finite-difference simulation in a similar but much simpler Helmholtz boundary-value problem. A solver written with the Python `findiff` library [@findiff], a library that implements finite difference methods for PDEs, was tested, alongside a slightly different finite-difference solver that used `findiff` for simply derivative discretization. The two solvers differed at most by $6.64 \times 10^{- 13}  \text{N/C}$ and as such the rest of the finite-difference solution results are given by that of the primary `findiff` solver. The validation test took the form of solving the scalar-valued Helmholtz equation on the unit square $\Omega = [0, 1] \times [0, 1]$, with the following boundary conditions, which may appear simple, but can be shown to yield a non-trivial solution:

$$
\begin{align*}
E (x, 0) = 3 & E (x, 1) = 10\\
E (0, y) = 6 & E (1, y) = 1
\end{align*}
$$

A FreeFEM-based solver, similar although not identical to the aforementioned fully-featured vector solver, was compared against the `findiff` solver. The results from both simulations are shown in [](#fig3a) and [](#fig3b).

:::{figure} fig/validation-solution-freefem.png
:label: fig3a
:align: center

Numerical solution obtained by FreeFEM-based (finite element) solver.
:::

:::{figure} fig/validation-solution-findiff.png
:label: fig3b
:align: center

Numerical solution obtained by `findiff` (finite-difference) solver.
:::

Comparison of the numerical solutions from the two solvers showed excellent agreement and the completion of an important intermediary diagnostic for the primary FreeFEM-based solver. Diferences between the two solutions showed almost zero difference on a number of test points evaluated from both solutions, as shown in [](#fig4).

:::{figure} fig/datapoints-comparison.png
:label: fig4
:alt: A bar chart showing the differences between the two solvers across each of the test points

Comparison between numerical solutions obtained by FreeFEM and `findiff`-based solvers
:::

The results suggest that the solver shows promise, at least to the extent of present testing. However, the author would like to note that a further validation test of the vector-valued Helmholtz equation has not been successfully completed as of the time of writing. Difficulties with performing an inverse coordinate transformation from the finite-difference numerical solution have yet to be resolved, among other issues. Two different methods have been attempted, that of polynomial interpolation as well as a neural network fit, but both do not meet research standards and much further work is necessary. In addition, it was found that the order of integrals was a significant factor in deciding the result of the solution, as well as the sign convention used, where there were significantly different values when changed. It is believed to be a result of the conventions of the `FreeFEM++` software, but should continue to be investigated.

# Planned upcoming research

Further theoretical work, including a more thorough treatment of the power collection system and theoretical modelling of the power transmission system, is necessary for advancing the research. More detailed studies of orbits and spacecraft design are also hoped for in upcoming work. In addition, construction and testing of physical prototypes to augument computational simulations is also essential. Prototypes are intended to be assembled via 3D printed components treated with electroless plating to form a smooth, metallic coating, after which specific tests may be performed. The verification of such prototypes in an experimental setting is highly anticipated to be carried out in the near future.

# Disclosures

The authors would like to acknowledge the assistance of using LLMs as a source of valuable knowledge and an educational tool. No part of this paper was taken in whole or in part from content provided by the use of such tools. In addition, the author acknowledges the great assistance provided by the `FreeFEM++` software documentation, including its many examples which included example solvers of the Helmholtz equation. Another excellent reference was the website of Nicolás Guarín-Zapata[^3], whose work on finite-difference methods on infinite domain was invaluable in the course of this research.

# Open access statement

This paper is released into the public domain and the author withdraws all rights to this work, in accordance Project Elara guidelines. For more details about the project, please see [the Project Elara website](https://elaraproject.github.io/).

# Acknowledgements

On behalf of Project Elara and as the author of this paper, I would like to acknowledge the numerous contributions that went into this research. The support and collaborative effort of the entire Project team was essential to all of the research's successes. Milo played a key role in providing engineering insight, Luke in mathematical and physical analysis, Charles in offering fresh suggestions and ideas, Max (Emilliano) in continual work on research, and Arnar and Nicholas for their immense enthusiasm. I would also like to thank Professor Persans and Professor Newberg of Rensselaer Polytechnic for their support, knowledge, and their generously-offered resources, and Professor Tysoe for valuable information on the suggestion of electronless plating. I thank the support of my family and friends, including Gabrielle for her valuable suggestions of emphasizing the distinctive features of the project. Finally, I thank Dr. Harold White of Limitless Space Institute and Dr. Andrew Bramante of Greenwich High School for their invaluable mentorship and guidance in the early days of my research.

[^1]: According to the IAU defined value of the solar luminosity $L_\odot$, after rounding. 
[^2]: Found through averaging the provided 2019 global power consumption figure of 22,848 TWh [@ieareport] over one year.
[^3]: See _[Finite differences in infinite domains](https://nicoguaro.github.io/posts/infinite_fdm)_.
