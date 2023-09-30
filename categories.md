@def title = "Crucial Flow Research"
@def hasmath = true
@def hascode = true
<!-- Note: by default hasmath == true and hascode == false. You can change this in
the config file by setting hasmath = false for instance and just setting it to true
where appropriate -->

# Categories

**Definition**: An *object* symbol $A$ refers to an identifiable mathematical structure, such as a set or something more sophisticated like a list or type.
A *unary operation* $f : A\rightarrow A$ relates an object $A$ to itself and any object defines an identity $1_A:A\rightarrow A$.
If a *binary operation* $\circ : A\times A\rightarrow A$ relates the product of an object with itself to itself, then the object $A$ is a *magma*.

**Notation**: If an object $\frak K$ is a collection, then a member $A$ is denoted $A\in \frak K$, without imposing any (set, class, list, etc) axioms on the structure of $\frak K$.

**Definition**: When a magma $\frak K$ is a collection with members $f,g,h\in\frak K$, then the order of the binary operation is specified with parenthesis.
For example, $f\circ(g\circ h)$ or $(f\circ g)\circ h$ since $f\circ g\circ h$ is generally ambiguous.

**Definition**: A *semicategory* $\frak K = \frak K(A,B,C,...;\circ)$ is a class or collection of morphisms related in a collection of objects $1_{\frak K}$ defined by $A,B,C,...$ and a binary operation $\circ:\frak K\times\frak K\rightarrow \frak K$ with composition axiom.
When composition is clearly understood, then the symbol is omitted.
A morphism $f\in\frak K(A,B)$ has a domain $\text{Dom}:\frak K\rightarrow 1_{\frak K}$ and codomain $\text{Cod}:\frak K\rightarrow 1_{\frak K}$ such that
$$ (f : A\rightarrow B) \in \frak K(A,B) \in \text{Dom}_{\frak K}\times\text{Cod}_{\frak K}\subseteq 1_{\frak K}\times 1_{\frak K} $$
when $1_{\frak K}$ is a set.
The semicategory of morphisms with domain $A$ and codomain $B$ is $\frak K(A,B)$.
A semicategory $\frak K(A) = \frak K(A,A)$ with a single object is called a *semigroup* and with a single morphism is called *trivial*.

**Axiom**: Let $A\overset f\rightarrow B\in\frak K$ and  $B\overset g\rightarrow C\in\frak K$, then $A\overset f\rightarrow B\overset g\rightarrow C = A\overset{gf}\longrightarrow C\in\frak K$.
The *composition* axiom introduces a concept of symbolic equation (=).

**Proposition** (associativity): Let $A\overset f\rightarrow B\overset g\rightarrow C\overset h\rightarrow D \in\frak K$,  then $h(gf)=(hg)f$
$$ A\overset{hgf}\longrightarrow D = A\overset{gf}\longrightarrow C\overset h\rightarrow D = A\overset f\rightarrow B\overset{hg}\longrightarrow D. $$
Hence any semicategory $\frak K$ is an associative magma where the parenthesis can be omitted due to the equation concept from composition.

**Definition**: Let $A\overset f\rightarrow B \overset g\rightarrow A \in\frak K$, then $A\overset{1_A}\longrightarrow A$ is an *identity* element if
$$ A\overset f\rightarrow B\overset g\rightarrow A = A\overset{1_A}\longrightarrow A\overset{f}\rightarrow B\overset{g}\rightarrow A\overset{1_A}\longrightarrow A \in\frak K. $$

**Lemma**: For any $A\in1_{\frak K}$, the identity morphism $1_A:A\rightarrow A$ is unique.

*Proof*: Let $1_A^1,1_A^2$ be identity morphisms, then $1_A^1 = 1_A^2$ since
$$ A\overset{1_A^1}\longrightarrow A\overset{1_A^2}\longrightarrow A = A\overset{1_A^1}\longrightarrow A = A\overset{1_A^2}\longrightarrow A \in\frak K $$
Therefore, $A\equiv 1_A$ and $1_{\frak K} = (A,B,C,...) \equiv (1_A,1_B,1_C,...)$. $\quad\square$

