---
title: import Command
description: imports the list of installed applications.
ms.date: 07/11/2024
ms.topic: overview
ms.localizationpriority: medium
---

# import command (winget)

The **import** command of the [winget](index.md) tool imports a JSON file of apps to install. The **import** command combined with the [**export**](./export.md) command allows you to batch install applications on your PC.

The **import** command is often used to share your developer environment or build up your PC image with your favorite apps.

## Usage

`winget import [-i] <import-file> [<options>]`

![Image of import command options](./images/import-help.png)

## Arguments

The following arguments are available.

| Argument    | Description |
|-------------|-------------|
| **-i,--import-file** | JSON file describing the packages to install. |

## Options

The options allow you to customize the import experience to meet your needs.

| Option      | Description |
|-------------|-------------|
| **--ignore-unavailable**  |  Suppresses errors if the app requested is unavailable.  |
| **--ignore-versions** |  Ignores versions specified in the JSON file and installs the latest available version. |
| **--no-upgrade** | Skips upgrade if an installed version already exists. |
| **--accept-package-agreements** | Used to accept the license agreement, and avoid the prompt. |
| **--accept-source-agreements** | Used to accept the source license agreement, and avoid the prompt. |
| **-?,--help** | Shows help about the selected command. |
| **--wait** | Prompts the user to press any key before exiting. |
| **--logs,--open-logs** | Open the default logs location. |
| **--verbose, --verbose-logs** | Used to override the logging setting and create a verbose log. |
| **--nowarn,--ignore-warnings** | Suppresses warning outputs. |
| **--disable-interactivity** | Disable interactive prompts. |
| **--proxy** | Set a proxy to use for this execution. |
| **--no-proxy** | Disable the use of proxy for this execution. |

## JSON Schema

The driving force behind the **import** command is the JSON file. You can find the [schema for the JSON file](https://github.com/microsoft/winget-cli/tree/master/schemas/JSON/packages) in the [Windows Package Manager Client repo on GitHub](https://github.com/microsoft/winget-cli).

The JSON file includes the following hierarchy.

| Entry      | Description |
|-------------|-------------|
| **Sources**  |  The sources application manifests come from.  |
| **Packages**  |  The collection of packages to install.  |
| **PackageIdentifier**  |  The Windows Package Manager package identifier used to specify the package.  |
| **Version**  |  [optional] The specific version of the package to install.  |

## Importing files

When the Windows Package Manager imports the JSON file, it attempts to install the specified applications in a serial fashion. If the application is not available or the application is already installed, it will notify the user of that case.

![Image of importing files command](./images/import-command.png)

In the previous example, the **Microsoft.WindowsTerminal** was already installed. Therefore the **import** command skipped the installation.
