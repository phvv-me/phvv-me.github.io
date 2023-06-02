---
date: '2020-05-25'
description: Demonstração da Métrica de Schwarzschild da Relatividade Geral a partir das equações de campo de Einstein com as coordenadas de Schwarzshild
language: português
layout: post
tags:
    - relativity
title: Demonstração da Métrica de Schwarzschild
---
<!--
---
title: Demonstrating the Schwarzschild's Metric
date: "2020-05-25"
description: General Relativity Schwarzschild's Metric Demonstration from Einstein's field equations with Schwarzshild coordinates
language: english
category: post
--- -->

As equações de campo de Einstein carregam toda a essência e todos os princípios por detrás da Relatividade Geral. Curiosamente, em notação tensorial, elas se reduzem a uma única expressão aparentemente muito simplória.

$$
  G_{\mu\nu} = 8 \pi \, G \, T_{\mu\nu}
$$

Entretanto, essa expressão trata na verdade de equações diferenciais de segunda ordem não-lineares e, portanto, resolvê-la é difícil mesmo em sistemas bem simples. O próprio Einstein, após propô-las, disse acreditar que tomaria ainda muito tempo para que alguém conseguisse achar uma solução. Felizmente, ele estava errado: no ano seguinte à sua exibição pública, <cite>Karl Schwarzschild</cite> publicou a primeira solução das equações de campo enquanto lutava na Primeira Guerra Mundial.

## Modelando o problema

Para alcançar esse feito, Schwarzschild assumiu um campo estático e esfericamente simétrico gerado por uma distribuição de massa esfericamente simétrica em repouso. Em outras palavras, imaginou um sistema como um planeta, uma estrela, o Sol na forma de uma esfera perfeita de raio $R$ em que toda a sua massa $m$ se encontra igualmente distribuída em um volume $V$ e parada (sem vibrações nem rotação). Matematicamente, isso se traduz num modelo para a densidade de massa do sistema como uma função $\rho$ expressa através de

$$
\rho(r) = \begin{cases}
  ^m / _V, & r \leq R \\
  \hskip1.3em 0, & r > R \\
\end{cases}
$$

Agora, para que vejamos como isso simplifica as equações de campo, é necessário olhar a definição do tensor de energia-momentum $T^{\mu\nu} = \dfrac{\partial p^\mu}{\partial S_\nu}$ onde $p^\mu$ é o quadrimomentum e $S_\nu$ se trata da hipersuperfície espaço-temporal, i.e.,

$$
dS_\nu = \displaystyle \prod_{\alpha \neq \nu} dx_\alpha = \dfrac{dx_0 dx_1 dx_2 dx_3}{ |dx^\nu| }
$$

Primeiramente, da imposição que a distribuição $\rho$ está em repouso, o quadrimomentum assume a forma

$$
p^\mu = m u^\mu = m (1, \vec{v}) = (m, 0) \Rightarrow p^a = 0 \\
\text{e} \ p^0 = \begin{cases}
    m, & r \leq R \\
    \hskip0.8em 0, & r > R \\
\end{cases}
$$

e, portanto, $T^{a\nu} = \dfrac{\partial p^a}{\partial S_\nu} = 0$. Por outro lado,

$$
T^{0b} =
        \dfrac{\partial p^0}{\partial S_b} =
        \dfrac{\partial m}{\partial x_0 \partial x_a \partial x_c} =
        \dfrac{\partial^2}{\partial x_a \partial x_c}\dfrac{\partial m}{\partial t} = 0
$$

Assim, o que se chega é que o único valor não nulo do tensor de energia-momentum é

$$
  T^{00} = \dfrac{\partial p^0}{\partial x_1 \partial x_2 \partial x_3} = \dfrac{\partial p^0}{\partial V} = \dfrac{p^0}{V} = \rho(r)
$$

Essa expressão nos leva a dois campos distintos: um na região interna do sistema $T^{00} = \tfrac{m}{V}$ e outro na região externa $T^{00} = 0$. Em sua análise, Schwarzschild considerou apenas a segunda região e é isso o que iremos replicar aqui.

Assumindo, então, $T_{\mu\nu} = T^{\mu\nu} = 0$, chega-se às **equações de vácuo**

$$
G_{\mu\nu} = 0 \Rightarrow
    R_{\mu\nu} - \tfrac{1}{2} R g_{\mu\nu} = 0
$$

É possível, ainda, simplificar mais a equação se calcularmos a contração do tensor de Einstein

