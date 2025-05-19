---
title: "Appendix"
---

(appendix-a)=
# Appendix A

Here, we show the derivation of the weak form of the vector-valued Helmholtz equation for our boundary conditions. As a starting point, recall that the general variational form of the vector Helmholtz equation is given by:

$$
\int_{\Omega} k^2 \Phi \cdot \mathbf{E} \hspace{0.17em}
dV - \int_{\Omega}
\nabla_J \mathbf{E} : \nabla_J \Phi \hspace{0.17em}
dV + \int_{\partial
} \Phi \cdot \nabla_J \mathbf{E}
\hspace{0.17em} d \mathbf{A} = 0
$$

Where : denotes the double dot-product. The boundary conditions we applied within our model were given by:

$$
\begin{align*}
\frac{\partial \mathbf{E}}{\partial n} |_{\partial
    \Omega_P} =
\frac{\partial \mathbf{E}}{\partial n} |_{\partial
    \Omega_W} = 0, & \Omega
\in \mathbb{R}^3 & \\
\lim_{r \rightarrow
    \infty}  \mathbf{E} = \epsilon &
\end{align*}
$$

To simplify modelling of far-field radiation, we used a coordinate transformation as shown in [@comsol], where we applied a coordinate transform $x \to \alpha \tanh x, y \to \beta \tanh y$ to mathematically extend the domain to infinity without needing to construct a larger grid, where, $\alpha$ and $\beta$ are respectively the half-length and half-width of the domain bounding box. Physically, such a coordinate transform approximately replicates an open boundary that allows outgoing electromagnetic waves to radiate outwards in all directions, allowing the radiative boundary conditions to be imposed without needing to discretize an infinite domain.

However, the direct application of the coordinate transformation results in significant mathematical complexities due to the dependence of the representation of the variational form on the choice of coordinates. Thus tensors will be used instead to give expressions of physical laws that are invariant under coordinate transformations. From this point on, all expressions of the weak form will be given in tensors unless otherwise specified. All tensors are assumed to be within Euclidean space where upper and lower indices are equivalent, that is, $A^i = A_i$. The Einstein summation convention is assumed, in which repeated indices are implicitly summed over, and all indices take the numerical values of $i = 1, 2, 3$ unless otherwise specified.

To begin, the weak form may be expressed in tensor notation as:

$$
 \int_{\Omega} k^2 \Phi_i E^i  \hspace{0.17em} dV -
      \int_{\Omega} \partial_j
E^i \partial^j \Phi_i  \hspace{0.17em} dV +
      \int_{\partial \Omega} \Phi_i
\partial_j E^i  \hspace{0.17em} dA^j = 0
$$

One may reduce by one dimension to just consider the 2D case, as was done to simplify the problem for this initial stage of research:

$$
 \int_{\Omega} k^2 \Phi_i E^i  \hspace{0.17em} dA -
      \int_{\Omega} \partial_j
E^i \partial^j \Phi_i  \hspace{0.17em} dA +
      \int_{\partial \Omega} \Phi_i
\partial_j E^i  \hspace{0.17em} dx^j = 0
$$

The old coordinates are denoted $x^i = \mathbf{x} = (x, y)$, and new coordinates denoted $x^k = \mathbf{x}' = (x', y')$ where $x' = x' (x)$ and $y' = y' (y)$. A change of variables was applied on the weak form $x^i \to x^k$. On the first integral term, the Kronecker delta was used to relabel indices from $i \to k$, by the relationships $\Phi_i = \delta_i^k \Phi_k, \quad E^i = \delta^i_k E^k$, from which one can substitute into the first integral term to obtain:

$$
 \int_{\Omega} k^2 \Phi_i E^i  \hspace{0.17em} dA = k^2 
\int_{\Omega}
\delta_i^k \Phi_k  \hspace{0.17em} \delta^i_k E^k 
\hspace{0.17em} dA
$$

The two Kronecker deltas are contracted over both of their indices, so $\delta_i^k  \hspace{0.17em} \delta^i_k = \delta^i_i = \delta^1_1 + \delta^2_2 + \delta^3_3 = 3$. Therefore the first term further simplifies to $\displaystyle 3 k^2  \int_{\Omega} \Phi_k \hspace{0.17em} E^k  \hspace{0.17em} dA$. For the second term, the chain rule $\partial_j = \dfrac{\partial x^k}{\partial x^j} \dfrac{\partial}{\partial x^k} = \partial_j x^k  \hspace{0.17em} \partial_k$ may be used to rewrite derivatives in terms of the new coordinates $x^k$. After substitution one finds:

