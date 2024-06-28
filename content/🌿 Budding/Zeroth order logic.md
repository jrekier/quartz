---
tags:
  - "🧐Philosophy"
  - "🧮Math"
---
Sometimes known as *Aristotelian* or *propositional* logic. It deals with simple propositions. The canonical one being:

	Socrates is a man
	All men are mortal
	Therefore Socrates is mortal

An argument of this form with two premises is called a *syllogism*.

All arguments of the type above can be formalized as:
$$
\begin{equation}
\begin{prooftree}
\AxiomC{$p$}
\AxiomC{$p\rightarrow q$}
\BinaryInfC{$q$}
\end{prooftree}
\end{equation}
$$
where the meaning of $p$ and $q$ is left completely [[Formal logic|arbitrary]]. 