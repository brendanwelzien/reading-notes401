# Matplotlib
- one of the most used Python packages for 2D-graphics
- easy way to visualize data through various formats
    - *IPython* is a shell that provides features that are good for matplotlib sessions
    - *pyplot* provides an interface to the OO plotting library and its functionality closely follows Matlab

### Simple Plotting
---> Say we want to draw **cosine and sine** functoins on the same plot
    ---> 1. get the data for sine and cosine functions
```python
import numpy as np
X = np.linspace(-np.pi, np.pi, 256, endpoint=True)
C, S = np.cos(X), np.sin(X)
```
- X is now a representation of a NumPy array with 256 values ranging from -π to +π (included) and C is the cosine (256 values) and S is the sine (256 values)

- Matplotlib comes with a set of defaults that can be altered
    ---> change colors and line widths
    ---> set limits *xlim()* and *ylim()*
    ---> setting ticks (*xticks()*, *yticks()*, tick container, and tick locating and formatting)
    ---> set tick labels *set_xticklabels()* / *set_yticklabels*
    ---> move spines
    ---> adding a legend *legend()*
    ---> annotate axis

### Animation
- the easiest way to make an animation is to create a *FuncAnimation* object that specifies what to update, what the update function is and the delay between frames



[<-- Back](README.md)