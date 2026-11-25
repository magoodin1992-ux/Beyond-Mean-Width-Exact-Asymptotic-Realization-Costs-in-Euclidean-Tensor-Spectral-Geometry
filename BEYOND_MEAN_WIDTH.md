# Beyond Mean Width: Exact Asymptotic Realization Costs in Euclidean Tensor Spectral Geometry

**Version 1 — November 25, 2026**  
**Attribution:** magoodin1992-ux (Victor Math); AI-assisted mathematical research and exposition.  
**Status:** research preprint, not peer reviewed or independently Lean-certified.

## Abstract

We study the exact asymptotic cost of realizing a common coherent label from independently purchased pairwise identity tensors. In a fixed finite network with linear edge costs, this cost equals a terminal-cut covering linear program, over arbitrary coefficient fields. The underlying all-terminal graph-tensor rate is known; we give an explicit label-selection argument using shared tags and extend the rate to designated terminals through splitting-off. For Euclidean distances, auxiliary sites cannot reduce the optimal asymptotic cost. The normalized Gaussian mean width provides a feasible dual certificate, and equality holds exactly when a feasible capacity assignment is tight on every strictly hyperplane-separable terminal split. This yields strict gaps for simplices with at least four vertices and generic strict interior receivers. We further compose the network optimum with a contextual zero-error encoding rate, separating semantic information requirements from wire realization. This note does not assert historical priority for the individual antecedent theorems.

## 1. Model and exact terminal-cut rate

Fix a finite undirected graph \(G=(V,E)\), nonnegative costs \(c_e\), a common coefficient field \(\mathbb F\), and a set \(S\subseteq V\) of at least two distinct demanded terminals. A wire on edge \(e=uv\) is the tensor \(\sum_{j=1}^{q_e}e_j^{(u)}\otimes e_j^{(v)}\), where \(q_e\ge1\) is an integer. Its purchased cost is \(c_e\log_2 q_e\). Group incident factors at each vertex. The available operations are arbitrary local linear maps, with scalar outputs at nonterminals. Their description and execution costs are not included in the wire budget.

For \(K\ge1\), write \(D_S(K)=\sum_{j=1}^K\bigotimes_{s\in S}e_j^{(s)}\), with scalar outputs elsewhere. Let \(Q_S(T)\) be the largest \(K\) such that \(T\) restricts locally to \(D_S(K)\). For \(T\) the product of the wires,

$$
\lim_{n\to\infty}\frac{\log_2 Q_S(T^{\otimes n})}{n}
=\min_{C:\,0<|C\cap S|<|S|}
\sum_{e\in\delta(C)}\log_2 q_e.
\tag{1}
$$

The limit exists by superadditivity and the finite cut bound. Here \(\delta(C)\) denotes crossing edges. The all-terminal case has established antecedents in Vrana–Christandl and Zhou [2–4].

**Upper bound.** The flattening rank of the desired output across every terminal-splitting cut is \(K\). The product of wires has rank equal to the product of the crossing wire dimensions. Local restriction cannot increase rank. This gives the upper bound in (1) on every power.

**All-terminal lower bound: binary multigraph.** Suppose a connected loopless multigraph has \(M\) edges, at least three vertices, and minimum cut \(\lambda\). Put \(d=M-\lambda\ge1\). The line graph is \(\lambda\)-connected: deleting fewer than \(\lambda\) edges preserves connectivity of the original graph. By the corrected Lovász–Saks–Schrijver general-position orthogonal representation theorem [6], there are vectors \(u_e\in\mathbb R^d\) in general position, orthogonal for disjoint edges. They can be taken integral: in line-graph vertex order, perturb inputs to rational vectors and project each away from the span of its previously assigned nonneighbors. At the original representation this procedure is stationary, each such constraint span has at most \(d-1\) independent vectors, and all the required nonzero minors persist under sufficiently small perturbations. Rational projection and clearing denominators give the claimed integral representation.

