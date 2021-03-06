[![Build Status](https://travis-ci.org/iskolbin/lratio.svg?branch=master)](https://travis-ci.org/iskolbin/lratio)
[![license](https://img.shields.io/badge/license-public%20domain-blue.svg)]()

Lua ratio
=========

Lua naive implementation of ratio arithmetic. Motivation is simple, if you need
fractions during your calculation there is 99% probability of encountering
rounding errors if you decide to use plain floats. Only powers of 2 are precisely
represented by float, i.e.`0.5` is exact, `0.75` is exact, but `0.1`, for example, 
is not. TL;DR; if you need absolute precision you should probably consider using 
ratios.

Limitations
-----------
* Internally ratio stores 2 Lua numbers in table. There are no overflow checks
during calculations.
* Use `Ratio.parse` with caution, while parsing something like `1/3` **should**

This library defines `Ratio` class which instances have assigned metatable with
support for addition, subtraction, multiplication, division, negation. Comparsion
operators are also overloaded.

```lua
local R = require('Ratio')
print( R(1,3) + R.parse(1/3)) -- 2/3
print( R(1,7) - R(2,3))       -- -11/21
print( R(2,-6) * R(4,-8))     -- 1/6
print( R(1,2) / R(7))         -- 1/14
```

Ratio.new( num=0, den=1 )
-------------------------
Create new ratio. Note that numerator and denominator(if specified) have to be
integers. If you need to convert floats or strings use `Ratio.parse`.

Ratio.parse( s )
----------------
Parses `s` and returns new ratio. Argument could be either number or string.

Ratio:tonumber()
----------------
Returns standart lua number representation of ratio

Ratio:num()
-----------
Returns numerator of ratio

Ratio:den()
-----------
Return denominator of ratio

Ratio:int()
-----------
Returns integral part of ratio

Ratio:frac()
------------
Returns fractional part of ratio

Ratio:tonumber()
----------------
Return lua number as numerator divided by denominator

Ratio:tointeger()
-----------------
Return lua number rounded towards zero
