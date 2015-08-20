<a name="logo"/>
<div align="center">
<a href="http://saig.physics.ualberta.ca/" target="_blank">
<img src="https://saig.physics.ualberta.ca/lib/tpl/dokuwiki/images/logo.png" alt="SAIG Logo" width="240" height="106"></img>
</a>
</div>

# Seismic.jl

This module provides tools to read, write, process, and plot 3D reflection 
seismic data.

## Installation
You will need these packages installed on your machine:

[PyPlot](https://github.com/stevengj/PyPlot.jl)
type `Pkg.add("PyPlot")` in Julia to install PyPlot and its dependencies.

[Docile](https://github.com/MichaelHatherly/Docile.jl)
type `Pkg.add("Docile")` in Julia to install Docile and its dependencies.

[Lexicon](https://github.com/MichaelHatherly/Lexicon.jl)
type `Pkg.add("Lexicon")` in Julia to install Lexicon and its dependencies.

[Grid](https://github.com/timholy/Grid.jl)
type `Pkg.add("Grid")` in Julia to install Grid and its dependencies.

### adding Seismic.jl to your path
Edit the file ~/.bashrc (linux) or ~/.bash_profile (Mac OS X) and add the following line
(editing /PATH/TO/ as needed):

`export SEISMIC_PATH=/PATH/TO/Seismic`

`export JULIA_LOAD_PATH=$SEISMIC_PATH/src`

`export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$SEISMIC_PATH/src/Imaging/c`

### Compiling C codes in src/Imaging/c (optional)
On the command line type `cd $SEISMIC_PATH/src/Imaging/c`, then modify the Makefile as needed for your system. Finally, type `make clean`, then `make`.

## Basic usage
Once you have installed all of the dependencies you can type `using Seismic` to start using
the functions. For example

```
using Seismic,SeismicPlotting

param = ["nt"=>500,"nx1"=>500,
	 "tau1"=>[0.4 1.0],"tau2"=>[0. 0.],"tau3"=>[0. 0.],"tau4"=>[0. 0.],
	 "v1"=>[3500. -4000],"v2"=>[99999. 99999.],"v3"=>[99999. 99999.],"v4"=>[99999. 99999.],
     "amp"=>[1. -0.5], "f0"=>[20. 20.]];
d = SeisLinearEvents(param);

plotpar = ["style"=>"overlay",
           "wiggle_trace_increment"=>10,
           "xcur"=>0.8,
           "vmin"=>-2,"vmax"=>2,
           "aspect"=>"auto",
           "xlabel"=>"X","xunits"=>"meters","ox"=>0,"dx"=>10,
           "ylabel"=>"Time","yunits"=>"seconds","oy"=>0,"dy"=>0.004,
           "wbox"=>8,"hbox"=>5,
           "cmap"=>"seismic"];

plotpar["style"]="color"; plotpar["title"]="color"; plotpar["name"]="plot1"; 
SeisPlot(d[:,:],plotpar);
plotpar["style"]="wiggles"; plotpar["title"]="wiggles"; plotpar["name"]="plot2"; 
SeisPlot(d[:,:],plotpar);
plotpar["style"]="overlay"; plotpar["title"]="overlay"; plotpar["name"]="plot3"; 
SeisPlot(d[:,:],plotpar);
```
will produce these three `.eps` files:

![plot1](http://www.ualberta.ca/~kstanton/files/plot1.png "color")

![plot2](http://www.ualberta.ca/~kstanton/files/plot2.png "wiggles")

![plot3](http://www.ualberta.ca/~kstanton/files/plot3.png "overlay")