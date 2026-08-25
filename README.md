## Overview

The PT Application Inspector plugin finds vulnerabilities and undocumented features in application source code. In addition to code analysis, built-in modules detect errors in configuration files and vulnerabilities in third-party components and libraries used in application development. The plugin supports the following languages: C#, Go, Java, JavaScript, Kotlin, PHP, Python, Ruby, Scala, SQL, Solidity, TypeScript, C/C++, Objective-C, and Swift.

***Note.** The scanning of projects in C/C++, Objective-C, and Swift is not supported in macOS.*

## How it works

### Enabling and disabling the plugin

You can enable or disable the plugin in the open project folder. If it is not the first time you are opening the project, the plugin is enabled automatically (scan and action history is saved). You can also set up the plugin to be automatically enabled when a new project is opened.

When the plugin is enabled, the **.ai** folder is created in the project. This folder contains a database, log files, and a configuration file.

![The .ai folder](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-enable-plugin.gif?raw=true)

### Installing the code analyzer

For the plugin to operate correctly, the PT Application Inspector code analyzer is required. You can install it automatically by clicking **Download Analyzer** in the pop-up notification in the Visual Studio Code interface or manually by downloading it from the link in the instructions below.

To manually install the code analyzer:

1. Download the archive with the analyzer using one of the links:

   * For Windows: [download](https://update.ptsecurity.com/api/v6/products/AI.INFRASTRUCTURE.INSTALLATOR.zip/2.9.0.1126/download/AI.INFRASTRUCTURE.INSTALLATOR.2.9.0.1126.zip)

   * For Linux: [download](https://update.ptsecurity.com/api/v6/products/AI.INFRASTRUCTURE.INSTALLATOR.tar.gz/2.9.0.1126/download/AI.INFRASTRUCTURE.INSTALLATOR.2.9.0.1126.tar.gz)

   * For macOS: [download](https://update.ptsecurity.com/api/v6/products/AI.INFRASTRUCTURE.INSTALLATOR.pkg/2.9.0.1126/download/AI.INFRASTRUCTURE.INSTALLATOR.2.9.0.1126.pkg)

2. In macOS, run the following command to remove the `com.apple.quarantine` attribute:

```bash
   xattr -d com.apple.quarantine <analyzer_file_path.pkg>
```

   Then run the installation file and follow the instructions.

3. The analyzer must be installed or unpacked to the following locations:

   * In Windows: `%LOCALAPPDATA%\Application Inspector Analyzer`

   * In Linux: `~/application-inspector-analyzer`

   * In macOS: `/Library/Application-Inspector-Analyzer`

![Installing the code analyzer](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-downoload-analyzer.gif?raw=true)

### Scanning a project

You can start a project scan in the following ways:
* By clicking the ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/start-scan.png) or ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/start-full-scan.png) in the **CODE SCANNING** section.
* By saving project changes (if you selected **On saving** for the **Trigger scan** setting).
* By running the command `PT Application Inspector: Scan Locally`.
* By running the command `PT Application Inspector: Start Full Local Scan`.

***Note.** Before scanning, all changes to the project are automatically saved.*

You can monitor the scan progress on the **OUTPUT** tab. The first scan usually takes longer due to the initial load on the database of vulnerable components.

General scan settings are configured in the `.aiproj.json` configuration file. You can create a configuration file and configure scan settings in it by running the command `PT Application Inspector: Create Project Settings File`.

![Starting a scan](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-start-scan.gif?raw=true)

### Stopping a scan

You can stop a project scan by running the command `PT Application Inspector: Stop Scan` or by clicking the ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/stop-scan.png) button in the **CODE SCANNING** section.

## Analyzing scan results

You can find the list of detected vulnerabilities in the **PROBLEMS** tab and in the **CODE SCANNING** section. If you click a vulnerability in the list, the line with its exit point gets highlighted in the code editor.

The **VULNERABILITY CODE** section may contain a data-flow diagram or a set of metavariables (only for the Solidity language and the Pygrep scan core).

The data-flow diagram shows how each process converts its inputs into outputs and how the processes interact with each other. The diagram may consist of the following sections:
* **Entry point**. A point where data flow analysis starts.
* **Data entry point**. A file and code line where untrusted data enter the program.
* **Data changes**. The description of one or several functions that modify potentially harmful input data. This section may not be displayed on the diagram if the input data were not modified.
* **Exit point**. The execution line of a potentially vulnerable function. This is the exit point related to the vulnerability in the source code.