Group \(a\) binary copies into edge labels \(j_e\in\{0,\ldots,q-1\}\), where \(q=2^a\). The integer vector \(\sum_e u_ej_e\) takes at most \(Aq^d\) values for a constant \(A\) depending only on the fixed representation. Some fiber \(F=\{j:\sum_eu_ej_e=g\}\) therefore has at least \(q^\lambda/A\) labelings. At any vertex the incident labels identify the entire member of the fiber: at most \(d\) edges are nonincident, and their vectors are independent.

The nonnegative integer residual \(\|\sum_e u_ej_e-g\|^2\) can be written as \(\sum_v w_v(j_{\mathrm{inc}(v)})\). Indeed its cross terms for disjoint edges vanish; assign each remaining term to an incident vertex and the constant to any one vertex. This is an integer identity on basis indices, not arithmetic in \(\mathbb F\).

Take \(N\) copies of the grouped graph tensor. Supply an additional coherent shared tag indexing tuples of local weight totals summing to zero. Each total lies in \([-NB,NB]\) for a fixed \(B\), so the tag uses \(O(\log N)\) bits at fixed graph and \(q\). A spanning tree supplies the tag: use wires carrying the tag alphabet and local equality filters at internal vertices. Extra binary copies of the original connected multigraph supply these wires with \(O(\log N)\) overhead.

At each vertex retain only local tuples whose total matches its tag component and whose local indices come from the fiber, relabeling them by the corresponding global fiber tuple. Local injectivity justifies the relabeling. A surviving term must have total residual zero across all \(N\) copies. Since each residual is nonnegative, every copy lies in \(F\). Conversely every tuple of fiber elements survives exactly once, because its weight totals determine its unique tag. The output is exactly \(D_V(|F|^N)\), with coefficient one per term over every field. Taking \(N\to\infty\) at fixed \(q\), then \(a\to\infty\), yields at least \(\lambda\) bits per original binary graph copy. The two-vertex case is a single grouped wire, and a disconnected graph has rate zero. This supplies the all-terminal lower bound.

**Eliminating nonterminals and arbitrary dimensions.** For a fixed large integer \(r\), restrict each edge in \(T^{\otimes r}\) to \(2\lfloor r\log_2(q_e)/2\rfloor\) binary wires. This yields even degrees at all vertices. Discard components containing no terminal; if terminals are disconnected the rate bound is zero. By the even-degree splitting-off theorem [5], pair incident edges at a nonterminal and replace \(av,vb\) by \(ab\), preserving local edge connectivity among remaining vertices. Repeat until only terminals remain; discard loops. This is a local tensor restriction: the equality functional on two indices at the eliminated site leaves an ordinary binary identity wire at the endpoints. For a loop use a fixed matching label and evaluate its two fixed endpoint factors to one. No field-dependent division is needed. The resulting terminal multigraph has minimum cut at least \(r\min_C\sum_{e\in\delta(C)}\log_2 q_e-2|E|\). Apply the all-terminal rate to repeated group copies, divide by \(r\), and let \(r\to\infty\). This proves (1).

## 2. Exact asymptotic purchased wire budget

Let \(L_S(m)\) be the infimum cost of an exact realization of \(D_S(2^m)\). If terminals are disconnected the cost is infinite for \(m>0\). Otherwise,

$$
C_G(S):=\lim_{m\to\infty}\frac{L_S(m)}{m}
=\min_{b\ge0}\left\{\sum_{e\in E}c_e b_e:
b(\delta(C))\ge1 \text{ for every terminal-splitting cut }C\right\}.
\tag{2}
$$

The flattening bound gives the lower bound for each finite realization by dividing its log capacities by \(m\). For the reverse direction, clip capacities to at most 1, preserving feasibility. The resulting compact rational polytope has an optimal rational vertex, even when costs are real. Choose a common denominator \(h\) for that vertex and take \(q_e=2^{hb_e}\). Its terminal minimum cut is at least \(h\). By (1), repeated copies supply at least \(h(1-\epsilon)\) bits per copy for every fixed \(\epsilon>0\) and all sufficiently large powers. Choose enough copies for the requested output, trim excess labels, divide cost by \(m\), and send \(\epsilon\) to zero. All output restrictions are exact; only the resource rate is asymptotic.