$$
\int_{\Omega} \partial_j E^i \partial^j \Phi_i 
      \hspace{0.17em} dA =
\int_{\Omega} (\partial_j x^k) \partial_k E^i
      (\partial^j x_k) \partial^k
\Phi_i  \hspace{0.17em} dA
$$

Where, after rearrangement and using the Kronecker delta for relabeling the $E$ and $\Phi$ indices (as shown previously with the first term), becomes:

$$
\int_{\Omega} (\partial_j x^k) (\partial^j x_k)
      \partial_k \delta^i_k E^k
\partial^k \delta_i^k \Phi_k  \hspace{0.17em} dA
$$

Taking out the Kronecker deltas allows for further simplification, where $\delta^i_k \delta_i^k = 3$ due to the double contraction previously explained:

$$
\int_{\Omega} \delta^i_k \delta_i^k (\partial_j x^k)
      (\partial^j x_k)
\partial_k E^k \partial^k \Phi_k  \hspace{0.17em} dA =
      3 \int_{\Omega}
(\partial_j x^k) (\partial^j x_k) \partial_k E^k
      \partial^k \Phi_k 
\hspace{0.17em} dA
$$

The third term may be simplified via the tensor transformation law $dx^j = \dfrac{\partial x^j}{\partial x^k} dx^k = \partial_k x^j dx^k$, from which one may obtain:

$$
\int_{\partial \Omega} \Phi_i \partial_j E^i \hspace{0.17em} dx^j = \int_{\partial \Omega} \Phi_i \partial_j E^i \partial_k x^j dx^k
$$

Now substituting in $\partial_j = \partial_j x^k  \hspace{0.17em} \partial_k$ and the two Kronecker delta identities $\Phi_i = \delta_i^k \Phi_k$ and $E^i = \delta^i_k E^k$ the result is:

$$
\int_{\partial \Omega} \delta_i^k \Phi_k \partial_j x^k 
      \hspace{0.17em}
\partial_k \delta^i_k E^k  \hspace{0.17em} \partial_k
      x^j dx^k
$$

Where, after another double contraction over the Kronecker deltas and rearranging, noting that $\partial_j x^k  \hspace{0.17em} \partial_k x^j = 1$, gives:

$$
3 \int_{\partial \Omega} \Phi_k \partial_j x^k 
      \hspace{0.17em} \partial_k x^j
\hspace{0.17em} \partial_k E^k 
      \hspace{0.17em} dx^k = 3 \int_{\partial
\Omega} \Phi_k \partial_k E^k 
      \hspace{0.17em} dx^k
$$

Altogether, after substitution of all simplified terms and ordering the terms such that the quasi-linear term is second due to software requirements, one finally obtains the weak form in the transformed coordinates:

$$
- 3 \int_{\Omega} \partial_j x^k  \hspace{0.17em}
      \partial^j x_k 
\hspace{0.17em} \partial_k E^k \partial^k \Phi_k 
      \hspace{0.17em} dA + 3 k^2 
\int_{\Omega} \Phi_k  \hspace{0.17em} E^k 
      \hspace{0.17em} dA + 3
\int_{\partial \Omega} \Phi_k \partial_k E^k 
      \hspace{0.17em} dx^k = 0
$$

After which some algebraic simplifications gives the most simplified general form:

$$
- \int_{\Omega} \partial_j x^k  \hspace{0.17em}
      \partial^j x_k 
\hspace{0.17em} \partial_k E^k \partial^k \Phi_k 
      \hspace{0.17em} dA + k^2 
\int_{\Omega} \Phi_k  \hspace{0.17em} E^k 
      \hspace{0.17em} dA + \int_{\partial
\Omega} \Phi_k \partial_k E^k 
      \hspace{0.17em} dx^k = 0
$$

In typical vector calculus notation rather than tensor notation, this may alternatively be written as:

$$- \int_{\Omega} (\nabla_J \mathbf{x}' : \nabla_J
      \mathbf{x}') (\nabla \cdot
\tilde{\mathbf{E}}) (\nabla \cdot \Phi)
      \hspace{0.17em} dA + k^2 
\int_{\Omega} \Phi \cdot \tilde{\mathbf{E}}\, d
      \mathbf{A} + \int_{\partial \Omega}
