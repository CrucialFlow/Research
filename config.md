<!--
Add here global page variables to use throughout your
website.
The website_* must be defined for the RSS to work
-->
@def website_title = "Crucial Flow Research"
@def website_descr = "Research flows in mathematics and music"
@def website_url   = "https://crucialflow.com/"

@def prepath = "site"

@def author = "Dream Scatter"

<!--
Add here global latex commands to use throughout your
pages. It can be math commands but does not need to be.
For instance:
* \newcommand{\phrase}{This is a long phrase to copy.}
-->
\newcommand{\scal}[1]{\langle #1 \rangle}

<!-- font shortcuts -->
\newcommand{\mb}[1]{\mathbb{#1}}
\newcommand{\mc}[1]{\mathcal{#1}}
\newcommand{\ms}[1]{\mathscr{#1}}
\newcommand{\mf}[1]{\frak{#1}}

<!-- arrow shortcuts -->
\newcommand{\ra}{\rightarrow}
\newcommand{\lra}{\longrightarrow}
\newcommand{\la}{\leftarrow}
\newcommand{\lla}{\longleftarrow}
\newcommand{\Ra}{\Rightarrow}
\newcommand{\Lra}{\Longrightarrow}
\newcommand{\La}{\Leftarrow}
\newcommand{\Lla}{\Longleftarrow}
\newcommand{\lr}{\leftrightarrow}
\newcommand{\llr}{\longleftrightarrow}
\newcommand{\Lr}{\Leftrightarrow}
\newcommand{\Llr}{\Longleftrightarrow}
\newcommand{\ua}{\uparrow}
\newcommand{\da}{\downarrow}
\newcommand{\Ua}{\Uparrow}
\newcommand{\Da}{\Downarrow}

<!-- match parenthesis -->
\newcommand{\mlr}[1]{\left|#1\right|}
\newcommand{\plr}[1]{\left(#1\right)}
\newcommand{\blr}[1]{\left[#1\right]}
\newcommand{\nlr}[1]{\mlr{\mlr{#1}}}
\newcommand{\nlrp}[2]{\nlr{#1}_{#2}}

<!-- exponent shortcuts -->
\newcommand{\inv}{^{-1}}
\newcommand{\nrt}[2]{\sqrt[\leftroot{-2}\uproot{2}#1]{#2}}

<!-- annotation shortcuts -->
\newcommand{\conj}[1]{\overline{#1}}
\newcommand{\ol}[1]{\overline{#1}}
\newcommand{\ul}[1]{\underline{#1}}
\newcommand{\os}[2]{\overset{!#1}{!#2}}
\newcommand{\us}[2]{\underset{!#1}{!#2}}
\newcommand{\ob}[2]{\overbrace{!#2}^{!#1}}
\newcommand{\ub}[2]{\underbrace{!#2}_{!#1}}
\newcommand{\bs}{\backslash}
\newcommand{\ds}{\displaystyle}

<!-- set builder -->
\newcommand{\set}[1]{\left\{ #1 \right\}}
\newcommand{\setc}[2]{\left\{ #1 : #2 \right\}}
\newcommand{\setm}[2]{\left\{ #1 \, \middle| \, #2 \right\}}
\newcommand{\Cp}[2]{C^{#1}(#2)}
\newcommand{\Cb}[3]{C^{#1}{[}#2,#3{]}}
\newcommand{\Cpb}[3]{C^{#1}({[}#2,#3{]})}

<!-- group generator -->
\newcommand{\gen}[1]{\left\langle #1 \right\rangle}

<!-- functions -->
\newcommand{\im}[1]{\text{im}(#1)}
\newcommand{\range}[1]{\text{range}(#1)}
\newcommand{\domain}[1]{\text{domain}(#1)}
\newcommand{\dist}[1]{(#1)}
\newcommand{\sgn}{\text{sgn}}

<!-- sums -->
\newcommand{\lset}[2]{#2_1,\dots,#2_{#1}}
\newcommand{\lsum}[2]{#2_1+\dots+#2_{#1}}
\newcommand{\norm}[3]{|#2_1|^{#1}+\dots+|#2_{#3}|^{#1}}
\newcommand{\norms}[4]{\sum_{#2=1}^{#4}|#3_{#2}|^{#1}}
\newcommand{\lc}[3]{#2_1#3_1+\dots+#2_{#1}#3_{#1}}
\newcommand{\lcs}[4]{\sum_{#4=1}^{#1}#2_{#4}#3_{#4}}

<!-- Linear Algebra -->
\newcommand{\mat}[1]{\begin{bmatrix}#1\end{bmatrix}}
\newcommand{\pmat}[1]{\begin{pmatrix}#1\end{pmatrix}}
%\newcommand{\dim}[1]{\text{dim}(#1)}
\newcommand{\rnk}[1]{\text{rank}(#1)}
\newcommand{\nul}[1]{\text{nul}(#1)}
\newcommand{\spn}[1]{\text{span}\,#1}
\newcommand{\col}[1]{\text{col}(#1)}
%\newcommand{\ker}[1]{\text{ker}(#1)}
\newcommand{\row}[1]{\text{row}(#1)}
\newcommand{\area}[1]{\text{area}(#1)}
\newcommand{\nullity}[1]{\text{nullity}(#1)}
\newcommand{\proj}[2]{\text{proj}_{#1}\left(#2\right)}
\newcommand{\diam}[1]{\text{diam}\,#1}

<!-- Vectors common -->
\newcommand{\myvec}[1]{\vec{#1}}
\newcommand{\vzero}{\myvec{0}}

\newcommand{\example}[1]{*Example*. #1}
\newcommand{\define}[1]{**Definition**. #1}
\newcommand{\definition}[2]{**Definition** (!#1). #2}
\newcommand{\theorem}[1]{**Theorem**. #1}
\newcommand{\proof}[1]{*Proof*. #1 $\square$}
\newcommand{\remark}[1]{*Remark*. #1}

\newcommand{\textit}[1]{*!#1*}

\newcommand{\say}[1]{"!#1"}

\newcommand{\rcases}[1]{\left.\begin{aligned}#1\end{aligned}\right\rbrace}
