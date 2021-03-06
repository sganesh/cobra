Cobra - Windows version of Linux Desktop Testing Project - http://ldtp.freedesktop.org

Verified with Windows XP SP3 / Windows 7 SP1

Minimum requirement .NET3.5

On Windows XP SP3 make sure you have installed:
.NET3.0 and .NET3.5 and KB971513
http://www.microsoft.com/download/en/details.aspx?displaylang=en&id=13821 (KB971513)

.NET restributable package download info - http://www.pagestart.com/netframeworkdwnldlinks.html

On Windows 7: Default .NET with the system should work fine

Tested with Python 2.5 / 2.6 / 2.7

Compile SetEnvironmentVariable and WinLdtpdService solutions, place the binary where you have all the dll's, README.txt, lgpl.rtf, before running Wix installer commands

LDTP packages are created with WiX installer - http://wix.tramontana.co.hu

To create WinLDTP package (Credit: David Connet <dconnet@vmware.com>):
If planing to build package, copy WinLdtpdService.exe to the folder where rest of DLL's exist
"c:\Program Files (x86)\Windows Installer XML v3.5\bin\candle.exe" -pedantic CobraWinLDTP.wxs
"c:\Program Files (x86)\Windows Installer XML v3.5\bin\light.exe" -pedantic -spdb -sadv -dcl:high -ext WixUIExtension -ext WixUtilExtension -dWixUILicenseRtf=License.rtf -out CobraWinLDTP.msi CobraWinLDTP.wixobj

By default LDTP listens in localhost, to listen in all ports, set environment variable
 LDTP_LISTEN_ALL_INTERFACE and then run WinLdtpdService.exe as an user with
 administrator privillage in Windows 7, else you will get exception Access Denied.
 Other option is: Disable ACL in Control Panel->User Accounts->Change User Account Control settings
Other option (Still you need to set LDTP_LISTEN_ALL_INTERFACE), you need to run as administrator:
netsh http add urlacl url=http://localhost:4118/ user=User
netsh http add urlacl url=http://+:4118/ user=User
netsh http add urlacl url=http://*:4118/ user=User

WinLDTP source files are distributed under LGPLv2.1 license
Following files are re-distributed as-is
Microsoft DLL's (Interop.UIAutomationClient.dll, UIAComWrapper.dll, WUIATestLibrary.dll) - http://uiautomationverify.codeplex.com/ - MS-PL license
XML RPC .NET library (CookComputing.XmlRpcV2.dll) - http://www.xml-rpc.net/ - MIT X11 license

WinLDTP works based on Microsoft accessibility layer.
 To check whether your application is accessibility enabled,
 download the binary from http://uiautomationverify.codeplex.com/ and verify the same.

Verified with Windows 8 developer edition

Minimum requirement .NET4.0
To compile for Windows 8 environment (You can compile it from Windows 7, Visual studio 2010), but make sure you change target framework as .NET 4.0 for Windows 8 and .NET 3.5 for Windows XP/7
NOTE: Don't select client profile

netsh http add urlacl url=http://localhost:4118/ user=User
netsh http add urlacl url=http://+:4118/ user=User

If you run WinLDTP where you have logged in as a domain user
netsh http add urlacl url=http://localhost:4118/ user=DOMAIN\User
netsh http add urlacl url=http://+:4118/ user=DOMAIN\User
