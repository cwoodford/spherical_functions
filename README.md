# Spherical Functions

Python/numba package for evaluating and transforming Wigner's 𝔇
matrices, Wigner's 3-j symbols, and spin-weighted (and scalar)
spherical harmonics.  These functions are evaluated directly in terms
of quaternions, as well as in the more standard forms of spherical
coordinates and Euler angles.<sup>[1](#euler-angles-are-awful)</sup>

The conventions for this package are described in detail on
[this page](http://moble.github.io/spherical_functions/).

## Dependencies

The only true requirements for this code are `python` and `numpy`.

However, this package can automatically use
[`numba`](http://numba.pydata.org/), which uses
[LLVM](http://llvm.org/) to compile python code to machine code,
accelerating most numerical functions by factors of anywhere from 2
to 2000.  It is *possible* to run the code without `numba`, but the
most important functions are roughly 10 times slower without it.

The only drawback of `numba` is that it is nontrivial to install on
its own.  Fortunately, the best python installer,
[`anaconda`](http://continuum.io/downloads), makes it trivial.  Just
install the main `anaconda` package.

If you prefer the smaller download size of
[`miniconda`](http://conda.pydata.org/miniconda.html) (which comes
with no extras beyond python), you'll also have to run this command:

```sh
conda install pip numpy numba
```


## Installation

Installation of this package is simple:

```sh
pip install git+git://github.com/moble/spherical_functions@master
```


## Usage

First, we show a very simple example of usage with Euler angles,
though it break my heart to do
so:<sup>[1](#euler-angles-are-awful)</sup>

```python
>>> import spherical_functions as sp
```

If you need to calculate values of the 𝔇 matrix elements or the Ylm
modes for many values of (ℓ, m', m), it is more efficient to do so all
at once.

```python
>>> modes = [[ell,mp,m] for ell in range(2,9)
... for mp in range(-ell, ell+1) for m in range(-ell, ell+1)]
>>> sp.wignerD(R, modes)
```


###### <sup>1</sup> Euler angles are awful

Euler angles are pretty much
[the worst things ever](http://moble.github.io/spherical_functions/#euler-angles)
and it makes me feel bad even supporting them.  Quaternions are
faster, more accurate, basically free of singularities, more
intuitive, and generally easier to understand.  You can work entirely
without Euler angles (I certainly do).  You absolutely never need
them.  But if you're so old fashioned that you really can't give them
up, they are fully supported.
