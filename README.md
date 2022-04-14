## Overview

The PT Application Inspector plugin allows finding security vulnerabilities and undocumented functionality in your application code as you write it. (PHP is supported). 

With the built-in analysis modules, the plugin highlights not only source code vulnerabilities and configuration file flaws but also vulnerable third-party components and libraries used in application development.

## Enabling and disabling the plugin

You can enable or disable PT Application Inspector in a currently open project folder. If it is not the first time the project is open, the plugin will be enabled automatically (the scan and action history is stored). You can also configure enabling the plugin automatically when you open a new project.

After you enable the plugin in your project, the .ai folder with the database, logs, and configuration file will be generated in your workspace. 

![AI-enable-plugin](/media/readme/AI-enable-plugin.gif)

## Installing the code analyzer

For the plugin to work properly, you must install the PT Application Inspector code analyzer. 

You can install the latest version in Visual Studio Code.

The path where it will be installed:
- In Windows: `%LOCALAPPDATA%\Application Inspector Analyzer`
- In Linux: `~/application-inspector-analyzer`
- In macOS: `/Library/Application-Inspector-Analyzer`

![AI-downoload-analyzer](/media/readme/AI-downoload-analyzer.gif)

## Scanning a project

You can start a project scan:

* By clicking `[PT AI] Start scan`
* By saving changes in a project (if you select `On saving` for the `Trigger scan` setting)
* With the `Start scan` command
* With the `Start full scan` command

> ***Note.** Before scanning, all changes in your project will be saved automatically .*

You can monitor the scan progress in the `Output` view and on the sidebar. The first scan can take a while because of the initial load on the database of vulnerable components.

It is possible to perform the general scan configuration in the file with the project settings. Run the `Create project settings file` command and edit the file to finetune the project analysis.

![AI-start-scan](/media/readme/AI-start-scan.gif)

## Stopping a scan

You can stop a project scan:

* By clicking `Stop scan`
* With the `Stop scan` command

## Exploring scan results

You can find the detected vulnerabilities in the `Problems` view and additional information about every vulnerability by clicking it.

The `[PT AI] Data flow` view contains a data flow diagram. It visualizes how each process converts its input into output and how processes interact.

The data flow diagrams consist of the following sections:

- **Entry point**. The starting point of the control flow. 

- **Data entry point**. A file and a code line with the coordinates of the input data entry.

- **Data changes**. The description of one or several functions that modify potentially malicious input data.

    > ***Note.** There may be no `Data changes` section in the diagram if input data is not modified.*

- **Exit point**. The execution line of a potentially vulnerable function. This is the exit point associated with the vulnerability in source code. The exit point coordinates are mapped to the vulnerability in the `Problems` view.

- **Best place to fix**. A code line best suited for patching a vulnerability. The section is displayed above the data flow.

You can go to the corresponding place in the editor from any section of the data flow diagram.

![AI-data-flow](/media/readme/AI-data-flow.gif)

When you click `[PT AI] Exploit`, an HTTP request is generated automatically. You can use an exploit to test a vulnerability detected in a deployed application.

> ***Note.** To exploit a vulnerability, you must specify a host where your application is deployed in the .aiproj file. Default: localhost.*

> ***Note.** To send an HTTP request, a third-party extention is required. We recommend that you use the REST client.*

![AI-exploit](/media/readme/AI-exploit.gif)

Some vulnerabilities have additional exploitation conditions. You can find them in the the `[PT AI] Additional conditions` view.

Content in the PT AI views depends on a code line where you place your cursor in the editor. 

When you browse through the diagram sections, the vulnerability information is pinned automatically until you move to another vulnerability. Also, if you want work on your code and view information about a particular vulnerability at the same time, you can pin the vulnerability manually.

![AI-pin-unpin](/media/readme/AI-pin-unpin.gif)

Several detected vulnerabilities may have the same exit point. Such vulnerabilities will be grouped if they have the same type. They will be displayed as one problem with different ways to exploit them. To view details on such vulnerabilities, go through the pages in the PT AI views.  

> ***Note.** If you confirm one vulnerability from a group, the entire problem will be confirmed. To discard the entire problem, you must discard all vulnerabilities in a group.*

![AI-group](/media/readme/AI-group.gif)

## Managing detected vulnerabilities

PT Application Inspector has a set of tools to manage detected vulnerabilities. Using the command palette and quick fix commands, you can suppress, confirm, discard, and filter them. 

