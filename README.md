
## stospice

Python library to convert s-sparameters into a spice subcircuit.

### Library

The library is named stospice and consists of one function called stospice.
The signature of the function is as follows:

```
stospice(
    filename,  # the name of the file to save the subcircuit to
    name,      # the name of the subcircuit inside
    f,         # list of s-parameter frequencies
    s,         # the NxN s-parameter matrix as an array
    z0         # line impedance of each port either as an array or single value
)
```

### As a Standalone Tool

You can run the library also as a standalone script.  The tool takes
a s-parameter touchstone file as input and generates a 'inc' 
subcircuit file from it.  The tool's command line usage is as follows:

```
usage: stospice.py [-h] filename

positional arguments:
  filename    s-parameter file to validate against

optional arguments:
  -h, --help  show this help message and exit
```

Usage of the tool requires the installation of the scikit-rf python library.

### Testing

You can also test the library using the test\_stospice.py script.
It takes a touchstone file as its argument and will then validate against
it using ngspice.  If no touchstone file is passed to the script, it just generates a random N-port s-parameter
matrix that it then validates itself against.  The test can also be run via unittest: "python -m unittest".
The test script's command line usage is as follows:

```
usage: test_stospice.py [-h] [--ports PORTS] [filename]

positional arguments:
  filename       s-parameter file to validate against

optional arguments:
  -h, --help     show this help message and exit
  --ports PORTS  number of ports to simulate against
```

### Notes

This tool is based off the following work:

1. The code s2spice.cpp from [Qucs-S](https://github.com/ra3xdh/qucs_s/blob/current/qucs/extsimkernels/s2spice.cpp).
2. The article, "Create S-Parameter Subcircuits for Microwave and RF Applications" by John S. Gerig, Wideband Associates.   This article also included QBASIC code for generating the subcircuit.

The original article by Gerig uses the "E" voltage controlled voltage source, using
an undocumented tabular argument.  The code from transmitterdan's [s2spice](https://github.com/transmitterdan/s2spice) uses a "G" device.
While the code from qucs\_s, uses instead the
"A" predefined device and its tabular argument.  This library uses the latter "A" device.

The library also supports S-matrices with one or more ports (up to 98) using the logic from s2spice.cpp.
The original article only supported 2, while s2spice.cpp only supports up to 8 ports.  I increased the number
of ports supported in case one wanted to perform port tuning which requires a lot of ports.

