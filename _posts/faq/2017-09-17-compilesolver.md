---
layout: single
category: faq
author_profile: false
excerpt: 
title: Compiling YALMIP with a solver does not work
tags:
comments: true
date: '2016-09-17'
sidebar:
  nav:
---

When compiling, you need to add some files to your include list. As an example, for [SEDUMI], you have to add the files **sedumi.m**, **ada_pcg.m** and **install_sedumi.m**. These are the files YALMIP checks for when detecting existence of [SEDUMI]. In addition to these files needed for the detection, the gateway to SeDuMi from YALMIP has to be added, **callsedumi.m**. For other solvers, see the file **definesolvers.m**. Files listed in the call and checkfor fields have to be added
