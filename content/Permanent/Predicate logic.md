---
title: "Predicate logic"
date: "2023-07-30"
tags: ["logic", "philosophy"]
enableToc: false
---
Also known as **first-order logic**, is an extension of propositional logic (then referred to as **zeroth-order logic**). 

This introduces **predicates**, and **quantifiers** over objects other than propositions. 

**Example:** 
$$
\exists x, \text{such that}~Px
$$
In the above, $x$ is called a *variable*.[^1] $P$ is a predicate, ie. a property assigned to the object, $x$. The symbol $\exists$ stands for the english phrase "there is", or "there exists".[^2] 

$\exists$ It is one of the two quantifiers. The other one is $\forall$ which stands for "for all" or simply "all". 

Predicate allows to do **calculus** when we introduce logical connecters such as the *conditional*: $\rightarrow$. 

**Usage:**

In predicate logic, the famous phrase "Socrates is a man, all men are mortal, therefore Socrates is mortal", can be formalised as the following set of statements:
$$
\exists s,Hs
$$
where $H$ is the predicate "being a man". The second part of the statement is:
$$
\forall x, H x\rightarrow Mx
$$
where $M$ is the predicate "being mortal". The full sentence is then:
$$
\begin{aligned}
\exists s,Hs\\
\frac{\forall x, H x\rightarrow Mx}{\vdash Ms}
\end{aligned}
$$
**Remark:**

In the above, we cheated and used the symbol $s$ to simply *denote* "Socrates". In reality, [denoting](https://en.wikipedia.org/wiki/On_Denoting) is a more subtle and complicated issue. 


[^1]: Note that $x$ needs not be a proposition, but it can be one.
[^2]: Note those two phrases are not necessarily equivalent (see [[Non existent objects]]).