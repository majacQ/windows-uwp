---
title: upgrade Command
description: upgrades the specified application.
ms.date: 05/05/2021
ms.topic: overview
ms.localizationpriority: medium
---

# upgrade command (winget)

The **upgrade** command of the [winget](index.md) tool upgrades the specified application. Optionally, you may use the [**list**](.\list.md) command to identify the application you want to upgrade.  

The **upgrade** command requires that you specify the exact string to upgrade. If there is any ambiguity, you will be prompted to further filter the **upgrade** command to  an exact application.

## Usage

`winget upgrade [[-q] \<query>] [\<options>]`

![Image of upgrade command arguments](images\upgrade.png)

## Arguments

The following arguments are available.

| Argument      | Description |
|-------------|-------------|  
| **-q,--query**  |  The query used to search for an app. |
| **-?, --help** |  Get additional help on this command. |

> [!NOTE]
> The query argument is positional. Wild-card style syntax is not supported. This is most often the string of characters you expect to help find the package you are upgrading.

## Options

The options allow you to customize the upgrade experience to meet your needs.

| Option      | Description |
|-------------|-------------|  
| **-m, --manifest** |   Must be followed by the path to the manifest (YAML) file. You can use the manifest to run the upgrade experience from a [local YAML file](install.md#local-install). |
| **--id**    |  Limits the upgrade to the ID of the application.   |  
| **--name**   |  Limits the search to the name of the application. |  
| **--moniker**   | Limits the search to the moniker listed for the application. |  
| **-v, --version**  |  Enables you to specify an exact version to upgrade. If not specified, latest will upgrade the highest versioned application. |  
| **-s, --source**   |  Restricts the search to the source name provided. Must be followed by the source name. |  
| **-e, --exact**   |   Uses the exact string in the query, including checking for case-sensitivity. It will not use the default behavior of a substring. |  
| **-i, --interactive** |  Runs the installer in interactive mode. The default experience shows installer progress. |  
| **-h, --silent** |  Runs the installer in silent mode. This suppresses all UI. The default experience shows installer progress. |
| **--purge** | Deletes all files and directories in the package directory (portable) |
| **-o, --log**  |  Directs the logging to a log file. You must provide a path to a file that you have the write rights to. |
| **--override** | A string that will be passed directly to the installer.    |
| **-l, --location** |    Location to upgrade to (if supported). |
| **--force** | When a hash mismatch is discovered will ignore the error and attempt to install the package.    |
| **--accept-package-agreements** | Used to accept the license agreement, and avoid the prompt. |
| **--accept-source-agreements** | Used to accept the source license agreement, and avoid the prompt. |
| **--header** | Optional Windows-Package-Manager REST source HTTP header. |
| **--all** | Updates all available packages to the latest application. |
| **--include-unknown** | Upgrade packages even if their current version cannot be determined. |
| **--verbose-logs** | Used to override the logging setting and create a verbose log. |
### Example queries

The following example upgrades a specific version of an application.

```CMD
winget upgrade powertoys --version 0.15.2
```

The following example upgrades an application from its ID.

```CMD
winget upgrade --id Microsoft.PowerToys
```

The following example shows upgrading all apps

```CMD
winget upgrade --all
```

## Using **upgrade**

To identify which apps are in need of an update, simply use **upgrade** without any arguments to show all available upgrades. 

In the example below, you will see **winget upgrade** shows the user which apps have an available update. From the available updates, the user identifies that an update is available for *JanDeDobbeleer.OhMyPosh* and uses **upgrade** to update the application.

![Animation demonstrating upgrade command](./images/upgrade.gif)

## Using **list** and **upgrade**
To search for an available update for a specific app, use to the [**list**](.\list.md) command. Once you have identified that a update is available for your specific app, use **upgrade** to install the latest. 

The example below shows the [**list**](.\list.md) command being used to identify that an update is available for *Microsoft.WindowsTerminalPreview*. The user then uses **upgrade** to update the application.
![Animation demonstrating upgrade command](./images/listUpgrade.gif)

## **upgrade** --all

**upgrade --all** will identify all the applications with upgrades available. When you run **winget upgrade --all** the Windows Package Manager will look for all applications that have updates available and attempt to install the updates.

> [!NOTE]
> Some applications do not provide a version.  They are always latest.  Because the Windows Package Manager cannot identify if there is a newer version of the app, an upgrade will not be possible.
