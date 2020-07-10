@def title = "Crucial Flow Research"
@def hasmath = true
@def hascode = true
<!-- Note: by default hasmath == true and hascode == false. You can change this in
the config file by setting hasmath = false for instance and just setting it to true
where appropriate -->

# [Crucial Flow Research](https://crucialflow.com)

Projects include mathematics and computer algebra research for differential geometric algebras, with an interest in aerospace engineering applications.
Foundations of the open source free software Grassmann.jl are based on differential geometric algebra and developed in the Julia language.
Interests include applications of Grassmann.jl software to explore relationships between quantum computing, number theory, geometric flows, aeroacoustics, relativity, optics, and electrical engineering.

\tableofcontents <!-- you can use \toc as well -->

<!-- ![research.jpg](/img/CFR-Desktop-1080-Compresssed.jpg) -->

Sponsor this at [liberapay](https://liberapay.com/chakravala), [GitHub Sponsors](https://github.com/sponsors/chakravala), [Patreon](https://patreon.com/dreamscatter), or [Bandcamp](https://music.crucialflow.com); also available as part of the [Tidelift](https://tidelift.com/funding/github/julia/Grassmann) Subscription.

@@img-small ![Grassmann.jl](/assets/grassmann.png) @@

## [Grassmann.jl](https://github.com/chakravala/Grassmann.jl)

*Leibniz-Grassmann-Clifford differential geometric algebra / multivector simplicial complex*

@@img-small [![DOI](https://zenodo.org/badge/101519786.svg)](https://zenodo.org/badge/latestdoi/101519786) @@

@@right [![GitHub stars](https://img.shields.io/github/stars/chakravala/Grassmann.jl?style=social)](https://github.com/chakravala/Grassmann.jl/stargazers)
[![YouTube](https://img.shields.io/badge/JuliaCon%202019-YouTube-red)](https://www.youtube.com/watch?v=eQjDN0JQ6-s)
[![DropBox](https://img.shields.io/badge/download_PDF-DropBox-blue.svg)](https://www.dropbox.com/sh/tphh6anw0qwija4/AAACiaXig5djrLVAKLPFmGV-a/Geometric-Algebra?preview=grassmann-juliacon-2019.pdf)
![GitHub tag (latest SemVer)](https://img.shields.io/github/v/tag/chakravala/Grassmann.jl)
[![Docs Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://grassmann.crucialflow.com/stable)
[![Docs Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://grassmann.crucialflow.com/dev)
[![Gitter](https://badges.gitter.im/Grassmann-jl/community.svg)](https://gitter.im/Grassmann-jl/community?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)
[![BiVector](https://img.shields.io/badge/bivector.net-Discourse-blueviolet)](https://bivector.net) @@

The [Grassmann.jl](https://github.com/chakravala/Grassmann.jl) package provides tools for doing computations based on multi-linear algebra, differential geometry, and spin groups using the extended tensor algebra known as Leibniz-Grassmann-Clifford-Hestenes geometric algebra.
Combinatorial products include `∧, ∨, ⋅, *, ⋆, ', ~, d, ∂` (which are the exterior, regressive, inner, and geometric products; along with the Hodge star, adjoint, reversal, differential and boundary operators).
The kernelized operations are built up from composite sparse tensor products and Hodge duality, with high dimensional support for up to 62 indices using staged caching and precompilation. Code generation enables concise yet highly extensible definitions.
The [DirectSum.jl](https://github.com/chakravala/DirectSum.jl) multivector parametric type polymorphism is based on tangent bundle vector spaces and conformal projective geometry to make the dispatch highly extensible for many applications.
Additionally, the universal interoperability between different sub-algebras is enabled by [AbstractTensors.jl](https://github.com/chakravala/AbstractTensors.jl), on which the type system is built.

![img/wave.png](/img/wave.png)

## [DirectSum.jl](https://github.com/chakravala/DirectSum.jl)

*Abstract tangent bundle vector space type operations at compile-time*

@@img-small [![DOI](https://zenodo.org/badge/169765288.svg)](https://zenodo.org/badge/latestdoi/169765288) @@

This package is a work in progress providing the necessary tools to work with arbitrary `Manifold` elements specified with an encoding having optional origin, point at infinity, and tangent bundle parameter.
Due to the parametric type system for the generating `TensorBundle`, the Julia compiler can fully preallocate and often cache values efficiently ahead of run-time.
Although intended for use with the [Grassmann.jl](https://github.com/chakravala/Grassmann.jl) package, `DirectSum` can be used independently.

## [AbstractTensors.jl](https://github.com/chakravala/AbstractTensors.jl)

*Tensor algebra abstract type interoperability with vector bundle parameter*

@@img-small [![DOI](https://zenodo.org/badge/169811826.svg)](https://zenodo.org/badge/latestdoi/169811826) @@

The `AbstractTensors` package is intended for universal interoperability of the abstract `TensorAlgebra` type system.
All `TensorAlgebra{V}` subtypes have type parameter `V`, used to store a `TensorBundle` value obtained from [DirectSum.jl](https://github.com/chakravala/DirectSum.jl).

For example, this is mainly used in [Grassmann.jl](https://github.com/chakravala/Grassmann.jl) to define various `SubAlgebra`, `TensorGraded` and `TensorMixed` types, each with subtypes. Externalizing the abstract type helps extend the dispatch to other packages.
By itself, this package does not impose any specifications or structure on the `TensorAlgebra{V}` subtypes and elements, aside from requiring `V` to be a `Manifold`.
This means that different packages can create tensor types having a common underlying `TensorBundle` structure.

@@img-small ![Dendriform.jl](/assets/dendriform.png) @@

## [Dendriform.jl](https://github.com/chakravala/Dendriform.jl)

*Dendriform dialgebra algorithms to compute Loday's arithmetic on groves of binary trees*

@@right [![](https://img.shields.io/badge/docs-stable-blue.svg)](https://chakravala.github.io/Dendriform.jl/stable)
[![](https://img.shields.io/badge/docs-latest-blue.svg)](https://chakravala.github.io/Dendriform.jl/latest) @@

Provides the types `PBTree` for planar binary trees, `Grove` for tree collections of constant degree, and `GroveBin` to compress grove data. This package defines various essential operations on planar binary trees and groves like `∪` for `union`; `∨` for `graft`; `left` and `right` for branching; `⋖`, `⋗`, `<`, `>`, `≤`, `≥` for Tamari's partial ordering; `⊴` for `between`; `/` and `\\` (i.e. `over` and `under`); and the `dashv` and `vdash` operations `⊣`, `⊢`, `+`, `*` for dendriform algebra.

Together these non-commutative binary operations satisfy the properties of an associative dendriform dialgebra. The structures induced by Loday's definition of the sum have the partial ordering of the associahedron known as Tamari lattice.

@@center ![tamari-grove-commutativity.png](/img/grove-sum-1.png) @@

* **Figure**: *Tamari associahedron, colored to visualize noncommutative sums of [1,2] and [2,1], code: [gist](https://gist.github.com/chakravala/fbc1b1a34adaeb7fdac93b3d488c57a4)*

View the documentation [stable](https://chakravala.github.io/Dendriform.jl/stable) / [latest](https://chakravala.github.io/Dendriform.jl/latest) for more features and examples.

## [Adapode.jl](https://github.com/chakravala/Adapode.jl)

*Adaptive multistep numerical ODE solver based on [Grassmann.jl](https://github.com/chakravala/Grassmann.jl) element assembly*

@@img-small [![DOI](https://zenodo.org/badge/223493781.svg)](https://zenodo.org/badge/latestdoi/223493781) @@

This Julia project originally started as a FORTRAN 95 project called [adapode](https://github.com/chakravala/adapode).
It is possible to work with L2 projection on a mesh and partial differential equations can also be assembled with various additional methods.
More general problems for finite element boundary value problems are also enabled by mesh representations imported from external sources. These methods can automatically generalize to higher dimensional manifolds and is compatible with discrete differential geometry.

@@img-small ![Reduce.jl](/assets/reduce.png) @@

## [Reduce.jl](https://github.com/chakravala/Reduce.jl)

*Symbolic parser generator for Julia language expressions using REDUCE algebra*

@@img-small [![DOI](https://zenodo.org/badge/90334073.svg)](https://zenodo.org/badge/latestdoi/90334073) @@

@@right [![GitHub stars](https://img.shields.io/github/stars/chakravala/Reduce.jl?style=social)](https://github.com/chakravala/Reduce.jl/stargazers)
[![Docs Stable](https://img.shields.io/badge/docs-stable-blue.svg)](https://reduce.crucialflow.com/stable)
[![Docs Dev](https://img.shields.io/badge/docs-dev-blue.svg)](https://reduce.crucialflow.com/dev)
[![Join the chat at gitter](https://badges.gitter.im/Reduce-jl/Lobby.svg)](https://gitter.im/Reduce-jl/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) @@

The premise behind Reduce.jl is based on the idea that `Symbol` and `Expr` types can be translated into computer algebra rewrite commands and then automatically parsed back into Julia ASTs, essentially extending the Julia language into a fully programable symbolic AST rewrite environment.

REDUCE is a system for general algebraic computations of interest to mathematicians, scientists and engineers.
Reduce.jl is an interface for applying symbolic manipulation on [Julia expressions](https://docs.julialang.org/en/latest/manual/metaprogramming) using [REDUCE](http://www.reduce-algebra.com)'s term rewrite system:

The upstream REDUCE software created by Anthony C. Hearn is maintained by collaborators on [SourceForge](https://sourceforge.net/p/reduce-algebra/).

This package is a heavily modifed version of Nathan Smith's [Maxima.jl](https://github.com/nsmith5/Maxima.jl) with many additional features.

![chakravala](https://avatars0.githubusercontent.com/u/18372368?s=400&u=e882385da78bec442e576713ab49497e1627c418)

## [Fatou.jl](https://github.com/chakravala/Fatou.jl)

*Fatou sets in Julia (Fractals, Newton basins, Mandelbrot)*

This package enables users of Julia lang to easily generate, explore, and share fractals of Julia, Mandelbrot, and Newton type. The name Fatou comes from the mathematician after whom the Fatou sets are named. Note that the Julia language is not named after the mathematician Julia after whom the Julia sets are named. This is a mere coincidence.
See [Explore Fatou sets & Fractals](/Fatou.jl) on here for detailed *examples*.

## [Wilkinson.jl](https://github.com/chakravala/Wilkinson.jl)

*Toolkit for studying numerical analysis and floating point algebra round-off*

@@img-small [![DOI](https://zenodo.org/badge/136759772.svg)](https://zenodo.org/badge/latestdoi/136759772) @@

This package is intended to help provide a complementary detailed analysis of polynomial rounding error estimates using newly defined local and global characteristic methods.
Using automated testing of different polynomial forms, an optimal expression form can be determined.
The methods used include a Simpson-Stieltjes integral method to estimate error bound discrepancy and a computationally efficient characteristic method.
The conclusions of the associated research (to be published by Advances in Engineering Mathematics) indicate the [`SyntaxTree`](https://github.com/chakravala/SyntaxTree.jl)`.exprval` method can be used to select optimal numerical code for polynomial basis functions with the [Reduce.jl](https://github.com/chakravala/Reduce.jl) symbolic rewrite package for the Julia language, which
is based on high-level code generation and macros operating on abstract syntax trees.
Due to the computational simplicity of the expression value method in comparison to the floating point error bound Simpson-Stieltjes integral estimation method, the expression value method is the demonstrably faster, more efficient, and equally reliable method for determining the optimal expression form characterization.
The purpose of this package is to help with the analysis of the characteristic methods and to explore the local properties of the Wilkinson-type error bounds on the floating point pseudo-algebra for polynomials.

## [VerTeX.jl](https://github.com/chakravala/VerTeX.jl)

*Typeset scattered graph data rewriter based on LaTeX nodes*

@@img-small [![DOI](https://zenodo.org/badge/124144717.svg)](https://zenodo.org/badge/latestdoi/124144717) @@

This project is a prototype concept for maintaining a body of research and citations via a computational graph database.
The `VerTeX` typeset scattered graph data rewriter is based on a new graph data format called VerTeX, which parses and generates LaTeX documents from nodes.
Current specifications are concerned with how to construct new documents from theorems and definitions using graph data.
This enables research collaborators to maintain databases of LaTeX nodes. The `VerTeX` julia package automatically parses this database of LaTeX nodes to extract citations and references. 
This system can also generate graph diagrams depicting the inter-relationships and dependencies of definitions, theorems, calculations, references, and results.

![lec-notes.png](/img/lec-notes.png)

## [Math Notes](https://github.com/chakravala/Math-Research-Notes)

*Theorems, Definitions, Papers, Research*

[![Build Status](https://travis-ci.org/chakravala/Math-Research-Notes.svg?branch=master)](https://travis-ci.org/chakravala/Math-Research-Notes)
[![DropBox](https://img.shields.io/badge/download_PDF-DropBox-blue.svg)](https://www.dropbox.com/sh/tphh6anw0qwija4/AADeLFJZZrm2jwCQzVebd93ba)
[![Join the chat at gitter](https://badges.gitter.im/Math-Research-Notes/Lobby.svg)](https://gitter.im/Math-Research-Notes/Lobby?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

Repository of chakravala/Michael's public notes.
Use the DropBox link to access the most up-to-date PDF, which is automatically updated in tandem with the github repo.

## [Dream Scatter](https://music.crucialflow.com)

![card.jpg](/img/Dream-Scatter-Card-45-x.jpg)

~~~
<iframe style="border: 0; width: 540px; height: 877px;" src="https://bandcamp.com/EmbeddedPlayer/album=2675505715/size=large/bgcol=333333/linkcol=4ec5ec/transparent=true/" seamless><a href="http://music.crucialflow.com/album/transient-phase">Transient Phase by Dream Scatter</a></iframe>
<iframe style="border: 0; width: 540px; height: 877px;" src="https://bandcamp.com/EmbeddedPlayer/album=2136683033/size=large/bgcol=333333/linkcol=ffffff/transparent=true/" seamless><a href="http://music.crucialflow.com/album/spectral-radius">Spectral Radius by Dream Scatter</a></iframe>
~~~
