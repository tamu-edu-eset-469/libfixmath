# libfixmath
Fixed point arithmetic library from Wikipedia article https://en.wikipedia.org/wiki/Libfixmath. The library support Q15.16 fixed point number only.

## Credits
### Developer: Ben Brewer
### Stable release: r64 / February 2, 2012
### License: MIT
### Website: https://code.google.com/p/libfixmath
### Repository: https://code.google.com/p/libfixmath/source/default/source

## Authors description
Cross Platform Fixed Point Maths Library

This is a tried and tested cross platform fixed point maths library.

This library implements the math.h functions in fixed point (Q15.16) format, a subset of the currently supported functions are: * sin, cos, tan * asin, acos, atan, atan2 * sqrt, exp * mul, div * sadd, ssub, smul, sdiv (saturated arithmetic)

## Function Reference

### Conversion Functions

Conversion from integers and floating point values. These conversions retain the numeric value and perform rounding where necessary.
* fix16_from_int(a) Simply multiplies a by fix16_one = 65536
* fix16_to_int(a) Divides by fix16_one and rounds to nearest integer.
* fix16_from_float(a) Multiplies by fix16_one and rounds to nearest value.
* fix16_to_float(a) Divides by fix16_one. Rounding is according to the current floating point mode.
* fix16_from_dbl(a) Multiplies by fix16_one and rounds to nearest value.
* fix16_to_dbl(a) Divides by fix16_one. All fix16_t values fit into a double, so no rounding happens.
* fix16_from_str(buf) Converts from string to fix16_t.
* fix16_to_str(value, buf, decimals) Converts from fix16_t to string.

### Basic arithmetic
These functions perform rounding and detect overflows, unless disabled with CompilationOptions. When overflow is detected, they return fix16_overflow as a marker value.

* fix16_add(a,b) Addition
    * Implementation 1: just C's + operator
    * Implementation 2: with overflow detection
* fix16_sub(a,b) Subtraction.
    * Implementation 1: just C's - operator
    * Implementation 2: with overflow detection
* fix16_mul(a,b) Multiplication .
    * Implementation 1: using int32_t * int32_t -> int64_t
    * Implementation 2: using (u)int16_t * (u)int16_t -> (u)int32_t
    * Implementation 3: using uint8_t * uint8_t -> int16_t
* fix16_div(a,b) Division.
    * Implementation 1: using uint32_t / uint32_t
    * Implementation 2: performing division manually with uint32_t
### Saturating aritmetic
Functions for basic arithmetic that saturate instead of overflowing. They are based around the functions listed above, but add extra logic to convert fix16_overflow to either fix16_min or fix16_max.

* fix16_sadd(a,b) Saturating addition
* fix16_ssub(a,b) Saturating subtraction
* fix16_smul(a,b) Saturating multiplication
* fix16_sdiv(a,b) Saturating division

### Transcendental functions
Roots, exponents & similar.

* fix16_sqrt(a) Square root. Performs rounding and is accurate to Fix16Limits.
* fix16_exp(a) Exponential function using power series approximation. Accuracy depends on range, worst case +-40 absolute for negative inputs and +-0.003% for positive inputs. Average error is +-1 for neg and +-0.0003% for pos.
* fix16_log(a) Natural logarithm using Newton approximation and fix16_exp(). Worst case error +-3 absolute, average error less than 1 unit.

### Trigonametric functions
Functions for sin, tan etc.

* fix16_sin(a) Sine for angle in radians
* fix16_sin_parabola(a) Alternative sine implementation.
* fix16_cos(a) Cosine for angle in radians
* fix16_tan(a) Tangent for angle in radians
* fix16_asin(a) Inverse of sine, output in radians
* fix16_acos(a) Inverse of cosine, output in radians
* fix16_atan(a) Inverse of tangent, output in radians
* fix16_atan2(a,b) Inverse of tangent with automatic sign handling. Output in radians.