Actions on vulnerabilities:
- Confirm or discard a vulnerability in the PT AI views.
- Suppress a vulnerability through the Quick fix menu.
- Filter detected vulnerabilities by severity, status, and `Suppressed` flag.

![AI-actions](/media/readme/AI-actions.gif)

![AI-show](/media/readme/AI-show.gif)

![AI-confirm-discard](/media/readme/AI-confirm-discard.gif)

## Comparing scan results

To compare two results within a project, select two scans in the `[PT AI] Scan history` view, right-click, and choose `Compare scan results`. 

> ***Note.** The comparing function and the `[PT AI] Scan history` view are available only if you enable the developer mode in the plugin settings.*

![AI-compare](/media/readme/AI-compare.gif)

## Commands and settings

### Commands available in the command palette:

<details>
    <summary><code>PT Application Inspector: Start scan</code></summary>
    <p>Start a project scan.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Start full scan</code></summary>
    <p>Start a full project scan.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Stop scan</code></summary>
    <p>Stop a scan. You cannot resume it afterwards.
The command is available while a scan is running.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Show vulnerabilities</code></summary>
    <p>Filter detected vulnerabilities by severity level, <b>Suppressed</b> flag, confirmation status. Only those vulnerabilities that match the selected filters will be displayed.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Enable</code></summary>
    <p>Enable the plugin for the current project.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Disable</code></summary>
    <p>Disable the plugin for the current project.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Download analyzer</code></summary>
    <p>Start downoloading the latest version of the analyzer.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Restart</code></summary>
    <p>Restart the plugin.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Create .aiignore file</code></summary>
    <p>Create a .aiignore file to exclude files and folders from scanning. The file syntax is similar to the .gitignore file. For more information on the syntax, see <a href="https://git-scm.com/docs/gitignore">https://git-scm.com/docs/gitignore</a>.</p>
</details>
<details>
    <summary><code>PT Application Inspector: Create project settings file</code></summary>
    <p>Scanning is performed based on the default settings. You can change them in the aiproj.json file. To create a .aiproj file, use this command. You can also use the <b>SkipGitIgnoreFiles</b> setting in the file to exclude from scanning files and folders from the .gitignore file. By default, it is enabled. </p>
</details><br>

### Settings

- **Allow telemetry collection**. Collect generalized data about scanned code and send it to Positive Technologies. To see a sample of collected data, click [here](/media/readme/telemetryExample.json). For details, refer to the privacy statement. Default: enabled.
- **Analyzer log level**. An analyzer log level. Default: error.
- **Automatically enable for any project**. Enable the plugin automatically for all projects without explicit confirmation from a user. Default: disabled.
- **Developer mode**. Activate the following functionality: `[PT AI] Scan history` view, comparing two scan results within a project, plugin logs in the output. Default: disabled.
- **Maximum number of stored log files**. Limit the number of stored log files. Default: 100.
- **Number of days to store log files for**. Limit the number of days to store log files for. Default: 30.
- **Number of scan results**. Limit the number of stored scan results. Stored scan results are displayed in the scan history. The setting is available only if you enabled the developer mode. If the limit is exceeded, every new scan result deletes the oldest scan result. If you reduce the limit, all extra results will be deleted and cannot be restored. Default: 10.
- **Trigger scan**. Select if a scan is started manually or after you save changes in a project. Default: manually.
- **Use all available resources for scanning**. Use all resources for faster scanning. It may negatively impact the performance of your computer. Default: disabled.

## Requirements
For the PT AI Application Inspector plugin to work correctly, the following technical requirements must be met:

* Visual Studio Code IDE version 1.65.0 or later
* 8 GB of RAM
* 5 GB of free disk space

Supported 64-bit OSs:
* Debian version 11.1 or later
* Fedora Workstation version 34 or later
* OpenSUSE version 15.3 or later
* Ubuntu Desktop version 20.04 or later
* Windows 10

Supported macOSs:
* Big Sur version 11.5 or later
* Monterey version 12.0.0 or later

## License
[EULA](LICENSE.txt)

## Privacy statement 
By default, the PT Application Inspector plugin collects anonymous usage data and sends it to Positive Technologies to help us understand how to improve the product. Positive Technologies does not pass collected information to third parties. Source code or IP addresses are not collected. You can stop data collection by disabling the `Allow telemetry collection` setting.

---
**Enjoy!**