$$
\begin{aligned}
                  G & = {G^\mu}_\mu \\
                    & = {R^\mu}_\mu - \tfrac{1}{2} R {g^\mu}_\mu \\
                    & = R - \tfrac{1}{2} R {\delta^\mu}_\mu \\
                    & = R - 2 R \\
                    & = - R \\
                    & = 0\text{, pois } G_{\mu\nu} = 0 \Rightarrow {G^\mu}_\mu = 0 \\
\end{aligned}
$$


Assim, chegamos à forma mais simples para a expressão das equações de campo no vácuo $R_{\mu\nu} = 0$

## Métrica nas Coordenadas de Schwarzschild

A premissa de campo estático no sistema de Schwarzschild leva a uma métrica independente do tempo e a um elemento de linha invariante frente inversões temporais. Essa segunda condição leva a vínculos na métrica, que podem ser obtidos por meio de

$$
\begin{aligned}
	ds^2(x^0) = ds^2(x'^0 = -x^0) & \Rightarrow g_{\mu\nu}dx^\mu dx^\nu = g_{\mu\nu}dx'^\mu dx'^\nu \\
                                  & \Rightarrow g_{00}dx^0dx^0 + g_{01}dx^0dx^1 + \dots = g_{00}dx^0dx^0 - g_{01}dx^0dx^1 + \dotsm  \\
                                  & \Rightarrow g_{a0} = g_{0a} = 0 \\
\end{aligned}
$$

Além disso, Schwarzschild assumiu um campo esfericamente simétrico, o que significa que, em coordenadas esféricas $(x^\mu) = (t, r, \theta, \varphi)$, a métrica precisa ser diagonal $g_{ij} = 0 \Leftrightarrow i \neq j$.

Logo, temos que

$$
\begin{cases}
	g_{\mu\nu,0} = 0 \\
	g_{a0} = g_{0a} = 0 \\
	g_{ij} = 0 \Leftrightarrow i \neq j \\
\end{cases}
$$

As condições acima levam a um _Ansatz_ componentes da métrica covariante em coordenadas esféricas

$$
(g_{\mu\nu}) = \left(\begin{matrix}
	-e^{2\tau} & 0 & 0 & 0 \\
	0 & e^{2\lambda} & 0 & 0 \\
	0 & 0 & r^2 & 0 \\
	0 & 0 & 0 & r^2 sen^2 \theta
\end{matrix}\right)
$$

onde $\tau = \tau(r) \text{ e } \lambda = \lambda(r)$

## Obtendo as conexões da métrica

Então, o que resta agora é descobrir como são as funções $\tau \text{ e } \lambda$. Para tal, utilizaremos a equação das geodésicas

$$
\ddot{x}^\alpha + \Gamma^\alpha_{\mu\nu}\dot{x}^\mu\dot{x}^\nu = 0
$$

para calcular as conexões $\Gamma^\alpha_{\mu\nu}$ da variedade geométrica do espaço-tempo, pois devemos utilizar as equações de campo de vácuo para determinar a métrica.

Pelo método das geodésicas, começamos computando o quadrado da lagrangiana $\mathcal{L}$, dado por

$$
\mathcal{L}^2 = g_{\mu\nu} \dot{x}^\mu \dot{x}^\nu
\Rightarrow \mathcal{L}^2 = -e^{2\tau}\dot{t}^2 + e^{2\lambda}\dot{r}^2 + r^2\dot{\theta}^2 + r^2sen^2\theta\dot{\varphi}^2
$$

onde $\dot{x}^\alpha = \dfrac{dx^\alpha}{d\lambda}$, em que $\lambda$ é um parâmetro qualquer.

Em seguida, por meio da equação de Euler-Lagrange

$$
\dfrac{d}{d\lambda}\dfrac{\partial\mathcal{L}^2}{\partial \dot{x}^\alpha} - \dfrac{\partial\mathcal{L}^2}{\partial x^\alpha} = 0,
$$
obtêm-se o valor das conexões

$$
\begin{aligned}

(\Gamma^t_{\mu\nu}) &=
\left(\begin{matrix}
      0 & \tau' & 0 & 0 \\
      \tau' & 0 & 0 & 0 \\
      0 & 0 & 0 & 0 \\
      0 & 0 & 0 & 0
\end{matrix}\right)

\\

(\Gamma^r_{\mu\nu}) &=
\left(\begin{matrix}
      \tau'e^{(2\tau - 2\lambda)} & 0 & 0 & 0 \\
      0 & \lambda' & 0 & 0 \\
      0 & 0 & -r e^{-2\lambda} & 0 \\
      0 & 0 & 0 & -r e^{-2\lambda} sen^2\theta
\end{matrix}\right)

\\

(\Gamma^\theta_{\mu\nu}) &=
\left(\begin{matrix}
      0 & 0 & 0 & 0 \\
      0 & 0 & r^{-1} & 0 \\
      0 & r^{-1} & 0 & 0 \\
      0 & 0 & 0 & - \tfrac{1}{2} sen 2 \theta
\end{matrix}\right)

\\

(\Gamma^\varphi_{\mu\nu}) &=
\left(\begin{matrix}
      0 & 0 & 0 & 0 \\
      0 & 0 & 0 & r^{-1} \\
      0 & 0 & 0 & cotg \, \theta \\
      0 & r^{-1} & cotg \, \theta & 0
\end{matrix}\right)

\end{aligned}

$$

## Calculando o tensor de Ricci

De posse das conexões e da equação de campo no vácuo $R_{\mu\nu} = 0$, devemos apenas calcular o tensor de Ricci, que se expressa como

$$
R_{\mu\nu} = {R^\alpha}_{\mu\alpha\nu} =
      \Gamma^\alpha_{\mu\nu,\alpha} +
      \Gamma^\beta_{\mu\nu} \Gamma^\alpha_{\alpha\beta} -
      \Gamma^\alpha_{\alpha\mu,\nu} -
      \Gamma^\beta_{\alpha\mu} \Gamma^\alpha_{\beta\nu}
$$

Assim,

$$
\begin{aligned}
    t:
                      R_{tt} & = \Gamma^\alpha_{tt,\alpha} +
                                 \Gamma^r_{tt} \Gamma^\alpha_{\alpha r} -
                                 \Gamma^\alpha_{\alpha t, t} -
                                 \Gamma^\beta_{\alpha t} \Gamma^\alpha_{\beta t} \\
                             & = \Gamma^r_{tt,r}
                                 \Gamma^r_{tt} \Gamma^\alpha_{\alpha r} -
                                 \Gamma^r_{tt} \Gamma^t_{rt} -
                                 \Gamma^t_{tr} \Gamma^r_{tt} \\
                             & = (\tau'' - \lambda' \tau' + \tau'^2 + 2\tfrac{\tau'}{r}) e^{(2\tau - 2\lambda)}

