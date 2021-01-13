---
title: "Laplace's Equation in Spherical Coordinates"
date: 2020-12-20
tags: [math]
excerpt: "Transforming Laplace's equation from cartesian to spherical coordinates."
mathjax: "true"
comments_id: 2
---

# Table of Contents

1. [Summary](#summary)
2. [Spherical Coordinates](#spherical_coordinates)
3. [Transforming to Spherical Coordinates](#transform)
4. [Table of Derivatives](#derivatives)

# Summary <a name="summary"></a>

Laplace's equation is a second order elliptic partial differential equation defined in cartesian coordinates as:

$$
\Delta f = \nabla \cdot \nabla f = \frac{\partial^2f}{\partial x^2} + \frac{\partial^2f}{\partial y^2} + \frac{\partial^2f}{\partial z^2} = 0
$$

Where $f = f(x,y,z)$ is a real-valued function and twice differentiable. Solutions to Laplace's equation are often called harmonic functions.

 It's possible to represent this equation in other coordinate systems, such as cylindrical or spherical coordinates. In spherical coordinates, the solution to Laplace's equation are called spherical harmonics and are often used in computer graphics to store lighting information.

This post will explain how to derive Laplace's equation in spherical coordinates:

$$
\Delta f = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial f}{\partial r} \right)  + \frac{1}{r^2 \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial f}{\partial \theta} \right) + \frac{1}{r^2 \sin^2 \theta} \frac{\partial^2 f}{\partial \varphi^2}
$$

$~$

# Spherical Coordinates <a name="spherical_coordinates"></a>

To go from cartesian coordinates to spherical coordinates we need the following transform:

$$
\begin{align}

x &= r\sin\theta\cos\varphi \\
y &= r\sin\theta\sin\varphi \\
z &= r\cos\theta

\end{align}
$$

Where $r > 0, \; \theta \in [0, \pi],\; \varphi \in [0, 2\pi]$. The inverse transform is:

$$
\begin{align}

r &= \sqrt{x^2 + y^2 + z^2} \\
\theta &= \arccos \left( \frac{z}{\sqrt{x^2 + y^2 + z^2}}  \right) \\
\varphi &= \arctan \left( \frac{y}{x}  \right)

\end{align}
$$

# Transforming to Spherical Coordinates <a name="transform"></a>

The first step is to use the chain rule on the equation in cartesian coordinates.

$$
\frac{\partial^2f}{\partial x^2} = \frac{\partial}{\partial x} \left( \frac{\partial f}{\partial x} \right) = \frac{\partial r}{\partial x} \frac{\partial}{\partial r} \left( \frac{\partial f}{\partial x}  \right) + \frac{\partial \theta}{\partial x} \frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial x}  \right)  \frac{\partial \varphi}{\partial x} \frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial x}  \right) 
$$

We can obtain similar results for $y$ and $z$. Since we don't have a solution, we need to use the chain rule on $f$ again and break it down into components that depend on the derivatives of $f$ with respect to $r, \theta, \varphi$. Once we have computed all the terms independently, we can replace in the equation above, for $x, y, z$ and simplify to obtain the desired result.

To obtain $\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}, \frac{\partial f}{\partial z}$ in terms of $\frac{\partial f}{\partial r}, \frac{\partial f}{\partial \theta}, \frac{\partial f}{\partial \varphi}$, we will need the transform from spherical to cartesian coordinates and differentiate them. it produces 9 different derivatives:

$$
\begin{align}

\frac{\partial r}{\partial x} &= \frac{x}{r}, &&\frac{\partial \theta}{\partial x} = \frac{xz}{(x^2+y^2+z^2)^{3/2} \sqrt{1 - \frac{z^2}{\sqrt{x^2+y^2+z^2}}}},  &&\frac{\partial \varphi}{\partial x} = -\frac{y}{x^2 + y^2} \\

\frac{\partial r}{\partial y} &= \frac{y}{r}, &&\frac{\partial \theta}{\partial y} = \frac{yz}{(x^2+y^2+z^2)^{3/2} \sqrt{1 - \frac{z^2}{\sqrt{x^2+y^2+z^2}}}}, &&\frac{\partial \varphi}{\partial y} = \frac{x}{x^2 + y^2} \\

\frac{\partial r}{\partial z} &= \frac{z}{r}, &&\frac{\partial \theta}{\partial z} = \frac{\frac{1}{\sqrt{x^2+y^2+z^2}} - \frac{z^2}{(x^2+y^2+z^2)^{3/2}}}{ \sqrt{1 - \frac{z^2}{\sqrt{x^2+y^2+z^2}}}}, &&\frac{\partial \varphi}{\partial z} = 0

\end{align}

$$

Which we then need to write in terms of $r, \theta, \varphi$, using the spherical coordinates transform:

$$
\begin{align}

\frac{\partial r}{\partial x} &= \sin\theta\cos\varphi, &&\frac{\partial \theta}{\partial x} = \frac{\cos\theta\cos\varphi}{r},  &&\frac{\partial \varphi}{\partial x} = -\frac{\sin\varphi}{r\sin\theta} \\

