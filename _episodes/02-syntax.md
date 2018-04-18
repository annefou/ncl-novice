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

~~~
; This is a comment on one single line
x=10 ; this is also a comment
/; this is a comment
   and you can expand it over several lines
;/
~~~
{: .language-bash}

* `->` - use to (im/ex)port variables via addfile(s) function(s)

~~~
f = addfile("f2000.T31T31.control.cam.h0.0008-12-22-00000.nc","r")
T = f->T
~~~
{: .language-bash}

* `@` - access/create attributes

~~~
print(T@units)
print(T@long_name)
~~~
{: .language-bash}

* `!` - access/create named dimension
In NCL, dimensions are ordered using row x column ordering [ie, row major], which is identical to C. By convention, dimensions are numbered from left(0) to right(n-1) where n is the total number of dimensions. NCL allows names to be assigned with dimensions. These named dimensions are essential for reordering an array. A named dimension is created by entering the variable name followed by the ! character, followed by the appropriate dimension index.

~~~
print(T!0)
~~~
{: .language-bash}

~~~
(0)     time
~~~
{: .output}

* `&` - access/create coordinate variable

~~~
print(T&time)
~~~
{: .language-bash}

~~~
Variable: time (coordinate)
Type: double
Total Size: 88 bytes
            11 values
Number of Dimensions: 1
Dimensions and sizes:   [time | 11]
Coordinates:
Number Of Attributes: 4
  long_name :   time
  units :       days since 0001-01-01 00:00:00
  calendar :    noleap
  bounds :      time_bnds
(0)     2910
(1)     2911
(2)     2912
(3)     2913
(4)     2914
(5)     2915
(6)     2916
(7)     2917
(8)     2918
(9)     2919
(10)    2920
~~~
{: .output}

* `{…}` - coordinate subscripting

It allows to access an array using the values of its coordinates. For instance, to access T for time=2914, you can either use subscript 4 or:
~~~
print(T({2914},0,0,0))
~~~
{: .language-python}

~~~
Variable: T (subsection)
Type: float
Total Size: 4 bytes
            1 values
Number of Dimensions: 1
Dimensions and sizes:   [1]
Coordinates:
Number Of Attributes: 8
  lon :    0
  lat : -87.15909455586285
  lev : 3.64346569404006
  time :        2914
  cell_methods :        time: mean
  long_name :   Temperature
  units :       K
  mdims :       1
(0)     260.7312
~~~
{: .output}

* `$...$` - enclose strings when (im/ex)port variables

~~~
dimnames = (/"time","lev","lat","lon"/)
attnames = (/"long_name"/)

;
; access to attribute
;	
att0 = T@$attnames(0)$

;
; Example of referencing a coordinate variable 
; without knowing the dimension name
;
coord0 = T&$T!0$
~~~
{: .language-bash}

* `(/../)` - array construction (variable); remove meta data

~~~
x=(/10,20,30/)
print(x)
~~~
{: .language-bash}

* `[/../]` - list construction;

~~~
x=[/10,20,30/]
print(x)
~~~
{: .language-bash}

* `[:]` - all elements of a list

~~~
print(x[:])
~~~
{: .language-bash}

* `:` - array syntax

~~~
print(T(1:2,0,0,0))
~~~
{: .language-bash}

* `|` - separator for named dimensions

~~~
print(T(time|0,lev|0,lat|0,lon|0))
~~~
{: .language-bash}