For computation, choose a root terminal \(s_0\). For each other terminal \(t\), introduce an independent signed unit flow \(f^t\) from \(s_0\) to \(t\), with \(-b_e\le f^t_e\le b_e\). Max-flow/min-cut shows equivalence to the cut constraints in (2). This gives a polynomial-size LP, with \(O(|S|(|E|+|V|))\) scalar conditions and polynomial-time exact value optimization for rational costs in the explicit input model. These are separate flow certificates; summed multicommodity capacity constraints are not required. The tensor realization theorem supplies simultaneous coherent output. Efficient compilation of the local maps is a separate, unresolved resource question.

## 3. Euclidean geometry and elimination of auxiliary sites

Now allow a wire between any pair of distinct sites at cost equal to their Euclidean distance. Let \(C(S)\) denote the terminal-only complete-graph optimum of (2). Any finite collection of auxiliary sites gives the same infimum when arbitrary such collections are allowed.

To see this, round any feasible auxiliary-network capacities upward to rational multiples and scale to even integer multiplicities. Split off nonterminals while preserving terminal connectivity. Each replacement \(av,vb\mapsto ab\) costs no more than the pair removed by the triangle inequality. Divide by the scale and let rounding error vanish. This proves that the terminal-only LP is a lower bound for every finite auxiliary configuration; (2) on the terminal-only graph gives the matching asymptotic construction.

## 4. Mean-width dual and exact tightness criterion

For distinct Euclidean terminal positions \(x_i\), define the normalized mean width

$$
W(S)=\frac{\sqrt{2\pi}}2\,\mathbb E
[\max_{i\in S}\langle Z,x_i\rangle-\min_{i\in S}\langle Z,x_i\rangle],
$$

where \(Z\) is a standard Gaussian in the affine span after translation. This has the segment normalization \(W(\{i,j\})=\|x_i-x_j\|\), and agrees with the shared-label price in [1].

The dual to (2) has nonnegative variables \(y_C\) on unordered nontrivial terminal cuts, with \(\sum_{C:e\in\delta(C)}y_C\le\|x_i-x_j\|\) and objective \(\sum_C y_C\). Assign \(y_C\) the normalized Gaussian threshold mass of the cut: project all sites onto \(Z\), integrate thresholds with density \(\sqrt{2\pi}/2\), and average. Each edge constraint is exactly tight, because the expected absolute projection of its displacement is \(\sqrt{2/\pi}\|x_i-x_j\|\). The total mass is \(W(S)\). A cut has positive mass exactly when its two vertex groups are strictly separable by an affine hyperplane: a strict separating direction has an open neighborhood with positive threshold interval; a positive interval itself gives a separation.

It follows that

$$
\boxed{C(S)=W(S)\iff
\exists b\text{ feasible in (2), with }b(\delta(C))=1
\text{ for every strictly separable split }C.}
\tag{3}
$$

Indeed the objective gap equals \(\sum_C y_C[b(\delta(C))-1]\), a sum of nonnegative terms; a minimum is attained in the clipped LP. This also establishes \(C(S)\ge W(S)\) without invoking the existence of a fully additive tensor-semiring spectral point. The Gaussian average of log cut ranks is multiplicative in exponential form and restriction-monotone, but need not be additive on direct sums.

## 5. Tight and strict examples

**Convex planar boundary and collinear sets.** A half-capacity boundary cycle is feasible and every strictly separating line crosses it twice. Thus (3) is tight, with cost half the perimeter. For collinear sites the sorted path with unit capacities is tight and its total cost is the interval length.

