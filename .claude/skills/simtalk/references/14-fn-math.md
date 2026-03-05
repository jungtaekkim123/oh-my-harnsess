> **Read this when:** Math functions: `abs`, `ceil`, `floor`, `sqrt`, trigonometry, random number distributions  
> **Skip this when:** Bit manipulation (see 15) or string processing (see 16)


## Contents

- [Mathematical Functions](#mathematical-functions)
  - [Basic Mathematical Functions](#basic-mathematical-functions)
  - [Functions for Numerical Values](#functions-for-numerical-values)
  - [Trigonometric Functions](#trigonometric-functions)
  - [atan2](#atan2)
  - [Distribution Functions, z_ functions](#distribution-functions-z_-functions)
  - [Cauchy [distribution], z_cauchy](#cauchy-distribution-z_cauchy)
  - [Fréchet [distribution], z_frechet](#fréchet-distribution-z_frechet)
  - [Gumbel [distribution], z_gumbel](#gumbel-distribution-z_gumbel)
  - [Laplace [distribution], z_laplace](#laplace-distribution-z_laplace)
  - [Logistic [distribution], z_logistic](#logistic-distribution-z_logistic)
  - [Loglogistic [distribution], z_loglogistic](#loglogistic-distribution-z_loglogistic)
  - [Paralogistic [distribution], z_paralogistic](#paralogistic-distribution-z_paralogistic)
  - [Pareto [distribution], z_pareto](#pareto-distribution-z_pareto)

## Mathematical Functions

### Mathematical Functions

Basic Mathematical Functions
               

Functions for Numerical Values

Trigonometric Functions
               

Distribution Functions, z_ functions
               

See also

Arithmetic Operators

---

### Basic Mathematical Functions
     
If the basis is 0, the exponent has to be greater than 0. 
If the exponent is not an integer, for example -0.5, the basis has to be greater than or equal to 0. || sqrt [SimTalk] | sqrt(x) | the square root. The parameter of data type real has to be equal to or greater than 0. |* The square root function sqrt only accepts parameters greater than or equal to 0.* The functions sqrt and pow also support the use of a physical unit. For sqrt this is limited though. If the radiant has a square unit, the result has the non-square unit. For other powers of units Plant Simulation returns a number of data type real without a unit.Note 
When using the functions exp, pow, gamma and the arithmetic operators in SimTalk, you have to make sure that the result is located within the range of numbers your computer can show. Use the gamma function to compute the factorial of a number n: n! = 1 · 2 · … · n = Γ (n+1)
Parameter

The parameter for the basic mathematical functions has the data type real or integer or it can be a value with a physical unit. 
Return Value

The return value has the data type real.
Example

```
var area := 2m * 2m; 
print area        // outputs 4m² in the Console
print sqrt(area)  // outputs 2m in the Console
```

See also

Arithmetic Operators

---

### Functions for Numerical Values
yields -2 || round [SimTalk] | round(x:real, places:integer) | the rounding of the real number x to the number of specified places |Note 
You can specify more than two parameters for the functions max and min.
For the functions max and min you cannot mix data types arbitrarily, i.e., all data types either have to be numerical, or all data types have to be of data type date and dateTime, or all have to be of data type string.
Parameters

The parameter for the functions for numerical values can have the data type real, integer, or it can be a value with a physical unit. 
The parameter can also have the data type date, dateTime, or string for the functions min and max. 
Return Value

The return value has the same data type as the parameter that you specify.
See also

Arithmetic Operators

---

### Trigonometric Functions

Trigonometric functions expect the parameter in radians or return the result in radians. You can specify parameters of data type real or integer. 
Return Value

The return value has the data type real. 
See also

atan2 [SimTalk]

---

### atan2
For any real number arguments x and y, both of which are not equal to zero, the function
atan2(y, x) returns the angle in radians between the positive x-axis of a
plane and the point given by the coordinates (x, y) on it. 
Syntax

```
atan2(y:real, x:real) → real
```

Parameters

The parameter y of data type real designates the coordinate on the y-axis.

The parameter x of data type real designates the coordinate on the x-axis.

Return Value

The return value has the data type real.
The angle is positive for counter-clockwise angles (upper half-plane, y > 0), and negative for clockwise angles (lower half-plane, y 0).
For x=0 and y=0 the function returns 0.
Back to

Trigonometric Functions

---

### Distribution Functions, z_ functions
   of data type randtime, and in SimTalk with the functions described below.| Function | Results in this distribution || z_beta([Stream:integer,]Alpha1:real,Alpha2:real) -> real | Beta [distribution], z_beta [SimTalk] || z_binominal([Stream:integer,]n:integer,p:real) -> real | Binomial [distribution], z_binomial [SimTalk] || z_cauchy([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Cauchy [distribution], z_cauchy [SimTalk] || z_cemp([Stream:integer,]Table:table) -> real | cEmp [continuous empirical distribution], z_cEmp [SimTalk] || z_demp([Stream:integer,]Table:table) -> real | dEmp [discrete empirical distribution], z_dEmp [SimTalk] || z_emp([Stream:integer,]Table:table,Column:integer) -> integer | Emp [primitive empirical distribution], z_emp [SimTalk] || z_erlang([Stream:integer,]Mu:time,Sigma:time[,LowerBound:real,UpperBound:real]) -> real | Erlang [distribution], z_erlang [SimTalk] || z_frechet([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Fréchet [distribution], z_frechet [SimTalk] || z_gamma([Stream:integer,]Alpha:real,Beta:time[,LowerBound:real,UpperBound:real]) -> real | Gamma [distribution], z_gamma [SimTalk] || z_geom([Stream:integer,]p:real[,LowerBound:real,UpperBound:real]) -> real | Geom [distribution], z_geom [SimTalk] || z_gumbel([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Gumbel [distribution], z_gumbel [SimTalk] || z_hypgeom([Stream:integer,]m:integer,n:integer,p:real) | Hypgeo [distribution], z_hypgeom [SimTalk] || z_laplace([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Laplace [distribution], z_laplace [SimTalk] || z_logistic([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Logistic [distribution], z_logistic [SimTalk] || z_loglogistic([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Loglogistic [distribution], z_loglogistic [SimTalk] || z_lognorm([Stream:integer,]Mu:time,Sigma:time[,LowerBound:real,UpperBound:real]) -> real | Lognorm [distribution], z_lognorm [SimTalk] || z_negexp([Stream:integer,]Beta:time[,LowerBound:real,UpperBound:real]) -> real | Negexp [distribution], z_negexp [SimTalk] || z_normal([Stream:integer,]Mu:time,Sigma:time[,LowerBound:real,UpperBound:real]) -> real | Normal [distribution], z_normal [SimTalk] || z_paralogistic([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Paralogistic [distribution], z_paralogistic [SimTalk] || z_pareto([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) -> real | Pareto [distribution], z_pareto [SimTalk] || z_poisson([Stream:integer,]Lambda:real) -> real | Poisson || z_triangle([Stream:integer,]c:real,a:real,b:real) -> real | Triangle [distribution], z_triangle [SimTalk] [triangular distribution] || z_uniform([Stream:integer,]LowerBound:real,UpperBound:real) -> real | Uniform [distribution], z_uniform [SimTalk] || z_weibull([Stream:integer,]Alpha:real,Beta:time) -> real | Weibull [distribution], z_weibull [SimTalk] |Parameters

The parameter Stream of data type integer designates the random number stream (compare Random Number Seed Values). 
If you call one of the distribution functions in a Method, the parameter Stream is optional. If you do not specify the stream, Plant Simulation uses the random number stream of the Method or of the user-defined attribute of data type method.
You can also call the distribution functions with the parameter Stream. For formulas this is required, as formulas never use the random number stream of the surrounding object.

All other parameters are the parameters of the corresponding distribution function as described under Probability Distributions. They all either are of data type real or integer.

Return Value

The return value has the data type real.
The distribution function z_emp returns a value of data type integer.
SimTalk

RandomSeed [SimTalk] - Method
See also

resetRandomNumberStream [SimTalk]
Parameters of the Distributions
Probability Distributions
Methods of the Distributions

---

### Cauchy [distribution], z_cauchy
The Cauchy distribution is a continuous probability
distribution.
Remarks

Use the Cauchy distribution to represent the occurrence of failures while developing
large systems.
Syntax

```
z_cauchy([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters are µ and θ both of which have to be greater than 0. The mean value and the standard deviation cannot be computed from the parameters. 
The density function is 
The distribution function is 

Return Value

The return value has the data type real.
SimTalk

Trigonometric Functions
See also

Parameters of the Distributions

---

### Fréchet [distribution], z_frechet
The Fréchet distribution is also called the Gumbel type II distribution or the inverse Weibull
distribution.
Remarks

Use the Fréchet distribution and the Gumbel distribution if you want to find
out the maximum of several random numbers. 
Syntax

```
z_frechet([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters µ and θ have to be positive. 
The density function for x > 0 is 
The distribution function is 
The following applies  and  for

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Gumbel [distribution], z_gumbel
The Gumbel distribution is also called the log-Weibull, the Gumbel type I distribution or the extreme value distribution. 
Remarks

Use the Gumbel distribution to model the distribution of the maximum (or the minimum) of
a number of samples of various distributions.
Syntax

```
z_gumbel([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters µ and θ have to be positive. 
The parameter µ determines the mean value of the distribution. The variance is  where  is the Euler-Mascheroni constant.
We set  and 
The density function is 
The distribution function is 

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Laplace [distribution], z_laplace
The Laplace distribution is a continuous distribution. The Laplace distribution is also called the Double-exponential
distribution.Syntax

```
z_laplace([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters are µ and σ > 0. The parameter µ sets the mean value of the distribution. The parameter σ > 0 sets the standard deviation of the distribution. 
The density function is  where 
For x < µ the distribution function is  and for x ≥ µ it is 

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Logistic [distribution], z_logistic
The logistic distribution is a continuous probability
distribution.
Remarks

The logistic distribution is used as lifetime distribution.
Syntax

```
z_logistic([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters are µ and σ > 0. 
The parameter µ sets the mean value of the distribution. 
The parameter σ > 0 sets the standard deviation of the distribution.
The density function is  where 
The distribution function is 

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Loglogistic [distribution], z_loglogistic
The loglogistic distribution is also called the Fisk distribution.
Remarks

The loglogistic distribution is used as income and
lifetime distribution.
Syntax

```
z_loglogistic([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters are α > 0 and β > 0. 
The density function is  for x >
0
The distribution function is 
 where 
 with β > 2

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Paralogistic [distribution], z_paralogistic
The paralogistic distribution is a transformed Pareto distribution.Syntax

```
z_paralogistic([Stream:integer, ]Mu:time,Theta:real[, LowerBound:real, UpperBound:real]) → real
```

Parameters

The parameters are α > 0 and θ > 0.
The density function is  with x > 0.
The distribution function is  with 

 for 

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---

### Pareto [distribution], z_pareto
The Pareto distribution is a power-law probability
distribution.Syntax

```
z_pareto([Stream:integer,]Mu:time,Theta:real[,LowerBound:real,UpperBound:real]) → real
```

Parameters

The parameters are α > 0 and θ > 0.
The density function is  for α > 1 and x ≥ θ
The distribution function is 

 for α > 2

Return Value

The return value has the data type real.
See also

Parameters of the Distributions

---