\frac{\partial r}{\partial y} &= \sin\theta\sin\varphi, &&\frac{\partial \theta}{\partial y} = \frac{\cos\theta\sin\varphi}{r}, &&\frac{\partial \varphi}{\partial y} = \frac{\cos\varphi}{r\sin\theta} \\

\frac{\partial r}{\partial z} &= \cos\theta, &&\frac{\partial \theta}{\partial z} = -\frac{\sin\theta}{r}, &&\frac{\partial \varphi}{\partial z} = 0

\end{align}

$$

This allows us to compute

$$
\frac{\partial f}{\partial x} = \frac{\partial r}{\partial x} \frac{\partial f}{\partial r} + \frac{\partial \theta}{\partial x} \frac{\partial f}{\partial \theta} + \frac{\partial \varphi}{\partial x} \frac{\partial f}{\partial \varphi}
$$

$$
\frac{\partial f}{\partial x} = \sin\theta\cos\varphi\frac{\partial f}{\partial r} + \frac{\cos\theta\cos\varphi}{r} \frac{\partial f}{\partial \theta} -\frac{\sin\varphi}{r\sin\theta} \frac{\partial f}{\partial \varphi}
$$

Derivatives for $y$ and $z$ are shown in the [derivatives table](#derivatives) at the end of this post. The next step is to take the derivative of $\frac{\partial f}{\partial x}$ with respect to $r, \theta, \varphi$:

$$
\frac{\partial}{\partial r} \left( \frac{\partial f}{\partial x}  \right) =
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r^2} -
\frac{\cos\theta\cos\varphi}{r^2} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial r \partial \theta} +
\frac{\sin\varphi}{r^2 \sin\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial r \partial \varphi}

$$

$$
\frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial x}  \right) =
\cos\theta\cos\varphi \frac{\partial f}{\partial r} +
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r \partial \theta}-
\frac{\sin\theta\cos\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial \theta^2} +
\frac{\cos\theta\sin\varphi}{r^2 \sin^2\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \theta \partial \varphi}

$$

$$
\frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial x}  \right) =
-\sin\theta\sin\varphi \frac{\partial f}{\partial r} +
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r \partial \varphi}-
\frac{\cos\theta\sin\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial \theta \partial \varphi} -
\frac{\cos\varphi}{r \sin\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \varphi^2}

$$

With this, we have everything needed to compute $\Delta f$ in spherical coordinates. One easy way is to group terms by derivatives in spherical coordinates. Most of them end up being 0, except $\frac{\partial f}{\partial r}$, $\frac{\partial^2 f}{\partial r^2}$, $\frac{\partial f}{\partial \theta}$, $\frac{\partial^2 f}{\partial \theta^2}$ and $\frac{\partial^2 f}{\partial \varphi^2}$. Adding all the non-zero terms gives:

$$
\Delta f = \frac{2}{r} \frac{\partial f}{\partial r} + \frac{\partial^2 f}{\partial r^2}  + \frac{\cos\theta}{r^2 \sin \theta} \frac{\partial f}{\partial \theta} + \frac{1}{r^2} \frac{\partial^2 f}{\partial \theta^2}  + \frac{1}{r^2 \sin^2 \theta} \frac{\partial^2 f}{\partial \varphi^2}
$$


Which can be simplified to:

$$
\Delta f = \frac{1}{r^2} \frac{\partial}{\partial r} \left( r^2 \frac{\partial f}{\partial r} \right)  + \frac{1}{r^2 \sin \theta} \frac{\partial}{\partial \theta} \left( \sin \theta \frac{\partial f}{\partial \theta} \right) + \frac{1}{r^2 \sin^2 \theta} \frac{\partial^2 f}{\partial \varphi^2}
$$

$~$

$~$

# Table of Derivatives <a name="derivatives"></a>

## Second-order derivatives in terms of first-order derivatives with mixed terms

$$
\frac{\partial^2f}{\partial x^2} = \frac{\partial}{\partial x} \left( \frac{\partial f}{\partial x} \right) = \frac{\partial r}{\partial x} \frac{\partial}{\partial r} \left( \frac{\partial f}{\partial x}  \right) + \frac{\partial \theta}{\partial x} \frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial x}  \right)  \frac{\partial \varphi}{\partial x} \frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial x}  \right) 
$$

$$
\frac{\partial^2f}{\partial y^2} = \frac{\partial}{\partial y} \left( \frac{\partial f}{\partial y} \right) = \frac{\partial r}{\partial y} \frac{\partial}{\partial r} \left( \frac{\partial f}{\partial y}  \right) + \frac{\partial \theta}{\partial y} \frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial y}  \right)  \frac{\partial \varphi}{\partial y} \frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial y}  \right) 
$$

$$
\frac{\partial^2f}{\partial z^2} = \frac{\partial}{\partial z} \left( \frac{\partial f}{\partial z} \right) = \frac{\partial r}{\partial z} \frac{\partial}{\partial r} \left( \frac{\partial f}{\partial z}  \right) + \frac{\partial \theta}{\partial z} \frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial z}  \right)  \frac{\partial \varphi}{\partial z} \frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial z}  \right) 
$$