\\

    r:
                      R_{rr} & = \Gamma^r_{rr,r} +
                                 \Gamma^r_{rr} \Gamma^\alpha_{\alpha r} -
                                 \Gamma^\alpha_{\alpha r, r} -
                                 \Gamma^\beta_{\alpha r} \Gamma^\alpha_{\beta r} \\
                             & = \Gamma^r_{rr,r}
                                 \Gamma^r_{rr} (\Gamma^r_{rr} + \Gamma^t_{rt} + \Gamma^\theta_{rt} + \Gamma^\varphi_{r\varphi}) -
                                 \Gamma^\alpha_{\alpha r, r} -
                                 ({\Gamma^r_{rr}}^2 + {\Gamma^t_{rt}}^2 + {\Gamma^\theta_{r\theta}}^2 + {\Gamma^\varphi_{r\varphi}}^2) \\
                             & = \lambda'\tau' -\tau'' -\tau'^2 + 2 \tfrac{\lambda'}{r}

\\

    \theta:
                      R_{\theta\theta} & = \Gamma^\alpha_{\theta\theta,\alpha} +
                                 \Gamma^\beta_{\theta\theta} \Gamma^\alpha_{\alpha\beta} -
                                 \Gamma^\alpha_{\alpha\theta, \theta} -
                                 \Gamma^\beta_{\alpha\theta} \Gamma^\alpha_{\beta\theta} \\
                             & = \Gamma^r_{\theta\theta,r}
                                 \Gamma^r_{\theta\theta} (\Gamma^r_{rr} + \Gamma^t_{rt} + \Gamma^\theta_{rt} + \Gamma^\varphi_{r\varphi}) -
                                 \Gamma^\varphi_{\varphi\theta,\theta} -
                                 2\Gamma^r_{\theta\theta}\Gamma^\theta_{r\theta} -
                                 \Gamma^\varphi_{\theta\varphi}\Gamma^\varphi_{\varphi\theta} \\
                             & = 1 - [1 + r(\tau' - \lambda')]e^{-2\lambda}

\\

    \varphi:
                      R_{\varphi\varphi} & = \Gamma^\alpha_{\varphi\varphi,\alpha} +
                                 \Gamma^\beta_{\varphi\varphi} \Gamma^\alpha_{\alpha\beta} -
                                 \Gamma^\alpha_{\alpha\varphi, \varphi} -
                                 \Gamma^\beta_{\alpha\varphi} \Gamma^\alpha_{\beta\varphi} \\
                             & = \Gamma^r_{\varphi\varphi,r} +
                                 \Gamma^\theta_{\varphi\varphi,\theta} +
                                 \Gamma^r_{\varphi\varphi} (\Gamma^r_{rr} + \Gamma^\theta_{r\theta} + \Gamma^t_{rt}) -
                                 \Gamma^r_{\varphi\varphi}\Gamma^\varphi_{r\varphi} -
                                 \Gamma^\theta_{\varphi\varphi}\Gamma^\varphi_{\theta\varphi} \\
                             & = R_{\theta\theta} sen^2 \theta

