---
layout: single
excerpt: "sqrt, sqrtm, power or cpower?"
title: Working with square roots
tags: [Second-order cone programming, Typical problems]
comments: true
date: '2009-08-29'
---

One of the strengths in YALMIP is the built-in convexity analysis and modelling framework for conic optimization. The command [sqrt] is implemented in YALMIP as a convexity aware [nonlinear operator]. If you use the positive increasing concave operator [sqrt] in a way that satisfies the implemented rules for preserving convexity (maximize it, bound it from below,...), [sqrt] will be implemented using second-order cone constraints, 

$$
\sqrt{x} \geq t \Leftrightarrow x\geq t^2 \Leftrightarrow  \left\| \begin{matrix}1-x\\2t\end{matrix}\right\|\leq 1+x 
$$

However, in many cases you may want to use a square-root in a nonconvex fashion, and solve the problem using a general-purpose nonlinear solver, such as [FMINCON]. In these situations, you do not want YALMIP to fail due to convexity propagation problems. In other cases, it might be the case that your model satisfies all convexity requirements, but you still want to solve the problem using [FMINCON], thus you do not want YALMIP to try to model the [sqrt] operator using second order cones.

The remedy to these situations is to use the operator [sqrtm] instead. The [sqrtm] operator is implemented as an [evaluation based nonlinear operator], and will therefore not generate any second-order cone constraints. Furthermore, the [sqrtm] operator does not require convexity.

As an example, consider the following problem. This model will be converted to and solved as a second-order cone program, since [sqrt] is used in compliance with convexity rules.

````matlab
x = sdpvar(3,1);
A = randn(3,3);A = A*A';

obj = x'*A*x - sqrt(sum(x));
F   = [1 <= x <= 2];
optimize(F,obj)
````

The following problem will however fail.

````matlab
obj = x'*A*x + sqrt(sum(x));
F   = [1 <= x <= 2];
optimize(F,obj)
````

By using the [sqrtm] operator instead, a general nonlinear problem is set up, and [FMINCON] is called.

````matlab
obj = x'*A*x + sqrtm(sum(x));
F   = [1 <= x <= 2];
optimize(F,obj)
````

Finally, we also note that square roots can be implemented using powers, such as **x^0.5**. This should be reserved for situations where you aim for a [geometric programming](/tutorial/geometricprogramming) approach.

Another related command is [cpower] which implements a conic model of powers,obviously reserved to convex cases where you intend to use a conic solver.