## First-order cartesian derivatives of $f$ in terms of spherical derivatives


$$
\begin{align}

\frac{\partial f}{\partial x} &= \sin\theta\cos\varphi\frac{\partial f}{\partial r} + \frac{\cos\theta\cos\varphi}{r} \frac{\partial f}{\partial \theta} -\frac{\sin\varphi}{r\sin\theta} \frac{\partial f}{\partial \varphi} \\

\frac{\partial f}{\partial y} &= \sin\theta\sin\varphi\frac{\partial f}{\partial r} + \frac{\cos\theta\sin\varphi}{r} \frac{\partial f}{\partial \theta} + \frac{\cos\varphi}{r\sin\theta} \frac{\partial f}{\partial \varphi} \\

\frac{\partial f}{\partial z} &= \cos\theta\frac{\partial f}{\partial r} - \frac{\sin\theta}{r} \frac{\partial f}{\partial \theta}
\end{align}

$$

## Second-order mixed derivatives

$$

\begin{align}

\frac{\partial}{\partial r} \left( \frac{\partial f}{\partial x}  \right) &=
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r^2} -
\frac{\cos\theta\cos\varphi}{r^2} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial r \partial \theta} +
\frac{\sin\varphi}{r^2 \sin\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial r \partial \varphi} \\

\frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial x}  \right) &=
\cos\theta\cos\varphi \frac{\partial f}{\partial r} +
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r \partial \theta}-
\frac{\sin\theta\cos\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial \theta^2} +
\frac{\cos\theta\sin\varphi}{r^2 \sin^2\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \theta \partial \varphi} \\

\frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial x}  \right) &=
-\sin\theta\sin\varphi \frac{\partial f}{\partial r} +
\sin\theta\cos\varphi \frac{\partial ^2 f}{\partial r \partial \varphi}-
\frac{\cos\theta\sin\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\cos\varphi}{r} \frac{\partial^2 f}{\partial \theta \partial \varphi} -
\frac{\cos\varphi}{r \sin\theta} \frac{\partial f}{\partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \varphi^2}

\end{align}

$$

$$

\begin{align}

\frac{\partial}{\partial r} \left( \frac{\partial f}{\partial y}  \right) &=
\sin\theta\sin\varphi \frac{\partial ^2 f}{\partial r^2} -
\frac{\cos\theta\sin\varphi}{r^2} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\sin\varphi}{r} \frac{\partial^2 f}{\partial r \partial \theta}-
\frac{\cos\varphi}{r^2 \sin\theta} \frac{\partial f}{\partial \varphi} +
\frac{\cos\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial r \partial \varphi} \\

\frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial y}  \right) &=
\cos\theta\sin\varphi \frac{\partial f}{\partial r} +
\sin\theta\sin\varphi \frac{\partial ^2 f}{\partial r \partial \theta}-
\frac{\sin\theta\sin\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\sin\varphi}{r} \frac{\partial^2 f}{\partial \theta^2} -
\frac{\cos\theta\cos\varphi}{r^2 \sin^2\theta} \frac{\partial f}{\partial \varphi} +
\frac{\cos\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \theta \partial \varphi} \\

\frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial y}  \right) &=
\sin\theta\cos\varphi \frac{\partial f}{\partial r} +
\sin\theta\sin\varphi \frac{\partial ^2 f}{\partial r \partial \varphi}-
\frac{\cos\theta\cos\varphi}{r} \frac{\partial f}{\partial \theta} +
\frac{\cos\theta\sin\varphi}{r} \frac{\partial^2 f}{\partial \theta \partial \varphi} -
\frac{\sin\varphi}{r \sin\theta} \frac{\partial f}{\partial \varphi} +
\frac{\cos\varphi}{r \sin\theta} \frac{\partial^2 f}{\partial \varphi^2}
\end{align}


$$


$$

\begin{align}

\frac{\partial}{\partial r} \left( \frac{\partial f}{\partial z}  \right) &=
\cos\theta\frac{\partial ^2 f}{\partial r^2} +
\frac{\sin\theta}{r^2} \frac{\partial f}{\partial \theta} -
\frac{\sin\theta}{r} \frac{\partial^2 f}{\partial r \partial \theta} \\

\frac{\partial}{\partial \theta} \left( \frac{\partial f}{\partial z}  \right) &=
-\sin\theta\frac{\partial f}{\partial r} +
\cos\theta \frac{\partial ^2 f}{\partial r \partial \theta}-
\frac{\cos\theta}{r} \frac{\partial f}{\partial \theta} -
\frac{\sin\theta}{r} \frac{\partial^2 f}{\partial \theta^2} \\


\frac{\partial}{\partial \varphi} \left( \frac{\partial f}{\partial z}  \right) &=
\cos\theta\frac{\partial ^2 f}{\partial r \partial \varphi} -
\frac{\sin\theta}{r} \frac{\partial^2 f}{\partial \theta \partial \varphi} 

\end{align}
$$

# References
- [https://en.wikipedia.org/wiki/Laplace%27s_equation]()

 