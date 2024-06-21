---
tags:
  - "🌎Geoscience"
---
The axial Coriolis torque is:
$$
2\Omega\hat{\mathbf{z}}\cdot \int_\mathcal{V} \mathbf{r}\times(\hat{\mathbf{z}}\times \mathbf{v})dV.
$$
It can be rewritten as [@AubertDumberry2011]:
$$
\Omega \oint_\mathcal{S}s^2 \mathbf{v}\cdot \hat{\mathbf{n}}dS.
$$
This should vanish identically when $\mathbf{v}\cdot\hat{\mathbf{n}}=0$, which is the no-penetration condition when the mantle is immobile [@KuangBloxham1997]. 

Things are less clear when the mantle is allowed to slip on top of the fluid core. In that case, the normal velocity of the flow must match that of the mantle at the surface: 
$$
\mathbf{v}\cdot \mathbf{\hat{n}}=\frac{\partial R}{\partial \varphi}\dot{\varphi},
$$
where $R$ is the level function of the CMB defined as:
$$
R=r+\epsilon(\theta,\varphi),
$$
with $r$ being the radial coordinate and $\epsilon$ being the topographic map, satisfying $\epsilon \ll R$. 

>[!Tip] Remark
> - It is not immediately clear how the effect of that torque manifests in the frame where the mantle is at rest.