**Generic interior receiver.** Let \(z\) lie strictly in the relative interior of the convex hull of the other sites, in affine dimension at least two, with no two other sites collinear through \(z\). If (3) held, take a generic projection direction and compare the nontrivial cuts immediately before and after \(z\). Tightness forces equality of total capacities from \(z\) to each projection side. Cross a direction perpendicular to \(x-z\) while avoiding the other such perpendicular hyperplanes. Only that edge changes sides, forcing \(b_{zx}=0\). Repeat for each \(x\); this contradicts the singleton cut at \(z\). Hence the gap is strict.

**Simplices.** For \(n\ge4\) affinely independent sites every nontrivial split is strictly separable. Tight singleton cuts force degree 1 at every vertex; tight pair cuts then force every edge capacity to be \(1/2\), contradicting degree \((n-1)/2>1\). Thus \(C(S)>W(S)\). For a regular unit-edge simplex the singleton cuts give cost at least \(n/2\), attained by a half-capacity cycle. For the regular tetrahedron specifically, \(W(S)=3/2+(3/\pi)\arcsin(1/3)<2=C(S)\). For completeness, represent its vertices by \(e_i/\sqrt2\) in \(\mathbb R^4\), so \(W=\sqrt\pi\,\mathbb E\max_{i\le4} Z_i\). Integration by parts gives \(\mathbb E\max Z_i=12\int\phi^2\Phi^2=(6/\sqrt\pi)\mathbb E\Phi(Y)^2\) with \(Y\sim N(0,1/2)\). This last expectation is the joint positive quadrant probability for two centered Gaussians of correlation \(1/3\), namely \(1/4+\arcsin(1/3)/(2\pi)\).

**A demanded centroid.** For a unit equilateral triangle and its centroid, the hull remains the same whether the centroid is demanded or not. With \(X,Y\) total capacities of rim edges and spokes, the three vertex singleton cuts give \(2X+Y\ge3\); the demanded centroid gives \(Y\ge1\). Therefore \(X+Y/\sqrt3\ge1+1/\sqrt3\). A half-capacity cycle using two rim edges and two spokes attains equality. Without the centroid requirement the triangle costs \(3/2\). By Section 3 both optima persist under arbitrary finite auxiliary sites. The spectral marginal is zero but the wire-cost marginal is \(1/\sqrt3-1/2>0\). See the companion note [7] for a direct cycle construction.

## 6. Task-conditioned information and realization

Let a finite hidden state \(x\in X\) be encoded before a receiver learns a feasible context \(z\), with relation \(R\subseteq X\times Z\). Each feasible pair has a nonempty set \(K_{x,z}\) of acceptable answers. One answer must serve each code/context pair. Form the incompatibility hypergraph on \(X\): a nonempty set \(U\) is forbidden when there is a context feasible for all its members for which \(\bigcap_{x\in U}K_{x,z}=\varnothing\). For multiple receivers use the constraints from each local receiver/context; their acceptance requirements must compose conjunctively.

The minimum alphabet \(k_*\) equals the hypergraph chromatic number. Every code class must avoid containing a forbidden set; conversely each such class has a common acceptable answer for every required context. In the deterministic exact-response case this reduces to the classical characteristic graph of zero-error coding with side information [8].

For the coherent implementation, place an encoder \(p\) and distinct copy receivers at terminal set \(A\). For a surjective code \(m:X\to[k]\), its encoding tensor is \(T_m=\sum_x e_x^{(p)}\otimes\bigotimes_{s\in A\setminus\{p\}}e_{m(x)}^{(s)}\). It is locally restriction-equivalent to \(D_A(k)\): expand each encoder label to the sum over its fiber, or conversely select one representative per fiber. This holds in every field. Consequently the minimum spectral price is \(W(A)\log_2 k_*\). For \(n\) independent coordinates and a block decoder, let \(k_n\) be the least alphabet. Concatenation gives submultiplicativity, hence \(B=\lim_n\log_2 k_n/n=\inf_n\log_2 k_n/n\). Combining the exact cut lower bound with (2) at \(\lceil\log_2 k_n\rceil\) bits and trimming proves the task-conditioned exact asymptotic purchased cost per coordinate:

