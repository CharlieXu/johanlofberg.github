---
layout: single
category: command
author_profile: false
excerpt: "Export model to SDPA ASCII file"
title: savesdpafile
tags: [Export]
comments: true
date: '2016-09-17'
sidebar:
  nav: "commands"
---

[savesdpafile] exports a YALMIP model to SDPA ASCII format

### Syntax

````matlab
savesdpafile(F,h,filename)
````

### Examples

Export SDP problem to ASCII file

````matlab
A = randn(3,3);A = -A*A';
P = sdpvar(3,3);
F = [P>0, A'*P+P*A <= -eye(3)];
savesdpafile(F,trace(P),'mysdpamodel');
````

### Comments

The SDPA ASCII format is limited (equalities and second order cones are not supported), hence many YALMIP models will fail to be saved.

If you have equalities in your model, you can circumvent this by telling YALMIP to eliminate them by using the option *removeequalities* (see details [sdpsettings])
