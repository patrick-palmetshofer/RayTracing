# RayTracing
This code aims to provide a simple ray tracing module for calculating various properties of optical paths (object, image, aperture stops, field stops).  It makes use of ABCD matrices and does not consider aberrations (spherical or chromatic). It is not a package to do "Rendering in 3D with raytracing".  

The code has been developed first for teaching purposes and is used in my "[Optique](https://itunes.apple.com/ca/book/optique/id949326768?mt=11)" Study Notes (french only), but also for actual use in my research. I have made no attempts at making high performance code.  Readability and simplicity of usage is the key here. It is a single file with only `matplotlib` as a dependent module.

The module defines `Ray` ,  `Matrix` and `OpticalPath` as the main elements.  An optical path is a sequence of matrices into which rays will propagate. Specific subclasses of `Matrix` exists: `Space`, `Lens` and `Aperture`. Finally, a ray fan is a collection of rays, originating from a given point with a range of angles.

## Getting started
You need `matplotlib`, which is a fairly standard Python module. If you do not have it,  installing [Anaconda](https://www.anaconda.com/download/) is your best option. You should choose Python 3.7 or later.

You create an OpticalPath, which you then populate with optical elements such as Space, Lens or Aperture. You can then adjust the optical path properties (object height for instance) and display in matplotlib.

This will show you a few examples of things you can do:

```shell
python ABCD.py
cd teaching
python demo.py
```

In order to be able to *import* the `ABCD` module, you must have one of the following:

1. The module `ABCD.py` in the same directory as your file
2. The path to `ABCD.py` added to `sys.path` manually or through the command-line with PYTHONPATH
3. The module ABCD installed in the standard location. ABCD.py has a special option `python ABCD.py install` will copy it to your standard directory. Soon, when it is more stable, it will be submitted to PyPi.

In your code, (such as the `test.py` or `demo.py`  files), you would do this:

```python
from ABCD import *

path = OpticalPath()
path.append(Space(d=10))
path.append(Lens(f=5, diameter=2.5))
path.append(Space(d=12))
path.append(Lens(f=7))
path.append(Space(d=10))
path.display()
```

You may obtain help by typing (interactively): `help(Matrix)`, `help(Ray)`,`help(OpticalPath)`

```python
python
>>> help(Matrix)
Help on class Matrix in module ABCD:

class Matrix(builtins.object)
 |  A matrix and an optical element that can transform a ray or another matrix.
 |  
 |  The general properties (A,B,C,D) are defined here. The operator "*" is 
 |  overloaded to allow simple statements such as:
 |  
 |  M2 = M1 * ray  
 |  or 
 |  M3 = M2 * M1
 |  
 |  In addition apertures are considered and the physical length is 
 |  included to allow simple management of the ray tracing.
 |  
 |  Methods defined here:
 |  
 |  __init__(self, A, B, C, D, physicalLength=0, apertureDiameter=inf, label='')
 |      Initialize self.  See help(type(self)) for accurate signature.
 |  
 |  __mul__(self, rightSide)
 |      Operator overloading allowing easy to read matrix multiplication 
 |      
 |      For instance, with M1 = Matrix() and M2= Matrix(), one can write M3 = M1*M2.
 |      With r = Ray(), one can apply the M1 transform to a ray with r = M1*r
 |  
 |  __str__(self)
 |      String description that allows the use of print(Matrix())
 |  
 |  displayHalfHeight(self)
 |      A reasonable height for display purposes for an element, whether it is infinite or 
```

## Examples

You can run the code directly from the [examples](./examples) directory.  The modules modify the path to be able to import `ABCD.py`.

You can run `demo.py` to see a variety of systems, `illuminator.py` to see a Kohler illuminator, and `invariant.py` to see an example of the role of lens diameters to determine the field of view.

![Figure1](assets/Figure1.png)
![Microscope](assets/Microscope.png)
![Illumination](assets/Illumination.png)

## Licence

This code is provided under the [MIT License](./LICENSE).