$$
\boxed{C_{\mathrm{task}}=B\,C_G(A).}
\tag{4}
$$

The zero-rate case follows from a spanning-tree upper bound linear in the log alphabet. This result applies to the declared coherent-label interface, not arbitrary randomized communication protocols or jointly constrained decoders. Classical coding complexity and the cost of constructing or verifying the code and local maps remain separate.

As an example, the five-cycle characteristic graph has one-use alphabet 3 and asymptotic rate \(\log_2\sqrt5\) (the classical five-cycle zero-error result). For two coordinates, \(x+2y\bmod 5\) is a five-coloring of the strong graph square. For the lower bound, unit vectors \(v_j=(a,b\cos(2\pi j/5),b\sin(2\pi j/5))\), with \(a^2=1/\sqrt5\), \(b^2=1-a^2\), are orthogonal for nonadjacent distinct vertices. Tensor powers give an orthonormal family for any independent set of the strong power; the squared overlap with the first-coordinate tensor vector is \(5^{-n/2}\). Bessel's inequality bounds each independent set by \(5^{n/2}\), so a coloring needs at least \(5^{n/2}\) colors. The paired construction matches this rate. Formula (4) prices its coherent realization on any fixed network.

## 7. Scope and open problems

The contribution of this note is the combination of terminal-specific graph-tensor realization, cost optimization, Euclidean auxiliary-site elimination, mean-width tightness, strict gaps and contextual encoding. Several ingredients and special cases have established antecedents. No claim of historical priority is made without a broader literature search. The exact cost is a purchased wire budget; it is not physical energy, elapsed runtime, a universal spectral characterization, or a proof of a complexity-class separation. Finite-block compiler size, efficient synthesis, extensions beyond pair wires and coherent-label interfaces, and the full external verification chain are open. The stated results have a mathematical proof here but have not undergone independent peer review or mechanized certification.

## References and provenance

1. OpenAI, *Euclidean geometry in the asymptotic spectrum of tensors*, November 24, 2026, [pinned manuscript](https://github.com/openai/math/blob/92b516ef8e2abf66c3db7aa31438d3010bc7956f/preprints/Euclidean-geometry-in-the-asymptotic-spectrum-of-tensors-November-24-2026/paper.pdf). Source of compatible Euclidean spectral pricing.
2. P. Vrana and M. Christandl, *Entanglement distillation from Greenberger–Horne–Zeilinger shares*, [arXiv:1603.03964](https://arxiv.org/abs/1603.03964). All-terminal graph conversion antecedent.
3. Zhou, [arXiv:2610.34273](https://arxiv.org/abs/2610.34273), Appendix B. Graph-tensor rate and extraction.
4. Zhou, [weighted graph-tensor manuscript](https://hub.valency.io/works/W_h3r52dg7), Appendix B. Weighted all-terminal rate.
5. W. Mader, undirected splitting-off theorem, [source](https://www.sciencedirect.com/science/article/pii/S0167506008705041).
6. Lovász–Saks–Schrijver, correction to the general-position orthogonal representation theorem, [DOI](https://doi.org/10.1016/S0024-3795(00)00091-4).
7. magoodin1992-ux, [SRG-7C91: A zero spectral marginal with positive asymptotic wire cost](https://github.com/magoodin1992-ux/asymptotic-tensor-spectral-geometry-extensions/blob/7e07e7d8edcb3bd9f12b7fff9f4649ee16fe27cc/SRG-7C91.md), November 25, 2026.
8. H. S. Witsenhausen, *The zero-error side information problem and chromatic numbers*, IEEE Transactions on Information Theory 22 (1976), 592–593; L. Lovász, *On the Shannon capacity of a graph*, IEEE Transactions on Information Theory 25 (1979), 1–7.

Derived from the Victor Math November 25, 2026 research checkpoint, with AI-assisted proof development. Original exposition licensed CC BY 4.0 to the extent rights are held by the publisher; external works retain their terms.
