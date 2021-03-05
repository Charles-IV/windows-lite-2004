# windows-lite-2004
 AME scripts

## About this fork
This fork is designed to preserve Windows Defender and Windows Update. [MickSt's fork](https://github.com/MickSt/windows-lite-2004) was used as a starting point. Preserving windows defender causes issues with the AME process however. Windows defender will detect all the scripts and the hardentools exe as malware. It will also deted the hosts file as being malicioiusly changed.

I also removed most of the post install script - it no longer installs chocolatey and loads of programs with it. instead it only installs hardentools.

I ran this on the standard Windows 10 20H2 iso from Microsoft. As these scripts were originally designed for 2004, it's possibe that more microsoft tracking bits and bobs are present that havent been removed. The only extra things i removed was the snap and sketch app, and the chromium based edge.

## How to use
This is a fork of Chris Titus Tech's fork of the AME script. You should follow his [video](https://youtu.be/TlMqdSiGcOg) and [writeup](https://christitus.com/windows-10-optimization-guide/). However, make sure you understand the difference between this script and his, so you are prepared for any consequences of these differences.

## Warnings
* Due to windows defender being preserved, you will need to tell defender to ignore the install scripts and hardentools exe (and probably need to tell defender restore them when windows defender ignores you). You will also need to add an exclusion for the hosts file (C:\Windows\System32\drivers\etc\hosts).
* This script removes the new chromium edge (and the old edge). Make sure you have another browser installed (like Firefox) before running this script. 

**TODO:** Test Windows Update. The windows update page in settings now works, but i havent tested an actual update. There are also some left over hosts file entries that may block it, but i dont think they do.

## Updates
Do SSU (Service Stack) Update first and reboot
https://www.catalog.update.microsoft.com/Search.aspx?q=Servicing%20Stack%20Update%20Windows%2010

Then do comulative update last and reboot
https://www.catalog.update.microsoft.com/Search.aspx?q=Cumulative%20Update%20Windows%2010

Make sure you download the Same MONTH and Architecture (x64)

Steps to Extract and Install
```
C:\> expand -F:* <.msu file> <dest>
dism /online /add-package /packagepath=C:\Windows10.0-EXTRACTED-x64.cab
```

Reboot between each one then run
```
dism /online /Cleanup-Image /StartComponentCleanup
```