You can go to the corresponding place in the code editor from any section of the data-flow diagram.

When scanning a project, the Pygrep kernel uses rules from the PT AI Enterprise Edition knowledge base or custom rules, the path to which is specified in the Solidity language settings. Each rule contains templates describing metavariables and regular expressions for finding these metavariables. A vulnerability is considered to be found if lines of code are found in which a regular expression corresponding to a metavariable gets a match.

![The [PT AI] Data flow section](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-data-flow.gif?raw=true)

The **EXPLOIT** section contains an automatically generated HTTP request that you can edit and use to check the vulnerability in a deployed web application.

***Note.** To exploit a vulnerability, specify the address of the host where your web application is deployed in the `.aiproj.json` file. The default value is "localhost."*

***Note.** To send an HTTP request, a third-party extension is required. It is recommended that you use the REST client.*

![Vulnerability exploitation](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-exploit.gif?raw=true)

Some vulnerabilities have additional exploitation conditions. They are displayed under **ADDITIONAL CONDITIONS**.

The contents of the **PT APPLICATION INSPECTOR** sections depend on the code line selected in the editor.

When you scroll through the sections of the diagram, the vulnerability information is automatically pinned until you move on to another vulnerability. If you want to view information about a certain vulnerability while working on the code, you can pin this vulnerability manually.

![Pinning a vulnerability](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-pin-unpin.gif?raw=true)

Several vulnerabilities can have the same exit point. If these vulnerabilities belong to the same type, they are grouped together and displayed as one problem with different exploitation options. In **PT APPLICATION INSPECTOR** sections, use the left and right arrows to view detailed information about such vulnerabilities.

***Note.** If you confirm one vulnerability from the group, the whole problem will be confirmed automatically. To discard an entire problem, you must discard all the vulnerabilities in the group.*

![Group of vulnerabilities](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-group.gif?raw=true)

### Managing detected vulnerabilities

The PT Application Inspector plugin contains a set of tools for managing detected vulnerabilities. With these tools, you can do the following:
* Confirm or discard vulnerabilities in the following ways:
   * By clicking the ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/confirm.png) or ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/discard.png) button in the **VULNERABILITY CODE**, **ADDITIONAL CONDITIONS**, or **EXPLOIT** section.
   * Using the vulnerability list in the **CODE SCANNING** section. Select multiple vulnerabilities to simultaneously change their status by clicking the corresponding button.
   * Using the **Quick Fix** context menu displayed next to the highlighted vulnerability in the code editor.
* Suppress vulnerabilities from scan results:
   * Using the **Quick Fix** context menu.
   * Using the vulnerability list in the **CODE SCANNING** section. Select multiple vulnerabilities to simultaneously suppress them by clicking **//**.
* View vulnerability descriptions by selecting **Show description for \<vulnerability name\> (PT AI)** in the vulnerability context menu in the **PROBLEMS** tab or in the **Quick Fix** context menu.
* Filter vulnerabilities by severity, status, and suppression from scan results by running the command `PT Application Inspector: Show Vulnerabilities` or by clicking ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/filter.png) in the **CODE SCANNING** section.
* Manage the statuses of multiple vulnerabilities by selecting them in the **CODE SCANNING** section and changing the status for all of them by clicking the corresponding button.

![Excluding a vulnerability from scan results](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-actions.gif?raw=true)

![Filtering vulnerabilities by severity](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-show.gif?raw=true)

![Confirming and discarding vulnerabilities](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-confirm-discard.gif?raw=true)

### Using the assistant

If a large number of vulnerabilities is detected during project scanning, you can sort them out much faster using the assistant function. The assistant gives recommendations in the following order:
* Confirm vulnerabilities that have an exploit
* Discard vulnerabilities with a detected filtering function
* Confirm or discard a group of vulnerabilities similar in type or vulnerable code
* Review vulnerability statuses assigned manually by the user

![Assistant overview](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-assistant-overview.gif?raw=true)