\\

    \mu \neq \nu: R_{\mu\nu} & = 0

\end{aligned}
$$

Chegamos, finalmente, ao sistema de equações diferenciais que temos que resolver

$$
\begin{cases}
      (\tau'' - \lambda' \tau' + \tau'^2 + 2\tfrac{\tau'}{r}) e^{(2\tau - 2\lambda)} = 0 \\
      \lambda'\tau' -\tau'' -\tau'^2 + 2 \tfrac{\lambda'}{r} = 0 \\
      1 - [1 + r(\tau' - \lambda')]e^{-2\lambda} = 0 \\
\end{cases}
$$

## Resolvendo o sistema

A segunda equação do sistema, $\lambda'\tau' -\tau'' -\tau'^2 + 2 \tfrac{\lambda'}{r} = 0$ pode ser reescrita na forma

$$
-\lambda'\tau' +\tau'' +\tau'^2 = 2 \tfrac{\lambda'}{r} \Rightarrow \tau'' - \lambda' \tau' + \tau'^2 = 2 \tfrac{\lambda'}{r}
$$

Assim, a primeira equação se torna

$$
\begin{aligned}
(2 \tfrac{\lambda' + \tau'}{r}) e^{(2\tau - 2\lambda)} = 0 & \Rightarrow \tfrac{\lambda' + \tau'}{r} = 0 \\
                                                           & \Rightarrow \lambda' + \tau' = 0 \\
                                                           & \Rightarrow \lambda + \tau = cte \\
\end{aligned}
$$

Agora, é razoável assumir que, para $r \gg R$, a métrica se torne plana, i.e.,

$$
\begin{aligned}
e^{2\tau} \approx e^{2\lambda} \approx 1 & \Rightarrow e^{2\tau + 2\lambda} = 1 \\
                                         & \Rightarrow e^{\tau + \lambda} = 1 \\
                                         & \Rightarrow \tau + \lambda = 0 \\
\end{aligned}
$$

Então, como $\lambda + \tau = cte, \forall r > R$ e $\lambda + \tau = 0, \forall r \gg R$, temos que

$$
\tau + \lambda = 0, \forall r > R
$$

Desse modo, a terceira equação do sistema se torna

$$
\begin{aligned}
1 - (1 + 2r\tau')e^{2\tau} = 0 & \Rightarrow (1 + 2r\tau')e^{2\tau} = 1 \\
                               & \Rightarrow (re^{2\tau})' = 1 \\
                               & \Rightarrow re^{2\tau} = r + C, \, C \in \mathbb{R}
\end{aligned}
$$

## Componentes da métrica e aproximação de campo fraco

De posse do resultado anterior, já é possível calcular cada componente da métrica,

$$
\begin{aligned}
g_{00} = -e^{2\tau} & = - (1 + \tfrac{C}{r}) \\
g_{11} = e^{2\lambda} & = (1 + \tfrac{C}{r})^{-1}
\end{aligned}
$$

Contudo, sabemos que, no limite Newtoniano, $g_{00} = -(1 + 2\Phi)$, onde $\Phi$ é o potencial gravitacional

$$
\Phi = - \tfrac{M}{r}
$$

Logo, tiramos que $C = - 2M$.

## Forma final da métrica de Schwarzschild e do elemento de linha

Finalmente, a partir das componentes calculadas, podemos escrever a **métrica de Schwarzschild** como

$$
(g_{\mu\nu}) = \left(\begin{matrix}
	- (1 - \tfrac{2M}{r}) & 0 & 0 & 0 \\
	0 & (1 - \tfrac{2M}{r})^{-1} & 0 & 0 \\
	0 & 0 & r^2 & 0 \\
	0 & 0 & 0 & r^2 sen^2 \theta
\end{matrix}\right)
$$

e o respectivo elemento de linha

$$
ds^2 = - (1 - \tfrac{2M}{r}) dt^2 + (1 - \tfrac{2M}{r})^{-1} dr^2 + r^2 (d\theta^2 + sin^2\theta d\varphi^2)
$$

Desse modo, está demonstrada a métrica de Schwarzschild para a região externa de um corpo massivo, estático e esfericamente simétrico.