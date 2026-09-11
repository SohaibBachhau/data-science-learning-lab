# Complex Numbers, Polynomials and Roots

Status: `developing`

This note contains the mathematical foundation needed for topics such as time-series stationarity and invertibility. The ideas are general mathematics, so they live here rather than inside the time-series branch.

## Imaginary numbers

The imaginary unit is defined by

$$
i^2=-1.
$$

Therefore

$$
i=\sqrt{-1}.
$$

Examples:

$$
\sqrt{-4}=2i,
$$

$$
\sqrt{-9}=3i.
$$

A complex number has the form

$$
z=a+bi,
$$

where `a` is the real part and `b` is the coefficient of the imaginary part.

Examples:

$$
3+2i,
$$

$$
-1+4i,
$$

$$
5=5+0i,
$$

$$
2i=0+2i.
$$

## Complex plane and modulus

A complex number can be viewed as a point on a two-dimensional plane:

- the horizontal coordinate is the real part `a`;
- the vertical coordinate is the imaginary coefficient `b`.

For

$$
z=a+bi,
$$

the distance from zero is called the modulus or absolute value:

$$
|z|=\sqrt{a^2+b^2}.
$$

This is just the Pythagorean theorem.

Example:

$$
z=3+4i
$$

has

$$
|z|=\sqrt{3^2+4^2}=5.
$$

For a purely imaginary number,

$$
|bi|=|b|.
$$

For a real number, use the ordinary absolute value.

## Unit circle

The unit circle consists of all points whose distance from zero is exactly 1.

So for any root `z`:

$$
|z|<1
$$

means the root lies inside the unit circle,

$$
|z|=1
$$

means it lies on the unit circle, and

$$
|z|>1
$$

means it lies outside the unit circle.

Examples:

- `z = 0.5` is inside because `|z| = 0.5`.
- `z = -3` is outside because `|z| = 3`.
- `z = i` is on the unit circle because `|i| = 1`.
- `z = 1 + i` is outside because `|z| = sqrt(2) > 1`.

## Polynomials

A polynomial is a sum of terms containing a variable raised to non-negative whole-number powers.

A general polynomial can be written as

$$
p(z)=a_0+a_1z+a_2z^2+\cdots+a_nz^n.
$$

The coefficients are the numbers `a_0, a_1, ..., a_n`.

The degree of the polynomial is the highest power with a non-zero coefficient.

Example:

$$
p(z)=2z^4+5z^2-3
$$

can be written as

$$
p(z)=2z^4+0z^3+5z^2+0z-3.
$$

Its degree is 4 and its coefficients are

$$
2,\ 0,\ 5,\ 0,\ -3.
$$

## Roots of a polynomial

A root is a value of `z` that makes the polynomial equal to zero.

Example:

$$
p(z)=z^2-5z+6.
$$

Factorizing gives

$$
(z-3)(z-2)=0.
$$

Therefore the roots are

$$
z=3,\qquad z=2.
$$

Each root is checked separately.

For example, if the roots are `3` and `-2`, then

$$
|3|=3,
$$

$$
|-2|=2.
$$

Both are outside the unit circle.

## Complex roots

Some polynomials have roots that are not real numbers.

Example:

$$
z^2+1=0.
$$

Then

$$
z^2=-1,
$$

so

$$
z=\pm i.
$$

Both roots lie on the unit circle because

$$
|i|=|-i|=1.
$$

Another example:

$$
z^2-2z+2=0.
$$

Using the quadratic formula gives

$$
z=1\pm i.
$$

Each root has modulus

$$
\sqrt{1^2+1^2}=\sqrt{2}>1,
$$

so both roots lie outside the unit circle.

## Higher-degree polynomials

For degree 2, the quadratic formula can be used.

Some higher-degree polynomials factorize easily by hand. When they do not, software is normally used to calculate the roots numerically.

The important workflow is therefore

```text
polynomial
→ set equal to zero
→ find all roots
→ check each root separately
→ calculate |z|
→ compare |z| with 1
```

This workflow is especially useful in time-series econometrics, where roots are used to study stationarity and invertibility.

## What to remember

- `i^2 = -1`.
- A complex number has the form `a + bi`.
- `|a + bi| = sqrt(a^2 + b^2)`.
- A polynomial is a sum of non-negative whole-number powers of a variable.
- A root makes a polynomial equal to zero.
- Different roots are checked separately.
- Compare the modulus of each root with 1 to determine whether it lies inside, on, or outside the unit circle.

## Course connection

These ideas are used in `knowledge/econometrics/time-series/` when studying the characteristic roots of AR and MA lag polynomials.
