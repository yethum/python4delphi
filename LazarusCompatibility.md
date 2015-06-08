# FPC-Lazarus compatibility #

The main parts of Python4Delphi are:

  1. PythonEngine.pas
> A collection of relatively low-level routines for communicating with Python, creating
> Python types in Delphi etc.
  1. VarPyth.pas
> Very high-level and convenient use of Python objects in Delphi using custom variants.
  1. WrapDelphi classes
> Units that allow easy manipulation of standard GUI Delphi objects in Python scripts.

All parts of Python4Delphi now work in FPC-Lazarus Win32.  A serious limitation when using Varpyth is that due to an FPC issue with variants (http://mantis.freepascal.org/view.php?id=20849) you will find that there are problems in converting Python Variants to native types and standard variants.

The WrapDelphi units have also been ported and Demo31 for Lazarus is included in SVN and works fine.  The only limitation is that the directive {$METHODINFO} does not exist in FPC, i.e. RTTI information is not produced for methods, and you cannot easily wrap Delphi methods.  Of course it can be done with a bit of work as you can see in the Wrapxxxx units.

MacOSX and Linux compatibility has not been tested. Please test and if required submit a patch.

64-bit is supported.