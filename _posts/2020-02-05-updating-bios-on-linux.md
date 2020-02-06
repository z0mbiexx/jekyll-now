---
layout: post
title: Updating BIOS on Linux Machine Without Windows 
---

So recently, someone was trying to update their BIOS on a computer where they wiped it with linux after they received it. It previously had Windows Vista and Windows 7 and being donated to the CLUG (Cochise Linux User Group) it wasn't going to be keeping Windows on it very much longer. So after many attempts of installing many different distros the issue they finally found was the kernel had to be 4.4 or earlier due to a BIOS version on the computer itself. So after this realization they had attempted to find a way to update the BIOS within linux itself.

This process is usually always done within windows as most utilities to do such tasks are all windows based.  So after a few different attempts with different options found online from different forums and resources I had the idea of using the HirensBootCD PE. It's basically a Windows 10 Portable Environment well after giving this idea to the one with the computer. They tried it and sure enough the BIOS were able to be flashed with the utilities and the latest Ubuntu was able to be installed no issues. So for anyone having issues with updating BIOS on a linux only machine..

Consider this option as a possible solution to just skipping the updates to  your BIOS.
