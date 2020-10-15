
# JGF(Z) format implementation
This package implements export and import functions for the JSON Graph Format (gZipped) `JGF(Z)` (https://jsongraphformat.info). Supported input formats/libraries are `networkx`, `igraph`, `numpy` matrices and `JXNF` files. All network, node and edges attributes are saved as well.

This project is being developed to support the new network datatype for (brainlife.io).


### Authors
- [Filipi N. Silva](https://filipinascimento.github.io)

### Contributors
- [Franco Pestilli](https://liberalarts.utexas.edu/psychology/faculty/fp4834)


### Funding
We kindly ask that you acknowledge the funding below in your publications and code reusing this code.

[![NIH-NIBIB-R01EB029272](https://img.shields.io/badge/NIH_NIBIB-R01EB029272-green.svg)](https://grantome.com/grant/NIH/R01-EB029272-01)

## Installation 

You can install this package using `pip`:

```bash
pip install jgf
```

or install it from this git repository:

```bash
git clone <repository URL>
cd <repository PATH>
pip install -e ./
```

## API Reference

API reference can be found in (https://jgf.readthedocs.io/).

## Example of use

To use the library in igraph environment simply import the correct module and run `save` or `load` functions:

```python
import igraph as ig
import jgf.igraph as jig

g = ig.Graph.Famous("Zachary")

# will save a compressed file
jig.save(g,"zachary.jgfz")

g, = jig.load("zachary.jgfz")
```

You can also use it to save and load connectivity matrices as square numpy matrices:

```python
import numpy as np
import jgf.conmat as jcm

A = np.array([
  [  0, 0.1, 0.2,   0,   0],
  [  0,   0,   0, 0.5,   0],
  [  0,   0,   0,   0, 1.0],
  [1.0, 1.0,   0,   0,   0],
  [  0,   0, 0.5,   0,   0],
  ])

nodeProperties = {
  "name" : [
    "Node 1",
    "Node 2",
    "Node 3",
    "Node 4",
    "Node 5",
  ]
}
# will save a compressed file
jcm.save(A,"example.jgfz",label= "Example", nodeProperties=nodeProperties)

B,properties = jcm.load("example.jgfz",getExtraData=True)
```