This clarifies the concept that any object $A$ has an identity $A\equiv 1_A$.

**Definition**: A *category* $\frak K$ is a semicategory where $A\in 1_{\frak K}$ implies $1_A\in\frak K$.

**Corollary**: For any semicategory $\frak K$ it's clear that $1_{\frak K}$ is a category.

**Definition**: Let $f,g\in\frak K$, if $gf=1_A$ and $fg=1_B$, then $f$ and $g$ are *isomorphisms* denoted $f=g^{-1}$ and $g=f^{-1}$ with
$$A\overset{1_A}\longrightarrow A = A\overset f\rightarrow B\overset{f^{-1}}\longrightarrow A, \quad B\overset{1_B}\longrightarrow B = B\overset g\rightarrow A\overset{g^{-1}}\longrightarrow B.$$
So if $f\in\frak K$ is an isomorphism, then its *inverse* $f^{-1}\in\frak K$ exists.

**Definition**: A *monoid* is a semigroup category, a *groupoid* is a category of isomorphisms. If it is both a monoid and groupoid, then it is called a *group*.

**Definition**: An *endomorphism* $f\in\frak K$ is defind by $\text{Dom}f=\text{Cod}f$ and if it is also an isomorphism then called *automorphism*.

**Corollary**: $1_{\frak K}$ is an automorphism groupoid, as $1_A1_A^{-1}=1_A$ for all $A\in1_{\frak K}$.

**Definition**: Let $g,h:B\rightarrow C\in\frak K$, then $f:A\rightarrow B$ is an *epimorphism* if $gf=hf$ implies $g=h$,
$$ A\overset f\rightarrow B\overset g\rightarrow C=A\overset f\rightarrow B\overset h\rightarrow C \implies B\overset g\rightarrow C = B\overset h\rightarrow C. $$

**Definition**: Let $g,h:A\rightarrow B\in\frak K$, then $f:B\rightarrow C$ is an *monomorphism* if $fg=fh$ implies $g=h$.
$$ A\overset g\rightarrow B\overset f\rightarrow C=A\overset h\rightarrow B\overset f\rightarrow C \implies B\overset g\rightarrow C = B\overset h\rightarrow C. $$

**Definition**: Let $\frak K,\frak L$ be categories, then $F:\frak K\rightarrow \frak L$ is a *functor*, where for each $A\overset f\rightarrow B\in\frak K$ there exists $F(A)\overset{F(f)}\longrightarrow F(B)\in\frak L$ with $F(1_A) = 1_{F(A)}\in\frak L$ for each $A\in\frak K$ and $F(gf) = F(g)F(f)\in\frak L$ whenever $A\overset f\rightarrow B\overset g\rightarrow C\in\frak K$.
Dual to a (covariant) functor, $F:\frak K\rightarrow \frak L$ is a *contravariant functor*, where for each $A\overset f\rightarrow B\in\frak K$ there exists $F(A)\overset{F(f)}\longrightarrow F(B)\in\frak L$ with $F(1_A) = 1_{F(A)}\in\frak L$ for each $A\in\frak K$ and $F(gf) = F(f)F(g)\in\frak L$ whenever $A\overset f\rightarrow B\overset g\rightarrow C\in\frak K$.


\tableofcontents <!-- you can use \toc as well -->

<!-- ![research.jpg](/img/CFR-Desktop-1080-Compresssed.jpg) -->

Sponsor this at [liberapay](https://liberapay.com/chakravala), [GitHub Sponsors](https://github.com/sponsors/chakravala), [Patreon](https://patreon.com/dreamscatter), or [Bandcamp](https://music.crucialflow.com); also available as part of the [Tidelift](https://tidelift.com/funding/github/julia/Grassmann) Subscription.

