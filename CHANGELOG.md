## [2.7.0]

- Added support for scanning of Scala and Swift projects.
- Added support for scanning of C/C++ and Objective-C projects in Windows and Linux.
- PT AI 5.2.0 API support.

## [2.6.0]

 - Added limited support for branch management: when synchronizing a local project and PT AI Enterprise Server project, the oldest branch is connected.
 - Added support for scanning of projects written in C# version 12 and projects created in .NET version 8.
 - Added support for scanning of .Net projects in macOS.
 - Updated the JSA.JS scan core for macOS.
 - Added the PT AI SERVER section where you can configure synchronization between a local project and PT AI Enterprise Server project.
 - PT AI 5.0.0 API support.

## [2.5.0]

- To help users sort out a large number of vulnerabilities detected during project scanning, the Assistant function has been added to the plugin. Assistant helps with the following:
    - Suggests vulnerabilities to be confirmed or discarded.
    - Groups similar vulnerabilities and offers to confirm or discard the entire group.
- Java 21 support.
- JSA.Net core now supports scanning projects in C# version 11.
- JSA.JavaScript core now supports the React framework.
- AI.PHP core, previously used to scan PHP projects, has been replaced with JSA.PHP.
- Fixed the Connection reset by peer error that occurred when scanning Go projects.
- Fixed a Java project scanning error that occurred when specifying JVM startup parameters.
- Fixed an issue with dependency loading when scanning Java projects.
- PT AI 4.11.0 API support.

## [2.4.2]

 - Plugin now allows you to select the SCA analysis module when creating a project on server PT AI.
 - Vulnerable components and vulnerabilities in components detected by the module and pulled from server PT AI are displayed in the list of vulnerabilities.
 - Fixed an error in the JSA.Go core that occurred when scanning Go projects.
 - Fixed an issue that caused the JSA.JVM core to incorrectly complete scanning of files containing a hyphen in the name.
 - PT AI 4.10.0 API support.

## [2.4.0]

New ways to integrate with PT AI Enterprise Edition have been added. Now you can do the following: 

 - Run a local project scan in PT AI Enterprise Server with or without saving the results on the server.
 - Send the source code of a project to PT AI Enterprise Server without running a scan
 - Synchronize scan results between the plugin and the PT AI server 
 - PT AI 4.9.1 API support.

## [2.3.1]

The following changes have been made in version 2.3.1:

- Added the Solidity programming language. You can enable code analysis for this language in the .aiproj.json file.
- Added the option to specify the path to downloaded dependencies used when analyzing code in Java and Python projects. The path parameter for downloading dependencies DependenciesPath must be specified in the .aiproj.json file in the PythonSettings or JavaSettings section.
- PT AI 4.8.1 API support.

## [2.3.0]

- PT AI 4.8.0 API support added.
- Minor bugfix

## [2.2.4]

- Minor bugfix

## [2.2.3]

To make the plugin easier to use, we added the PT APPLICATION INSPECTOR tab to the Activity Bar. This tab contains the following:
-    The new CODE SCANNING section with the list of detected vulnerabilities, scan start and stop buttons (moved from the the status bar in the lower part of the window), and the filter button to filter vulnerabilities by severity, status, and suppression from scan results (duplicates the PT Application Inspector: Show Vulnerabilities command).
-    The DATA FLOW, ADDITIONAL CONDITIONS, SCAN HISTORY, and EXPLOIT sections moved from the EXPLORER panel.

## [2.2.2]

- Fixed links in README.

## [2.2.1]

- For static analysis of JavaScript and TypeScript applications, you can now use separate scan modules: Taint and JSA. You can manually select one of them or both by aiproj file.
- Fixed the Java project scanning errors.
- Fixed the error that occurred when scanning with the module that searches for vulnerable components in an isolated network.
- PT AI 4.7.1 API support added.

## [2.2.0]

- In version 2.2.0, you can scan applications written in several languages. When creating a project, PT Application Inspector plugin analyzes extensions of project files with source code and automatically identifies their languages. If necessary, you can change languages manually.
- Added support for the Ruby language and its scan engine.
- Added support for the Go language and its scan engine.
- Added the JSA.Net scan engine that allows scanning C# projects in Windows and Linux.
- Replaced the scan engine for Java projects. This fixed issues with dependency loading and improved search for vulnerabilities.
- Improved the calculation mechanism for the RAM allocated to the processor cores during local scanning if the Use all available resources setting is disabled in the plugins. Improved stability of scan results.
- PT AI 4.7.0 API support added.

## [2.1.0]

- You can now confirm, discard vulnerabilities from scan results in their context menu in the code editor (quick fix actions)
- For the Precheck scanning stage, the Feeds processing step is now displayed
- The [PT AI] SCAN HISTORY section is now displayed not only in developer mode
- Entering the PT Application Inspector: Show vulnerabilities command now automatically opens the PROBLEMS tab
- In case of an error in the code analyzer installation, a pop-up window now displays the Try
again button, which you can click to restart the installation on the spot
- Data is now stored using SQLite instead of LiteDB
- For languages that have a main scan module (Java, JavaScript/TypeScript, PHP and Python), the PM Taint core is no longer used
- Optimized the scanning process
- ALT Linux OS is now supported in the test mode
- PT AI 4.6.0 API support added.

## [2.0.1]

- PT AI 4.5.0 API support added
- Minor bugfixes

## [2.0.0]

- Added the possibility of teamwork - integration with Application Inspector Enterprise
- The pre-check stage for the vulnerable components search module has been accelerated
- Scan settings format changed (.aiproj file)
- Minor bugfixes

## [1.3.0]

- Added the ability to scan Python applications

## [1.2.0]

- Added the ability to scan JavaScript and TypeScript applications

## [1.1.0]

- Added the ability to scan Java applications

## [1.0.0]

- Initial release!
