# Setting up
* [Prerequisites](#prerequisites)
* [Setting up the development environment](#setting-up-the-development-environment)
* [Setting up static analysis tools](#setting-up-static-analysis-tools)

The instructions in all parts of this document work for Linux, OS X, and Windows, with the following pointers:
- Change `./gradlew` to `gradlew.bat` in Windows.
- Change all references of `Eclipse → Preferences → ...` to `Window → Preferences → ...` in Windows.
- All the commands are assumed to be run from the root project folder, unless otherwise specified.
- When a version is specified for any tool, install that version instead of the latest version available.

> If you encounter any problems during the setting up process, please refer to our [troubleshooting guide](troubleshooting-guide.md) before posting a help request in our [issue tracker](https://github.com/TEAMMATES/teammates/issues).

## Prerequisites

1. Install GitHub for Windows/Mac (recommended), or at least, Git.
1. Install JDK 1.7.
1. Download [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/) version Luna.
1. Install Google Plugin for Eclipse version 4.4.<br>
   Be careful to omit other plugins shown on the screen (e.g Google App Engine Tools for Android, GWT plugin).<br>
   Instructions can be found [here](https://developers.google.com/eclipse/docs/install-eclipse-4.4).<br>
   Note: Sometimes the update site for the GAE plugin does not work. In that case, follow the instructions [here](https://developers.google.com/eclipse/docs/install-from-zip).
1. Install the latest [TestNG Eclipse plugin](http://testng.org/doc/download.html).

## Setting up the development environment

1. Fork our repo at https://github.com/TEAMMATES/teammates.git. Clone that fork to your hard disk.
1. Run the command `./gradlew appengineDownloadSdk` to obtain a copy of the Google App Engine SDK.
1. Configure Eclipse (if you worry that these settings will interfere with your other projects, you can use a separate Eclipse instance for TEAMMATES):
   * Google App Engine: Go to `Eclipse → Preferences → Google → App Engine`, click the `Add` button, and point it to where Gradle keeps the SDK.<br>
     This directory can be found by running the command `./gradlew printUserHomeDir`.<br>
     Further instructions for installing can be found [here](https://developers.google.com/eclipse/docs/using_sdks).
   * Text encoding: Go to `Eclipse → Preferences → General → Workspace`, change the `Text file encoding` setting from `Default` to `Other: UTF-8`.
   * JRE: Go to `Eclipse → Preferences → Java → Installed JRE` and ensure a JDK (not a JRE) is selected (use JDK 1.7, as recommended by GAE).
     One of the items in the [troubleshooting guide](troubleshooting-guide.md) explains how to do this.
   * Tab behavior: In TEAMMATES, we use 4 spaces (2 spaces for HTML) in place of tabs. Configure it with `Eclipse → Preferences → `:
     * `General → Editors → Text Editors → Insert spaces for tabs`
     * `Web → HTML Files → Editor`
     * `Web → CSS Files → Editor`
     * `JavaScript → Code Style → Formatter → Edit → Tab Policy → Spaces Only`
     * `XML → XML Files → Editor`
   * HTML/JSP syntax: HTML/JSP syntax validator provided by Eclipse is not used during build-time.<br>
     To turn it off, go to `Eclipse → Preferences → Validation → HTML Syntax Validator` and uncheck the `Build` option. Similarly with `Eclipse → Preferences → Validation → JSP Syntax Validator`.
1. Run the command `./gradlew setup`.<br>
   This creates the main config files (these are not under revision control because their contents vary from developer to developer).
   * `.project`<br>
   * `gradle.properties`<br>
     If you want to use a JDK other than the one specified in your PATH variable, add the value to the variable `org.gradle.java.home`.<br>
     This value must be a valid **JDK 1.7** directory.
   * `src/main/resources/build.properties`<br>
     For now, property values can remain as they are.<br>
     (Optional) If you want to use alternative email services to develop and test email features, refer to [this document](emails.md).
   * `src/test/resources/test.properties`<br>
     Append a unique id (e.g your name) to **each** of the default accounts found at the bottom of this file,
     e.g change `test.student1.account=alice.tmms` to `test.student1.account=alice.tmms.KevinChan`.
   * `src/main/webapp/WEB-INF/appengine-web.xml`<br>
     For now, property values can remain as they are.
1. Run the command `./gradlew resetEclipseDeps`.<br>
   This will download the dependencies required by TEAMMATES and places them in the appropriate directories to be used by Eclipse.<br>
   In addition, it will generate the `.classpath` file for Eclipse configuration.<br>
   This command can be run again whenever the dependencies need to be updated.
1. Import the project to your Eclipse instance.
   * Start Eclipse and go to `File → Import...`.
   * Select `Existing Projects into Workspace` under `General`.
   * Set the `root directory` to the location where the repo is cloned.
   * Click `Finish`.

If you followed every step correctly, you should have successfully set up the development environment.
You may proceed to the development routine as lined out in [this document](development.md).

## Setting up static analysis tools

TEAMMATES uses a number of static analysis tools in order to maintain code quality and measure code coverage.
It is highly encouraged to set up these tools in your local development environment.

Refer to [this document](staticAnalysis.md) for details on the tools used, how to set them up, and how to run them locally.
