---
title: PowerToys Command Not Found for Windows
description: A PowerShell 7 module that detects an error thrown by a command and suggests a relevant WinGet package to install, if available.
ms.date: 11/19/2024
ms.topic: concept-article
no-loc: [PowerToys, Windows, Command Not Found, Win]
# Customer intent: As a Windows power user, I want to learn about the Command Not Found utility in PowerToys for Windows.
---

# Command Not Found utility

A PowerShell 7 module that detects command-line errors and suggests a relevant WinGet package to install, if available.

> [!IMPORTANT]
> There are some incompatibilities between Command Not Found and some PowerShell configurations. Read more about them in [issue 30818](https://github.com/microsoft/PowerToys/issues/30818) on GitHub.

![Command Not Found screenshot](../images/pt-cmd-not-found.png)

## Requirements

- [PowerShell 7](/PowerShell/scripting/install/installing-PowerShell-on-windows)
- [PowerShell Microsoft.WinGet.Client module](https://www.powershellgallery.com/packages/Microsoft.WinGet.Client)

## Install the module

To install the Command Not Found module, go to the Command Not Found page in PowerToys settings and select **Install**. Once the installation has completed, the following PowerShell 7 experimental features needed for the module to function will be enabled:

- PSFeedbackProvider
- PSCommandNotFoundSuggestion

After that, the PowerShell profile file will be appended with following block of PowerShell commands:

```psh
#34de4b3d-13a8-4540-b76d-b9e8d3851756 PowerToys CommandNotFound module
Import-Module "<powertoys install dir>/WinGetCommandNotFound.psd1"
#34de4b3d-13a8-4540-b76d-b9e8d3851756
```

> [!NOTE]
> The profile file will be created if needed. Restart PowerShell session to use the module.

## Uninstall the module

To uninstall the Command Not Found module, go to the Command Not Found page in PowerToys settings and select **Uninstall**. Once the uninstallation has completed, the block of commands previously added will be removed from the PowerShell profile file.

[!INCLUDE [install-powertoys.md](../includes/install-powertoys.md)]
