# Using GCC with MATLAB MEX on a Mac

## Installation
To use the GNU Compiler Collection's `gcc`, `g++`, or `gfortran` with MATLAB MEX, first register the compilers by copying the provided GCC XML files to the appropriate location in `MATLAB_R20XXX.app`:
```
$ cp g*_maci64.xml /Applications/MATLAB_R2020b.app/bin/maci64/mexopts/
```
***Note**: The provided XML files are for `gcc-10` and `g++-10`. If you would like to use a different version of GCC you must modifying these files accordingly.*

Next, start MATLAB and check the value of `$PATH` to make sure it includes the location of your version of GCC:
```
>> getenv('PATH')
```
If you have GCC installed in a location such as `/usr/local/bin` (which is the case if you installed via Homebrew), then you may need to add this location to MATLAB's `$PATH`. This is best done by adding the following line to MATLAB's `startup.m` script:
```
setenv('PATH', ['/usr/local/bin:' getenv('PATH')])
```

## Setting the default compiler
The compiler files shipped with MATLAB may take priority over GCC by default. To fix this, either copy the provided Clang XML files to the appropriate location in `MATLAB_R20XXX.app`:
```
$ cp clang*_maci64.xml /Applications/MATLAB_R2020b.app/bin/maci64/mexopts/
```
or edit the Clang XML files in `/Applications/MATLAB_R2020b.app/bin/maci64/mexopts/` to have `Priority="B"`.

## Selecting GCC
If all goes well, executing `mex -setup C` should select GCC (and give you the option to choose a different C compiler):
```
>> mex -setup C
MEX configured to use 'gcc-10' for C language compilation.

To choose a different C compiler, select one from the following:
Xcode with Clang  mex -setup:/Applications/MATLAB_R2020b.app/bin/maci64/mexopts/clang_maci64.xml C
gcc-10  mex -setup:/Applications/MATLAB_R2020b.app/bin/maci64/mexopts/gcc_maci64.xml C
```
Similarly, for C++:
```
>> mex -setup C++
MEX configured to use 'g++-10' for C++ language compilation.

To choose a different C++ compiler, select one from the following:
g++-10  mex -setup:/Applications/MATLAB_R2020b.app/bin/maci64/mexopts/g++_maci64.xml C++
Xcode Clang++  mex -setup:/Applications/MATLAB_R2020b.app/bin/maci64/mexopts/clang++_maci64.xml C++
```
Finally, for FORTRAN:
```
>> mex -setup Fortran
MEX configured to use 'gfortran' for FORTRAN language compilation.
```
(Note that if you have `ifort` installed, you may see an option here to select it.)
