# Four-Dimensional Projection: Tesseract Rotation and Observable Dynamics

## Evidence classification

`SOURCE_DERIVED → INFERRED`

This artifact formalizes the mathematical and physical analogies presented in the supplied tesseract analysis. Analogies to relativity and fluid dynamics are retained as interpretive models, not as claims that Euclidean 4D rotation is literally relativistic motion.

## 1. State space

Represent a tesseract as the hypercube

$$
\mathcal{T}=\{(x,y,z,w)\mid x,y,z,w\in[-L,L]\}.
$$

Its combinatorial structure contains:

- 16 vertices;
- 32 edges;
- 24 square faces;
- 8 cubic cells.

The Euclidean metric is

$$
ds^2=dx^2+dy^2+dz^2+dw^2.
$$

A rigid rotation preserves this 4D metric even when its lower-dimensional projection appears to deform.

## 2. Rotation in the XW plane

A simple 4D rotation occurs in a plane rather than around a single 3D axis. For rotation in the XW plane, the YZ subspace is invariant.

For a point $\mathbf v=(x,y,z,w)^T$, the XW pair evolves as a planar rotation. With $\theta=\omega t$:

$$
\begin{pmatrix}
x'\\w'
\end{pmatrix}
=
\begin{pmatrix}
\cos\theta&-\sin\theta\\
\sin\theta&\cos\theta
\end{pmatrix}
\begin{pmatrix}
x\\w
\end{pmatrix}.
$$

The eigenvalue structure of the 4D rotation contains two invariant directions and a complex-conjugate pair associated with the rotating XW subspace.

## 3. Projection as information reduction

An observer restricted to $\mathbb{R}^3$ cannot directly observe $w$. Projection therefore removes or encodes information about one state variable.

### Orthographic projection

The simplest projection is

$$
P_{orth}(x,y,z,w)=(x,y,z).
$$

It discards $w$ and preserves parallel geometry.

### Perspective projection

A perspective model can encode the hidden coordinate through scale. For a projection plane at $w=0$ and a source at distance $D$, the supplied analysis uses a scale factor of the form

$$
\mathcal{S}=\frac{1}{1-w'/D}.
$$

This produces apparent expansion and contraction as the object moves through the hidden coordinate. In a bounded simulation, the parameters must prevent the denominator from reaching zero.

## 4. Apparent motion and hidden variables

The important conceptual result is that apparently discontinuous behavior in the projection can correspond to continuous deterministic motion in the full state space.

For the 16 vertices, grouping points by fixed $(y,z)$ produces four groups of four points in the XW plane. Their projected X trajectories may cross even though their full 4D trajectories remain distinct because their hidden $w$ coordinates differ.

Thus:

`projected intersection != physical collision in full state space`.

This is a general lesson for inverse problems and partially observed dynamical systems.

## 5. Oscillator interpretation

For a vertex undergoing XW rotation, the observable coordinate can be written in harmonic form:

$$
x(t)=x_0\cos(\omega t)-w_0\sin(\omega t).
$$

The hidden coordinate follows the complementary quadrature:

$$
w(t)=x_0\sin(\omega t)+w_0\cos(\omega t).
$$

The projected coordinate therefore behaves like an oscillator even though the underlying system is a rigid rotation.

The supplied analysis notes that the apparent "breathing" of the projection can exhibit frequency components associated with the geometry of the complete rotation. Such frequency interpretations should be derived from the chosen projection and observable, not assumed universally.

## 6. Relativity analogy

The supplied report compares XW rotation with certain features of Lorentz transformations and Wick rotation. This is an analogy of mathematical structure, not an identification of Euclidean rotation with physical relativistic motion.

The useful conceptual correspondence is:

```text
hidden coordinate
      ↓
projection / transformation
      ↓
observable contraction or expansion
      ↓
interpretation by a lower-dimensional observer
```

A Lorentzian spacetime uses a different metric signature, so direct physical equivalence must not be inferred from visual similarity.

## 7. Fluid-dynamical analogy

The report also interprets the 3D projection as if it were a compressible flow. A 4D incompressible rigid motion can produce an apparent source/sink pattern after projection because the observer has lost one component of the state and its derivatives.

This motivates a useful inverse-problem principle:

`divergence observed in a projection does not necessarily imply a source or sink in the full state space`.

The analogy is useful for visualization and reasoning about reduced-order models, but it should not be presented as literal fluid mechanics.

## 8. General systems insight

The tesseract model provides a reusable abstraction for systems where:

- the true state has hidden dimensions;
- observations are projections;
- apparent discontinuities arise from information loss;
- multiple hidden states map to similar observations;
- state reconstruction requires additional measurements or priors.

A generic model is:

$$
y_t=P(x_t),\qquad x_{t+1}=F(x_t,u_t),
$$

where $x_t$ is the full state, $P$ is the observation operator and $y_t$ is the observable state.

The inverse problem is generally underdetermined unless the observation process and system dynamics provide sufficient constraints.

## 9. Visualization architecture

For an interactive implementation, separate:

1. canonical 4D state;
2. rotation engine;
3. projection operator;
4. 3D scene representation;
5. camera/view transform;
6. numerical diagnostics;
7. explanatory overlays.

The same canonical state should drive every visualization mode so that orthographic and perspective projections can be compared without duplicating simulation logic.

## 10. Portfolio integration

This knowledge is relevant to Projects 40, 41, 53, 57, 60 and 72 where multimodal visualization, symbolic interfaces, world-state modeling and evidence-preserving observation are already part of the architecture.

Core principle:

`Observed state is a projection of system state; projection artifacts must not be mistaken for changes in the underlying system.`
