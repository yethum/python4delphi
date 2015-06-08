# Using P4D with Python 2.6, 3.0 #

Python 2.6 and Python 3.0 rely on Microsoft C++ dynamic link libraries which are installed
using Side by Side installation and are no longer placed in the Windows System32
directory.

This affects Delphi programs using P4D.  The problem that will occur is that you will
not be able to load c-extensions such as _socket.pyd,_ctypes.pyd and the importing of
modules such socket and ctypes will fail.

To resolve this you need to add a manifest to your Delphi application.  Here is an
example of the manifest file that PyScripter uses.

File **XP\_UAC.manifest**
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<assembly xmlns="urn:schemas-microsoft-com:asm.v1" manifestVersion="1.0">
  <assemblyIdentity
    version="1.0.0.0"
    processorArchitecture="*"
    name="PyScripter"
    type="win32"/>
  <dependency>
    <dependentAssembly>
      <assemblyIdentity
        type="win32"
        name="Microsoft.Windows.Common-Controls"
        version="6.0.0.0"
        processorArchitecture="*"
        publicKeyToken="6595b64144ccf1df"
        language="*"/>
    </dependentAssembly>
  </dependency>
  <dependency>
    <dependentAssembly>
      <assemblyIdentity
        type="win32"
        name="Microsoft.VC90.CRT"
        version="9.0.21022.8"
        processorArchitecture="x86"
        publicKeyToken="1fc8b3b9a1e18e3b"
        language="*"/>
    </dependentAssembly>
  </dependency>  
  <trustInfo xmlns="urn:schemas-microsoft-com:asm.v3">
    <security>
      <requestedPrivileges>
        <requestedExecutionLevel level="asInvoker"/>
      </requestedPrivileges>
    </security>
  </trustInfo>
  <asmv3:application>
    <asmv3:windowsSettings xmlns="http://schemas.microsoft.com/SMI/2005/WindowsSettings">
      <dpiAware>true</dpiAware>
    </asmv3:windowsSettings>
  </asmv3:application>
</assembly>
```

The key here is the dependency on Microsoft.VC90.CRT.

To use this manifest in Delphi you need to create a file say

File **XP\_UAC.rc**
```
1 24 ".\XP_UAC.manifest"
```

then compile the file ito XP\_UAC.res using brcc32.exe and link the resulting file into your application.