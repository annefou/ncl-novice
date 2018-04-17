---
title: "Introduction"
teaching: 0
exercises: 0
questions:
- "What is NCL?"
objectives:
- "Learn how to start NCL"
- "The netCDF data model"
keypoints:
- "NCL and its netCDF data model"
---

# What is NCL?

NCAR Command Language is an Integrated Processing Environment.
NCL syntax is close to python or matlab.

<img src="../fig/whatis-ncl.png" width="80%">

~~~
;================================================;
;  maponly_1.ncl
;================================================;
;
; Concepts illustrated:
;   - Drawing a default cylindrical equidistant map
;
;================================================;
;
; These files are loaded by default in NCL V6.2.0 and newer
; load "$NCARG_ROOT/lib/ncarg/nclscripts/csm/gsn_code.ncl"   
; load "$NCARG_ROOT/lib/ncarg/nclscripts/csm/gsn_csm.ncl"   
; ================================================;
begin

  wks  = gsn_open_wks("png","maponly")    ; send graphics to PNG file
  plot = gsn_csm_map(wks,False)        ; draw global map

  end
~~~

Ncl is an interpreted language (not compiled)

- Like python, R, matlab
- Unlike C, C++, fortran
- Many operations implemented in C/fortran under
the hood = fast performance
- Interpreter is invoked via the “ncl” command:

~~~
$ ncl
~~~
{: .language.bash}

~~~
 Copyright (C) 1995-2015 - All Rights Reserved
 University Corporation for Atmospheric Research
 NCAR Command Language Version 6.3.0
 The use of this software is governed by a License Agreement.
 See http://www.ncl.ucar.edu/ for more details.
ncl 0>
~~~
{: .output}

# How to run it / what’s required to run it

# The NetCDF data model à NCL’s data model

# Language Syntax

# Array indexing, coordinate variables, attributes, data types

# control-of-flow constructs

# Printing

# Debugging