You can start the assistant from the pop-up notification that appears when the scan is completed or by clicking the ![pic](https://github.com/POSIdev-community/AI.Plugin.VSCode/raw/release/2.9.0/media/readme/run-assistant.png) button. You can choose to go through the whole scenario or only certain steps.

![Assistant actions](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-assistant-action.gif?raw=true)

### Comparing scan results

You can compare results of two scans within a project. To do this, under **SCAN HISTORY**, select the scans you need and then select **Compare scan results** in the context menu.

![Comparing scan results](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-compare.gif?raw=true)

## Integration with PT AI Enterprise Edition

The PT Application Inspector plugin can be integrated with PT AI Enterprise Edition. The integration allows several team members to simultaneously work with vulnerabilities and their statuses in the IDE and PT AI Enterprise Edition web interface, thereby increasing code security.

To configure the integration:

1. Use one of the following ways to connect to PT AI Enterprise Server:

   * Run the `PT Application Inspector: Connect to PT AI Server` command.

   * Click the **Connect to PT AI Server** button in the **PT AI SERVER** section.

2. Enter the PT AI Enterprise Server URL and sign in to PT AI Enterprise Edition via your SSO system.

   ![Connecting to PT AI Enterprise Server](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-connect-to-server.gif?raw=true)

3. Perform the required integration scenario:

   * Upload the source code to PT AI Enterprise Server.

   ![Upload the source code](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-create-project.gif?raw=true)

   * Send a local project for scanning to PT AI Enterprise Server with or without saving the results on the server.

   ![Remote scan](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-remote-scan.gif?raw=true)

   * Synchronize the results of the local scan and the scan in PT AI Enterprise Server.

   ![Synchronizing projects](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-map-project.gif?raw=true)

4. Work with code, scan, confirm, and discard vulnerabilities as you normally do.

For more information about the integration, see the PT AI Enterprise Edition User Guide.

## Managing branches

If a project is a Git repository, the plugin uses a current branch as the local working branch. Local scan results, vulnerability statuses, and data on synchronization from PT AI Enterprise Server are associated with that branch.

When you set up synchronization between a local project and a PT AI Enterprise Server project, you must select the branch on the server that matches a current local branch. You can map a different branch later using the command `PT Application Inspector: Change PT AI Server Project Branch` or by clicking the **Switch branch** button in the **PT AI SERVER** section.

Branch mapping is needed for the following operations:
* Uploading source code to PT AI Enterprise Server
* Sending a local project to PT AI Enterprise Server for scanning
* Synchronization of vulnerability statuses and scan results

When you switch branches in Git, the plugin automatically switches to a corresponding local branch. If the new local branch is not yet mapped to a PT AI Enterprise Server branch, a notification with the **Select Branch** button is displayed. Before uploading code, syncing artifacts, or running a remote scan, you must select the required branch in PT AI Enterprise Server.

![Branch switching](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-switch-branch.gif?raw=true)

When the names of a local and remote branch differ, the plugin displays a warning before uploading source code or scan artifacts. You can continue the operation if the mapping was intentional, or you can cancel the action and select a different server branch.

If the Git repository is not initialized, the option to select a remote branch is still available. If the mapped branch was deleted in PT AI Enterprise Server, select a different branch when you receive the corresponding notification.

![Push to mapped branch](https://github.com/POSIdev-community/AI.Plugin.VSCode/blob/release/2.9.0/media/readme/AI-push-to-branch.gif?raw=true)

## Plugin commands and settings

### Plugin commands

To start working with the plugin, you can enter the following commands into the command palette:
* `PT Application Inspector: Scan Locally`. Start an incremental scan of a local project.
* `PT Application Inspector: Start Full Local Scan`. Start a full scan of a local project.
* `PT Application Inspector: Change PT AI Server Project Branch`. Change the PT AI Enterprise Server branch that matches a local working branch.
* `PT Application Inspector: Scan Remotely and Save Results on Server`. Start a full scan of a project in PT AI Enterprise Server and save the results on the server (command for integration).
* `PT Application Inspector: Scan Remotely Without Saving Results on Server`. Start a full scan of a project in PT AI Enterprise Server without saving the results on the server (command for integration).
* `PT Application Inspector: Stop Scan`. Stop the scan.
* `PT Application Inspector: Stop Remote Scan`. Stop the remote scan of a project in PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Show Vulnerabilities`. You can also filter vulnerabilities by severity, confirmation, and suppression status. Only the vulnerabilities that match the selected filters will be displayed.
* `PT Application Inspector: Enable`. Enable the plugin for the current project.
* `PT Application Inspector: Disable`. Disable the plugin for the current project.
* `PT Application Inspector: Download Analyzer`. Download the latest version of the code analyzer.
* `PT Application Inspector: Restart`. Restart the plugin.
* `PT Application Inspector: Create .aiignore File`. Create an exclusion configuration file. In the `.aiignore` file, you can specify folders, files, and file formats to be excluded from scanning using the `.gitignore` file syntax. For more information, see [git-scm.com/docs/gitignore](https://git-scm.com/docs/gitignore).
* `PT Application Inspector: Create Project Settings File`. Create the configuration file `aiproj.json`. In the file, you can change default scan settings. You can also use the **SkipGitIgnoreFiles** setting to exclude from scanning files and folders from the `.gitignore` file. By default, this setting is enabled.
* `PT Application Inspector: Connect to PT AI Server`. Connect to PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Reconnect to PT AI Server (Connected)`. Reconnect to PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Disconnect from PT AI Server`. Disconnect from PT AI Enterprise Server (command for integration).
* `PT Application Inspector: PT AI Server Authentication`. Enter the authentication token (command for integration).
* `PT Application Inspector: Manage Projects`. Display the list of projects from PT AI Enterprise Server (command for integration). With this command, you can select a project in PT AI Enterprise Server and connect your local project to it in Visual Studio Code.
* `PT Application Inspector: Create PT AI Server Project`. Upload a local project from IDE to PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Pull scan results from PT AI server`. Fetch scan results from PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Push scan results to PT AI server`. Send scan results to PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Push source code to PT AI server`. Upload the source code of a local project to PT AI Enterprise Server (command for integration).
* `PT Application Inspector: Run Assistant`. Run the assistant.
* `PT Application Inspector: Stop Assistant`. Stop the assistant.

### Plugin settings

You can configure the plugin settings by clicking **Extensions** → **PT Application Inspector** → the gear button → **Settings** in the action panel.

The plugin configuration page contains the following settings:
* **Allow telemetry collection**. Collection of general scan information to be sent to PT AI Enterprise Edition. By default, this setting is enabled.
* **Analyzer log level**. The severity level starting from which the code analyzer events will be logged. The default value is error.
* **Automatically enable for any project**. Silent activation of the plugin when opening a project. By default, this setting is disabled.
* **Developer mode**. Advanced plugin features. By default, this setting is disabled.
* **Maximum number of stored log files**. The default value is 100.
* **Number of days to store log files**. The default value is 30.
* **Number of scan results**. Maximum number of scan results saved in the scan result history. The default value is 10. If the limit is exceeded, each new scan result deletes the oldest result.
* **Trigger scan**. Start scan condition: manually on clicking a start button or automatically when a project file is changed. Default: manually.
* **Use all available resources for scanning**. The use of all available RAM and CPU resources to increase scanning speed. By default, this setting is disabled.
* **Actions with new scan results on the PT AI server**. The behavior of the plugin when receiving new scan results from PT AI Enterprise Server if synchronization with the project is configured. The default value is **Notify about new results**.
* **Run the assistant**. Activation of the assistant automatically after the first scan or manually by clicking the corresponding button. The default value is "Automatically after the first scan".
* **Quick Fix menu**. Display of assistant tips. By default, this setting is enabled.
* **Vulnerabilities to confirm or discard**. The number of vulnerabilities to be confirmed or discarded starting from which a notification from the assistant will be displayed. The default value is 15.
* **Similar vulnerabilities**. The number of similar vulnerabilities starting from which a notification from the assistant will be displayed. The default value is 15.

## Requirements

For the correct operation of the PT Application Inspector plugin, the following technical requirements must be met:
* Visual Studio Code IDE 1.72.0 or later
* 8 GB RAM
* 5 GB of free hard drive space

Supported 64-bit OS:
* Debian 11 Bullseye or later
* Fedora Workstation 38 or later
* OpenSUSE Leap 15.5 or later
* Ubuntu 22.04 LTS or later
* Ubuntu 23.04 or later
* Windows 10
* ALT Linux OS in the test mode

Supported macOS:
* Big Sur 11.5 or later
* Monterey 12.0.0 or later

## Privacy statement

By default, the PT Application Inspector plugin collects anonymous telemetry. This allows our specialists to improve the stability and performance of the product. They can optimize resource consumption and speed up scanning, find and fix errors across different IDE versions more quickly, and understand which features are used most often to improve the user experience.

Only technical metrics (interaction events, environment settings, and the main scanning settings) for the plugin and IDE are sent. Source code, credentials, tokens, and project contents are completely excluded. All data is transmitted over a secure HTTPS channel, processed anonymously, and not shared with third parties. It does not contain any confidential information.

If you do not want to participate in telemetry collection, disable the **Allow telemetry collection** setting. Changes take effect immediately, without restarting the IDE.
