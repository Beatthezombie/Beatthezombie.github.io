---
title: "Solution to Laplace's Equation"
date: 2021-01-13
tags: [math]
excerpt: "Solving Laplace's equation in spherical coordinates."
mathjax: "true"
comments_id: 3
---
*Disclaimer: The following proofs are not rigorous and skip over important steps to make the post easier to read. Full proofs can be found online.*

# Table of Contents

1. [Summary](#summary)
2. [Solving Laplace's Equation](#laplace)
    1. [Solution for the Equation Depending on $\varphi$](#sol_varphi)
    2. [Solution for the Equation Depending on $r$](#sol_r)
    3. [Solution for the Equation Depending on $\theta$](#sol_theta)
    4. [Solution to Laplace's Equation](#final_sol)

# Summary <a name="summary"></a>

In this post I'll show the steps to solve Laplace's equation in spherical coordinates. The reason is the solution contains the definition of spherical harmonics and requires the associated Legendre differential equation which we solved previously in this [post](https://beatthezombie.github.io/legendre/). Spherical harmonics have some very interesting properties that I will present in a future post.

We start with Laplace's equation:
$$
\Delta f = \nabla \cdot \nabla f = \frac{\partial^2f}{\partial x^2} + \frac{\partial^2f}{\partial y^2} + \frac{\partial^2f}{\partial z^2} = 0
$$

we convert it to spherical coordinates $(r, \theta, \varphi)$ then we show that the solution is:

$$
f(r, \theta, \varphi) =  \sum_{\ell = 0}^{\infty} \sum_{m = -\ell}^{\ell} \left( B_{\ell m} r^\ell + \frac{C_{\ell m} }{r^{\ell  + 1}} \right)P_\ell^m(\cos\theta) e^{im\varphi}
$$


# Laplace Equation <a name="laplace"></a>

We start with Laplace's equation in spherical coordinates. A detailed post about how to convert Laplace's equation from cartesian to spherical coordinates is available [here](https://beatthezombie.github.io/laplace_equation_spherical/).

$$
\Delta f = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial f}{\partial r} \right)  + \frac{1}{r^2 \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta\frac{\partial f}{\partial \theta} \right) + \frac{1}{r^2 \sin^2 \theta} \frac{\partial^2 f}{\partial \varphi^2} = 0
$$

To simplify the equation, we can multiply by $r^2$ on both sides. Since this is a second order partial differential equation, we can try the separation of variables methods, where we assume the solution is of the form:

$$f(r, \theta, \varphi) = R(r)Y(\theta, \varphi)$$

We then use the chain rule on the derivatives of $f$ to express them in terms of $R$ and $Y$.

$$
\frac{\partial f}{\partial r} = \frac{\partial f}{\partial R} \frac{dR}{dr} = Y(\theta, \varphi) \frac{dR}{dr}
$$

$$
\frac{\partial f}{\partial \theta} = \frac{\partial f}{\partial Y} \frac{\partial Y}{\partial \theta} = R(r) \frac{\partial Y}{\partial \theta}
$$

$$
\frac{\partial^2 f}{\partial \varphi^2} = \frac{\partial }{\partial \varphi} \left(\frac{\partial f}{\partial \varphi} \right) =R(r) \frac{\partial^2 Y}{\partial \varphi^2}
$$

Replacing the derivatives and reorganizing in the original equation:

$$
Y(\theta, \varphi)\frac{d}{d r} \left( r^2 \frac{dR}{dr} \right)  +
 \frac{R(r)}{\sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial Y}{\partial \theta} \right) +
  \frac{R(r)}{\sin^2 \theta} \frac{\partial^2 Y}{\partial \varphi^2} = 0
$$

$$
\frac{1}{R(r)}\frac{d}{d r} \left( r^2 \frac{dR}{dr} \right)  +
 \frac{1}{Y(\theta, \varphi) \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial Y}{\partial \theta} \right) +
  \frac{1}{Y(\theta, \varphi) \sin^2 \theta} \frac{\partial^2 Y}{\partial \varphi^2} = 0
$$


We can then separate the $r$ components from the $\theta, \varphi$ using a constant:

$$
\frac{1}{R(r)}\frac{d}{d r} \left( r^2 \frac{dR}{dr} \right) = c_1
$$

$$
\frac{1}{Y(\theta, \varphi) \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial Y}{\partial \theta} \right) +
\frac{1}{Y(\theta, \varphi) \sin^2 \theta} \frac{\partial^2 Y}{\partial \varphi^2} = -c_1
$$

The first equation is now an ordinary differential equation. The second equation is still a partial differential equation so we apply a separation of variables again with:

$$Y(\theta, \varphi) = \Theta(\theta)\Phi(\varphi) $$

Similarly after replacing the derivatives and simplifying:

$$
\Theta(\theta)\Phi(\varphi)c_1 \sin^2 \theta  + 
\Phi(\varphi) \sin \theta \frac{d}{d \theta} \left( \sin \theta \frac{d \Theta}{d\theta} \right) +
\Theta(\theta) \frac{d^2 \Phi}{d \varphi^2} = 0
$$

$$
c_1\sin^2 \theta  + 
\frac{1}{\Theta(\theta)} \sin \theta \frac{d}{d \theta} \left( \sin \theta \frac{d \Theta}{d\theta} \right) +
\frac{1}{\Phi(\varphi)} \frac{d^2 \Phi}{d \varphi^2} = 0
$$

We can separate the $\theta$ components from $\varphi$ using a new constant:

$$
c_1\sin^2 \theta  + 
\frac{1}{\Theta(\theta)} \sin \theta \frac{d}{d \theta} \left( \sin \theta \frac{d \Theta}{d\theta} \right) = c_2
$$

$$
\frac{1}{\Phi(\varphi)} \frac{d^2 \Phi}{d \varphi^2} = -c_2
$$


## Solution for the Equation Depending on $\varphi$ <a name="sol_varphi"></a>

Now that all our equations are ordinary differential equation, we can start solving them. The easiest one to solve is the equation in $\Phi$.

$$
\frac{d^2 \Phi}{d \varphi^2} + \Phi(\varphi)c_2= 0 
$$

This is a common ODE and is solved using the characteristic equation. Making an educated guess, let's make $c_2 = m^2$. Solving the ODE gives us 2 complex solutions but using this form we can write it as one:

$$\Phi(\varphi) = a_m e^{im\varphi}$$

Where $a_m$ is some constant, $m$ can be position or negative. This solution is periodic, with period $2\pi$.

## Solution for the Equation Depending on $r$ <a name="sol_r"></a>

The next ODE to solve is:

$$
\frac{1}{R(r)}\frac{d}{d r} \left( r^2 \frac{dR}{dr} \right) = c_1
$$

This one can be solved using a power series. Let's start with $R(r) = r^\ell$ where $\ell$ is an integer. After substituting in the equation we get:

$$ (\ell(\ell+1) - c_1) = 0 $$

$$ \ell^2 + \ell - c_1 = 0$$

There we can set $c_1 = \ell(\ell+1)$. Notice that $\ell$ and $-(\ell + 1)$ will both result in $c_1 = \ell(\ell+1)$ therefore we have two solutions in the power series:

$$ R(r) = \sum_{\ell = 0}^\infty \left( B_\ell r^\ell + \frac{C_\ell }{r^{\ell  + 1}} \right)$$

## Solution for the Equation Depending on $\theta$ <a name="sol_theta"></a>

The last equation to solve is:

$$
\ell(\ell+1)\sin^2 \theta  + 
\frac{1}{\Theta(\theta)} \sin \theta \frac{d}{d \theta} \left( \sin \theta \frac{d \Theta}{d\theta} \right) = m^2
$$

Which can be rewritten as:

$$ 
\frac{1}{\sin \theta}  \frac{d}{d \theta} \left( \sin \theta \frac{d \Theta}{d\theta} \right) + \left(\ell(\ell+1) - \frac{m^2}{\sin^2\theta}\right) \Theta= 0
$$

This is quite similar to the associated Legendre differential equation. Let's do a change of variable with $x=\cos\theta$. Computing the derivatives gives us:

$$
\frac{dx}{d\theta} = -\sin\theta = - \sqrt{1 - x^2}, \quad \frac{d}{d\theta} = - \sqrt{1 - x^2} \frac{d}{dx}
$$

The differential equation can then be written in terms of $x$:

$$ 
\frac{d}{dx} \left( (1-x^2) \frac{d \Theta}{dx} \right) + \left(\ell(\ell+1) - \frac{m^2}{1 -x ^2}\right) \Theta= 0
$$

$$ 
(1-x^2)\frac{d^2\Theta}{dx^2} -
2x \frac{d \Theta}{dx}  +
\left(\ell(\ell+1) - \frac{m^2}{1 -x ^2}\right) \Theta= 0
$$

Which is exactly the associated Legendre differential equation. A detailed derivation of the solution is available in [this post](https://beatthezombie.github.io/legendre/). From the associated Legendre polynomials, we have:

$$\Theta(\theta) = P_\ell^m(\cos\theta) $$

Where $\ell, m$ are integers, $\ell\geq 0$ and $0 \leq m \leq \ell$. This constrains $P_\ell ^m$ to be a polynomial.

$~$

## Solution to Laplace's Equation <a name="final_sol"></a>

We found that:

$$ R(r) = \sum_{\ell = 0}^\infty \left( B_\ell r^\ell + \frac{C_\ell }{r^{\ell  + 1}} \right)$$

And

$$
Y(\theta, \varphi) =  \Theta(\theta)\Phi(\varphi) = a_m e^{im\varphi}P_\ell^m(\cos\theta)
$$

Note that the solution to the angular part, $Y(\theta, \varphi)$ will be used to define spherical harmonics of degree $\ell$ and order $m$. For fixed $m, \ell$ we have the following solution:

$$
f(r, \theta, \varphi) = \left( B_{\ell m} r^\ell + \frac{C_{\ell m} }{r^{\ell  + 1}} \right)P_\ell^m(\cos\theta) e^{im\varphi}
$$

Which results from the separation of variable method. $B_{\ell m}$ and $C_{\ell m}$ are constants that have been combined and depend on $m$ and $\ell$. They  need to be determined using the boundary conditions of a specific problem. Since we have infinitely many solutions, the sum over all $m$ and $\ell$ is also a solution:

$$
f(r, \theta, \varphi) =  \sum_{\ell = 0}^{\infty} \sum_{m = 0}^{\ell} \left( B_{\ell m} r^\ell + \frac{C_{\ell m} }{r^{\ell  + 1}} \right)P_\ell^m(\cos\theta) e^{im\varphi}
$$

We can extend the range of $m$ by using:

$$
P_\ell^{-m}(x) = (-1)^m \frac{(\ell-m)!}{(\ell+m)!}P_\ell^m(x)
$$

Which comes from the properties of associated Legendre polynomials. Our final solution is then:

$$
f(r, \theta, \varphi) =  \sum_{\ell = 0}^{\infty} \sum_{m = -\ell}^{\ell} \left( B_{\ell m} r^\ell + \frac{C_{\ell m} }{r^{\ell  + 1}} \right)P_\ell^m(\cos\theta) e^{im\varphi}
$$


# References
- [https://en.wikipedia.org/wiki/Laplace%27s_equation]()
- [http://www.physics.usu.edu/Wheeler/EM3600/Notes11SeparationOfVariablesSpherical.pdf]()
 