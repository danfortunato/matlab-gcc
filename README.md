# Using GNU GCC with MATLAB MEX

To use GNU GCC (e.g. `gcc-10`) with MATLAB MEX, first register the compiler by copying the provided XML file to the appropriate location in `MATLAB_R20XXX.app`:
```
$ cp gcc_maci64.xml /Applications/MATLAB_R2020a.app/bin/maci64/mexopts/
```
Next, start MATLAB and check the value of `$PATH` to make sure it includes the location where your version of GNU GCC is installed:
```
>> getenv('PATH')
```
If you have GNU GCC installed in a location such as `/usr/local/bin` (which is the case if you installed via Homebrew), then you may need to add this location to MATLAB's `$PATH`. This is best done by adding the following line to MATLAB's `startup.m` script:
```
setenv('PATH', ['/usr/local/bin:' getenv('PATH')])
```
If all goes well, executing `mex -setup C++` should give you the option to choose which C++ compiler to use.
