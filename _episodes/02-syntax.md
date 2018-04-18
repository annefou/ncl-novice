---
title: "NCL language syntax"
teaching: 0
exercises: 0
questions:
- "What is NCL syntax?"
objectives:
- "Learn about NCL syntax"
- "Learn to read a netCDF file"
- "Learn to write variables to netCDF file"
- "Learn to iterate over files"
keypoints:
- "NCL main syntax language"
- "Read and write netCDF files with NCL"
- "Loop over a large number of netCDF files"
---

# Language Syntax

## NCL control construct

The syntax is very close to the Fortran syntax:

~~~
if (a.eq.b) then
…
else
…
end if
~~~
{: .language-bash}

A simple do loop:

~~~
do i=0,99
…
end do
~~~
{: .language-bash}

Or you can use a `while` loop with a condition to exit the loop:

~~~
do while(a.gt.0)
...
end do
~~~
{: .language-bash}

The condition is specified in brackets and must be a logical (TRUE/FALSE).

For example, let's loop over all the netCDF files available in the current directory:

~~~
files = systemfunc("ls *.nc") ; NetCDF file names 

do nf=0,dimsizes(files)-1
  print(files(nf))
end do
~~~
{: .language-bash}

We used the built-in NCL function `systemfunc` which allows to make system calls i.e. any available bash statement. 
In our example, it returns a vector containing the names of all the netCDF files listed in the current directory.

Then to access a single element, use the NCL array syntax i.e. index specified within brackets.

### Built-in functions

We used a built-in function (`systemfunc`) and NCL is a very rich language containing a large number of built-in functions. It would not be possible to enumerate all of them here, so the best is to refer to the NCL documentation [here](https://www.ncl.ucar.edu/Document/Functions/Built-in/).

### User-defined functions

To make your code more modular, you can define your own functions:

~~~
function plus2(i)
begin
  return i+2
end
~~~
{: .language-bash}

Then you can call this function:
~~~
print(plus2(3))
~~~
{: .language-bash}

~~~
(0)     5
~~~
{: .output}

### NCL main syntax characters

* `=` - assignment
* `:=` - reassignment (allow to change the shape and content of a variable)
~~~

aInt= (/1,3,4/)
print(aInt)
aInt=5  ; assign all the 3 values to 5 but keep aInt vector dimension
print(aInt)
aInt:=5 ; erase aInt and create a new scalar variable containing one value only
print(aInt)
~~~
{: .language-bash}

~~~
ncl 9> aInt = (/1,3,4/)
ncl 10> print(aInt)
Variable: aInt
Type: integer
Total Size: 12 bytes
            3 values
Number of Dimensions: 1
Dimensions and sizes:   [3]
Coordinates:
(0)     1
(1)     3
(2)     4
ncl 11> aInt=5
ncl 12> print(aInt)


Variable: aInt
Type: integer
Total Size: 12 bytes
            3 values
Number of Dimensions: 1
Dimensions and sizes:   [3]
Coordinates:
(0)     5
(1)     5
(2)     5
ncl 13> aInt:=5
ncl 14> print(aInt)


Variable: aInt
Type: integer
Total Size: 4 bytes
            1 values
Number of Dimensions: 1
Dimensions and sizes:   [1]
Coordinates:
(0)     5

~~~
{: .output}

* `;` - comment [can appear anywhere; text to right ; ignored]
* `/;` .. `;/` - comment block; typically text spanning multiple lines
* `->` - use to (im/ex)port variables via addfile(s) function(s)
* `@` - access/create attributes
* `!` - access/create named dimension
* `&` - access/create coordinate variable
* `{…}` - coordinate subscripting
* `$...$` - enclose strings when (im/ex)port variables via addfile(s)
* `(/../)` - array construction (variable); remove meta data
* `[/../]` - list construction;
* `[:]` - all elements of a list
* `:` - array syntax
* `|` - separator for named dimensions
* `\` - continue character [statement to span multiple lines]
* `::` - syntax for external shared objects (eg, fortran/C)
* `.` - access elements of a hdf5 (compound) group

# Array indexing, coordinate variables, attributes, data types

# control-of-flow constructs

# Printing

# Debugging