* `\` - continue character [statement to span multiple lines]

~~~
print(T \
(1:2,0,0,0))
~~~
{: .language-bash}

### Arrays and Lists

#### Arrays
* Have fixed shape and size
* All elements are of the same type
* Scalars are 1D arrays of size 1
* Constant time to access an element

#### List:
* Can grow/shrink dynamically
* Can contain elements of differing types
* access time proportional to size of list

* Scalar variables:

~~~
a_int = 1
a_float = 2.0 ; 0.00002 , 2e-5
a_double = 3.2d ; 0.0032d , 3.2d-3
a_string = "a"
a_logical = True ; or False note capital T/F
~~~
{: .language-bash}


* array constructor characters (/…/)

~~~
– a_integer = (/1, 2, 3/) ; ispan(1,3,1)
– a_float = (/2.0, 5 , 8.0/) ; fspan(2,8,3)
– a_double = (/12 , 2d0 , 3.2 /) ; (/12,2 ,3.2 /)*1d0
– a_string = (/"abcd", "e", "Hello, World”/)
– a_logical = (/True, False, True/)
– a_2darray = (/ (/1,2,3/), (/4,5,6/), (/7,8,9/) /)
~~~
{: .language-bash}

### Variables creation and deletion

~~~
a = 2.0
pi = 4.0*atan(1.0)
s = (/ "Paris", "Oslo", "London", "Berlin" /)
r = f->precip ; (time,lat,lon)
R = random_normal(20,7, (/N,M/) ) ; R(N,M)
q = new ( (/ntim, klev, nlat, mlon/), "double" )
; free memory; Generally, do not need to do this
; delete each variable individually
delete(a)
delete(pi)
delete(s)
delete(r)
delete(R)
; delete multiple variables in one line
delete( [/ a, pi, s, r, R, q /] ) ; [/…/] list syntax 
~~~
{: .language-bash}

### Datatypes

#### numeric (classic netCDF3)

* double (64 bit)
* float (32 bit)
* long (64 bit; signed +/-)
* integer (32 bit; signed +/-)
* short (16 bit; signed +/-)
* byte ( 8 bit, signed +/-)
* complex NOT supported

#### enumeric (netCDF4; HDF5)

* int64 (64 bit; signed +/-)
* uint64 (64 bit; unsigned )
* uint (32 bit; unsigned )
* ulong (32 bit; unsigned )
* ushort (16 bit; unsigned )
* ubyte ( 8 bit, unsigned)

#### non-numeric

* string
* character
* graphic
* file
* logical
* list

### Conversion between datatypes

* NCL is a ‘strongly typed’ language
    * constraints on mixing data types
* coercion
    * implicit conversion of one type to another
* automatic coercion when no info is lost
    * let i be integer and x be float or double
    * fortran: x=i and i=x
    * NCL: x=i and i=toint(x)
* many functions to perform conversions

### Array subsetting

Standard Array Subscripting (Indexing)

* ranges: start/end and [optional] stride
* index values separated by :
* omitting start/end index implies default begin/end 

Consider T(time,lev,lat,lon)

* T -->  entire array [ don't use T(:,:,:,:) ]
* T(0,0,:,::5) --> 1st time index, 1st lev index, all lat, every 5th lon
* T(:3, 0, ::-1, :50) --> 1st 4 time indices, 1st lev, reverse, 1st 51 lon
* T(7:12,0, 45,10:20) --> 6 time indices, 1st lev,46th value of lat, 10-20 indices of lon

> ## Tips
> Good programming: Use variables not hard wired 
> ; time index tstrt:tlast, all lev, all lat :,
> ; longitude index values ln1:ln2
> T(tstrt:tlast, :, : , ln1:ln2 ) 
> 
{: .callout}

#### Arrays: Indexing & Dimension Numbers

*  row major
    * left dimension varies slowest; right dim varies fastest
    * dimension numbering left to right [0,1,..]
* subscripts
    * 0-based [ entire range for N index values: 0,N-1 ]


Consider T(:, :, :, :) --> T (0, 1, 2, 3)

* left dimension is 0 : varies slowest
* mid-left dimension is 1
* mid-right dimension is 2
* right dimension is 3 : varies fastest


Some processing functions operate on dimension numbers

Example: T(ntim, klev, nlat, mlon) --> T(0, 1, 2, 3)

* Tzon = dim_avg_n( T, 3 ) --> Tzon(ntim, lev, nlat)
* Tstd = dim_stddev_n( T, 0 ) --> Tstd (lev, nlat, mlon)


## Debugging and Error Messages

* NCL does not have a built-in debugger
* use print /printVarSummary ; examine output!
* nmsg = num( ismissing(x) ) ; count # _FillValue
* print(“x: min=“+min(x) +” max=“+max(x) )
* Error messages; Warning or Fatal
* Look at the message; often describe problem/issue
* eg: Fatal: left and right side have different sizes
* printVarSummary of variables before Fatal
* Common error messages:
http://www.ncl.ucar.edu/Document/Language/error_messages.shtml


## Help and Support

### Documentation and Examples

* http://www.ncl.ucar.edu/
   * numerous downloadable examples to get you going
* downloadable reference manuals [pdf], FAQ
   * http://www.ncl.ucar.edu/Document/Manuals/language_man.pdf