\Phi \cdot (\nabla \cdot
      \tilde{\mathbf{E}}) \hspace{0.17em} d \mathbf{x} = 0
$$

When applying boundary conditions to the boundary integral, the only contribution is that of the radiative boundary condition, which reduces to the constant Dirichlet boundary condition $\widetilde{\mathbf{E}} |_{\partial \Omega_B} = \epsilon $ and thus:

$$
\int_{\partial \Omega} \Phi \cdot (\nabla \cdot \tilde{\mathbf{E}}) \hspace{0.17em} d \mathbf{x} = 0
$$

And therefore the boundary integral vanishes. We have therefore obtained our most simplified weak form:


$$- \int_{\Omega} (\nabla_J \mathbf{x}' : \nabla_J
      \mathbf{x}') (\nabla \cdot
\tilde{\mathbf{E}}) (\nabla \cdot \Phi)
      \hspace{0.17em} dA + k^2 
\int_{\Omega} \Phi \cdot \tilde{\mathbf{E}}\, d
      \mathbf{A} = 0
$$

(appendix-b)=
# Appendix B

In this section, we show the domain parametrization used for our model. To start, the Laplacian in a generalized Euclidean coordinate transformation $x^i \to x^j$ takes the form:

(laplacian-transform)=
$$
\nabla^2 = \partial^i \partial_i x^j \partial_j +
      \partial^i x_j \partial_i
x^j \partial^j \partial_j
$$

This result is obtained using the transformation rule for partial derivatives, which is simply the chain rule:

$$
\dfrac{\partial}{\partial x^j} = \dfrac{\partial x^i}{\partial x^j} \dfrac{\partial}{\partial x^i} = \partial_j x^i \partial_i
$$

Which is then substituted into the definition of the Laplacian $\nabla^2 = \partial^k \partial_k$ and distributed to obtain the result in [](#laplacian-transform). Using this expression, with the coordinate transforms $x' = \alpha \tanh x$, $y' = \beta \tanh y$, the transformed Laplacian becomes:

$$
\nabla^2 = \alpha^2 {(1 - x'}^2) \left[
      \frac{\partial}{\partial x'}  \left(
{(1 - x'}^2)
      \frac{\partial}{\partial x'} \right) \right] + \beta^2 {(1 -
y'}^2)
      \left[ \frac{\partial}{\partial y'}  \left( {(1 -
      y'}^2)
\frac{\partial}{\partial y'} \right) \right]
$$

Thus the Helmholtz equation in the aforementioned transformed coordinates has the form:

$$
\begin{align*}
\alpha^2 {(1 - x'}^2) \left[ \frac{\partial}{\partial
      x'}  \left( {(1 - x'}^2)
\frac{\partial}{\partial x'} \right) \right] &+
      \beta^2 {(1 - y'}^2) \left[
\frac{\partial}{\partial y'}  \left( {(1 -
      y'}^2) \frac{\partial}{\partial y'}
\right) \right] \tilde{\mathbf{E}} (x',
      y') \\ &+ k^2 \tilde{\mathbf{E}} (x', y') = 0
\end{align*}
$$

The geometry of the simulation was parametrized by four constants, the simulation volume width $D$ and length $L$, the primary reflector radius $R_1$, secondary reflector radius $R_2$, opening gap radius $b$ (where the opening is located at the rear of the primary reflector dish), and the primary reflector anchor point $d_1$. The primary collector and secondary mirror were respectively parametrized as follows:

$$
\begin{align*}
  x_1 (t) = d_1 - \frac{1}{2 R_1} t^2, \quad y_1 (t) = t, \quad &t \in [- R_1, - b] \cup [b, R_1] \\
  x_2 (t) = d_1 - \frac{R_1}{2} + \frac{1}{2 R_1} t^2, \quad y_2 (t) = t, \quad &t \in [-R_2, R_2]
\end{align*}
$$

The bounding box of the simulation was parametrized as follows, for which $t \in [0, 1]$:

$$
\begin{align*}
  x_T (t) &= Lt - \frac{L}{2}, 
    & y_T (t) = \frac{D}{2}\\
  x_B (t) &= Lt - \frac{L}{2},
    & y_B (t) = - \frac{D}{2}\\
  x_L (t) &= - \frac{L}{2},
    & y_L (t) = Dt - \frac{D}{2}\\
  x_R (t) &= \frac{L}{2},
    & y_R (t) = Dt -\frac{D}{2}
\end{align*}
$$
