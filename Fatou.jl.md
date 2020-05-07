@def title = "Fatou.jl"

## What is `Fatou`

[![Build Status](https://travis-ci.org/chakravala/Fatou.jl.svg?branch=master)](https://travis-ci.org/chakravala/Fatou.jl) [![Build status](https://ci.appveyor.com/api/projects/status/mdathjmu7jg57u77?svg=true)](https://ci.appveyor.com/project/chakravala/fatou-jl) [![Coverage Status](https://coveralls.io/repos/github/chakravala/Fatou.jl/badge.svg?branch=master)](https://coveralls.io/github/chakravala/Fatou.jl?branch=master) [![codecov.io](http://codecov.io/github/chakravala/Fatou.jl/coverage.svg?branch=master)](http://codecov.io/github/chakravala/Fatou.jl?branch=master)

Julia package for Fatou sets. Install using `Pkg.add("Fatou")` in Julia. See [Explore Fatou sets & Fractals](https://github.com/chakravala/Fatou.jl/wiki/Explore-Fatou-sets-&-fractals) in Wiki for detailed *examples*. This package provides: `fatou`, `juliafill`, `mandelbrot`, `newton`, `basin`, `plot`, and `orbit`; along with various internal functionality using `Reduce` and Julia expressions to help compute `Fatou.FilledSet` efficiently. Full documentation is included. The `fatou` function can be applied to a `Fatou.Define` object to produce a `Fatou.FilledSet`, which can then be passed as an argument to the `plot` function of `PyPlot`. Creation of `Fatou.Define` objects is done via passing a function expression (in variables `z`, `c`) and optional keyword arguments to `juliafill`, `mandelbrot`, and `newton`.

`Fatou.Define` provides the following optional keyword arguments:

```Julia
Q::Expr 	= :(abs2(z)),           # escape criterion, (z, c) -> Q
C::Expr 	= :((angle(z)/(2π))*n^p)# coloring, (z, n=iter., p=exp.) -> C
∂    = π/2, # Array{Float64,1}      # Bounds, [x(a),x(b),y(a),y(b)]
n::Integer  = 176,                  # vertical grid points
N::Integer  = 35,                   # max. iterations
ϵ::Number   = 4,                    # basin ϵ-Limit criterion
iter::Bool  = false,                # toggle iteration mode
p::Number   = 0,                    # iteration color exponent
newt::Bool  = false,                # toggle Newton mode
m::Number   = 0,                    # Newton multiplicity factor
mandel::Bool= false,                # toggle Mandelbrot mode
seed::Number= 0.0+0.0im,            # Mandelbrot seed value
x0          = nothing,              # orbit starting point
orbit::Int  = 0,                    # orbit cobweb depth
depth::Int  = 1,                    # depth of function composition
cmap::String= ""                    # imshow color map
```

**Basic Usage** (filled-in Julia set)

Another feature is a plot function designed to visualize real-valued-orbits. The following is a cobweb orbit plot of a function:

```Julia
juliafill(:(z^2-0.67),∂=[-1.25,1.5],x0=1.25,orbit=17,depth=3,n=147) |> orbit
```

![img/orbit.png](/frac/orbit.png)

With `fatou` and `plot` it is simple to display a filled in Julia set:

```Julia
c = -0.06 + 0.67im
nf = juliafill(:(z^2+$c),∂=[-1.5,1.5,-1,1],N=80,n=1501,cmap="gnuplot",iter=true)
plot(fatou(nf), bare=true)
```

![img/filled-julia.png](/frac/filled-julia.png)

It is also possible to switch to `mandelbrot` mode:

```Julia
mandelbrot(:(z^2+c),n=800,N=20,∂=[-1.91,0.51,-1.21,1.21],cmap="gist_earth") |> fatou |> plot
```

![img/mandelbrot.png](/frac/mandelbrot.png)

**Generalized Newton basin fractals**

Another type are the Julia sets of the generalized Newton's method,

$$ z \mapsto z - m \frac{f(z)}{f'(z)}.) $$

Consider the polynomial map `f = :(z^3-1)` with variable `m = 1`. To get a Julia function that applies the Newton method to this formula use `η = Fatou.newton_raphson(f,m)`. Repeated function composition converges towards cube-root of 1. For example,
```Julia
julia>  ξ = Fatou.funk(η); ζ = 2.1; [ξ(ζ,0), [Fatou.recomp(η,ζ,k) for k ∈ 2:4]...]
4-element Array{Float64,1}:
 1.47559
 1.13681
 1.01581
 1.00024
```

This package comes with a plot function designed to visualize real-valued-orbits. The following is a cobweb orbit plot of the function with the Newton method applied to it using

```Julia
newton(:(z^3-1),∂=[0.4,2.5],x0=2.1,orbit=4,depth=2,n=42) |> orbit
```

![img/nf1-orbit.png](/frac/nf1-orbit.png)

The set of points that are within an `ϵ` neighborhood of the roots `ri` of the function `f` is

$$ D_0(\epsilon) = \left\{ z\in\mathbb{C}: \left|\\,z - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

`Fatou` also provides `basin` to display the the Newton / Fatou basins using set notation in LaTeX in `IJulia`.

```Julia
map(display,[basin(newton(:(z^3-1)),i) for i ∈ 1:3])
```

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{z^{3} - 1}{3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

$$ D_2(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

$$ D_3(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\left(z - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Now compute the Newton fractal Julia set for a function with annotated plot of root convergents (1):

```Julia
newton(:(z^3-1),ϵ=0.001,n=800,cmap="brg") |> fatou |> plot
```

![img/nf1-roots.png](/frac/nf1-roots.png)

Compute the Newton fractal Julia set for a function with annotated plot of iteration count:

```Julia
nf = newton(:(z^3-1),n=800,ϵ=0.1,N=25,iter=true,cmap="jet")
nf |> fatou |> plot
basin(nf,3)
```

![img/nf1-iter.png](/frac/nf1-iter.png)

$$ D_3(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\left(z - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{\left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{3} - 1}{3 \left(z - \frac{z^{3} - 1}{3 z^{2}}\right)^{2}} - \frac{z^{3} - 1}{3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Now change the multiplicity parameter m from 1 to 2 (2). # Repeated function composition produces further singularities:

```Julia
nf = newton(:(z^3-1),m=2,n=800,N=37,ϵ=0.27,iter=true,cmap="ocean",orbit=17,depth=3)
orbit(z->nf.F(z,0), [-π 2π -1],17,3,147); PyPlot.ylim(-2,7)
nf |> fatou |> plot
basin(nf,3)
```

![img/nf2-orbit.png](/frac/nf2-orbit.png)
![img/nf2-iter.png](/frac/nf2-iter.png)

$$ D_3(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{2 \left(z - \frac{2 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{3} - 2}{3 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{2}} - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{3} - 2}{3 \left(z - \frac{2 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{3} - 2}{3 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{2}} - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{2}} - \frac{2 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{3} - 2}{3 \left(z - \frac{2 z^{3} - 2}{3 z^{2}}\right)^{2}} - \frac{2 z^{3} - 2}{3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Set multiplicity parameter to `m = -0.5` for this generalized Newton fractal (3):

```Julia
nf = newton(:(z^3-1),m=-0.5,n=800,N=10,cmap="hsv",x0=0.9,orbit=17,depth=4)
nf |> fatou |> plot
orbit(nf); PyPlot.ylim(-7,2)
```

![img/nf3-limit.png](/frac/nf3-limit.png)
![img/nf3-orbit.png](/frac/nf3-orbit.png)

Change polynomial function (4):

```Julia
nf = newton(:(z^3-2z-5),n=800,p=0.3,cmap="RdGy")
orbit(z->nf.F(z,0), [-1.5π π/2 0.2],27,2,147); PyPlot.ylim(-11,3)
nf |> fatou |> plot
basin(nf,2)
```

![img/nf4-orbit.png](/frac/nf4-orbit.png)
![img/nf4-roots.png](/frac/nf4-roots.png)

$$ D_2(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{- 2 z + \left(z - \frac{z^{3} - 2 z - 5}{3 z^{2} - 2}\right)^{3} - 5 + \frac{2 z^{3} - 4 z - 10}{3 z^{2} - 2}}{3 \left(z - \frac{z^{3} - 2 z - 5}{3 z^{2} - 2}\right)^{2} - 2} - \frac{z^{3} - 2 z - 5}{3 z^{2} - 2} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (5):

```Julia
newton(:(z^2-1),m=1+1im,∂=π/2.4,n=800,N=10,cmap="hsv") |> fatou |> plot
```

![img/nf5-limit.png](/frac/nf5-limit.png)

Generalized Newton fractal example (6):

```Julia
newton(:(z^2-im),m=-0.5+2im,n=800,N=10,cmap="hsv") |> fatou |> plot
```

![img/nf6-limit.png](/frac/nf6-limit.png)

Generalized Newton fractal example (7):

```Julia
nf = newton(:(z^8-15z^4-16),m=1.5,∂=[-2π/3,0,-π/3,π/3],n=1501,N=17,cmap="gist_stern",x0=-1,orbit=17,depth=3)
nf |> orbit; PyPlot.ylim(-3,7)
nf |> fatou |> plot
basin(nf,1)
```
![img/nf7-orbit.png](/frac/nf7-orbit.png)
![img/nf7-limit.png](/frac/nf7-limit.png)

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{1.5 z^{8} - 75961.5}{8 z^{7}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (8):

```Julia
newton(:(z^8-15z^4-16),m=-0.5+2im,∂=[-2π/3,0,-π/3,π/3],n=500,N=10,cmap="hsv") |> fatou |> plot
```
![img/nf8-limit.png](/frac/nf8-limit.png)

Generalized Newton fractal example (9):

```Julia
nf=newton(:(sin(z)),m=1,∂=[-2π/3,-π/3,-π/6,π/6],n=800,N=17,iter=true,cmap="gist_earth",x0=-1.5,orbit=17,depth=3)
nf |> orbit; PyPlot.ylim(-30,30)
nf |> fatou |> plot
basin(nf,3)
```
![img/nf9-orbit.png](/frac/nf9-orbit.png)
![img/nf9-iter.png](/frac/nf9-iter.png)

$$ D_3(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} - \frac{\sin{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}}{\cos{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}} + \frac{\sin{\left (- z + \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} + \frac{\sin{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}}{\cos{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}} \right )}}{\cos{\left (- z + \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} + \frac{\sin{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}}{\cos{\left (z - \frac{\sin{\left (z \right )}}{\cos{\left (z \right )}} \right )}} \right )}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (10):

```Julia
nf = newton(:(sin(z)-1),m=1-1im,∂=[-2π/3,-π/3,-π/6,π/6],n=800,N=33,iter=true,ϵ=0.05,cmap="cubehelix")
nf |> fatou |> plot
basin(nf,2)
```

![img/nf10-iter.png](/frac/nf10-iter.png)

$$ D_2(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{1}{\cos{\left (z \right )}} \left(1 + i\right) \left(\sin{\left (z \right )} - 1\right) - \frac{\left(1 + i\right) \left(\sin{\left (z - \frac{1}{\cos{\left (z \right )}} \left(1 + i\right) \left(\sin{\left (z \right )} - 1\right) \right )} - 1\right)}{\cos{\left (z - \frac{1}{\cos{\left (z \right )}} \left(1 + i\right) \left(\sin{\left (z \right )} - 1\right) \right )}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (11):

```Julia
nf = newton(:(z^6+z^3-1),m=(1-0.4im),∂=[-0.5,0.5,-1,0],n=800,N=33,ϵ=1e-7,
        p=0.7,cmap="YlGnBu",C="(-angle(z)/(2π))*n^e")
nf |> fatou |> plot
basin(nf,1)
```

![img/nf11-limit.png](/frac/nf11-limit.png)

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\left(1.0 + 0.4 i\right) \left(z^{6} - z^{3} - 1\right)}{6 z^{5} - 3 z^{2}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (12):

```Julia
newton(:(cos(z)-1),m=-0.5+2im,n=350,N=15,ϵ=0,cmap="hsv") |> fatou |> plot
```

![img/nf12-limit.png](/frac/nf12-limit.png)

```Julia
newton(:(cos(z)-1),m=0.5-2im,n=350,N=15,ϵ=0,cmap="hsv") |> fatou |> plot
```

![img/nf12-alt.png](/frac/nf12-alt.png)


Generalized Newton fractal example (13):

```Julia
nf = newton(:(cos(z)-1),m=1,∂=π,n=500,N=35,ϵ=0,cmap="YlGnBu",x0=-2,orbit=17,depth=3)
nf |> fatou |> plot
display(basin(nf,2))
orbit(nf); PyPlot.ylim(-5,1)
```

![img/nf13-roots.png](/frac/nf13-roots.png)

$$ D_2(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z + \frac{\cos{\left (z \right )} - 1}{\sin{\left (z \right )}} + \frac{\cos{\left (z + \frac{\cos{\left (z \right )} - 1}{\sin{\left (z \right )}} \right )} - 1}{\sin{\left (z + \frac{\cos{\left (z \right )} - 1}{\sin{\left (z \right )}} \right )}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

![img/nf13-orbit.png](/frac/nf13-orbit.png)

Generalized Newton fractal example (14):

```Julia
nf = newton(:(z^5-3im*z^3-(5+2im)z^2+3z+1),m=1-0.24im,∂=2.0,n=800,ϵ=0.01,iter=true,N=27,cmap="brg") 
nf |> fatou |> plot
basin(nf,1)
```

![img/nf14-iter.png](/frac/nf14-iter.png)

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \frac{\left(1.0 - 0.24 i\right) \left(z^{5} - 3 i z^{3} - z^{2} \left(5 + 2 i\right) + 3 z + 1\right)}{5 z^{4} - 9 i z^{2} - 2 z \left(5 + 2 i\right) + 3} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (15):

```Julia
nf = newton(:(log(z)),m=1+1im,∂=2π,n=500,N=27,cmap="brg")
nf |> fatou |> plot
basin(nf,2)
```

![img/nf15-limit.png](/frac/nf15-limit.png)

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,- z \left(1 - i\right) \log{\left (z \right )} + z - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (16):

```Julia
nf = newton(:(z^(4.0+3.0im)-1),m=2.1,∂=π,n=500,N=27,cmap="terrain")
nf |> fatou |> plot
basin(nf,1)
```
![img/nf16-limit.png](/frac/nf16-limit.png)

$$ D_1(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,- \frac{z z^{-4 - 3 i}}{4 + 3 i} \left(2.1 z^{4 + 3 i} - 2.1\right) + z - r_i\\,\right|<\epsilon,\\,\forall r_i(\\,f(r_i)=0 )\right\}) $$

Generalized Newton fractal example (17):

```Julia
nf = newton(:(e^z+1),m=1,∂=2π,n=800,iter=true,N=27,cmap="brg",x0=5,orbit=11,depth=3)
orbit(nf); PyPlot.ylim(-10,7)
nf |> fatou |> plot
basin(nf,2)
```

$$ D_2(\epsilon) = \left\{z\in\mathbb{C}:\left|\\,z - \left(e^{z} + 1\right) e^{- z} - \left(e^{z - \left(e^{z} + 1\right) e^{- z}} + 1\right) e^{- z + \left(e^{z} + 1\right) e^{- z}} - r_i\\,\right|<\epsilon,\\,\forall r_i(\\\,f(r_i)=0 )\right\}) $$

![img/nf17-iter.png](/frac/nf17-iter.png)
![img/nf17-orbit.png](/frac/nf17-orbit.png)
