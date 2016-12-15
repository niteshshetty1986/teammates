# Tool stack
* [Deployment environment](#deployment-environment)
* [Development environment](#development-environment)
  * [Online services and integrations](#online-services-and-integrations)
* [Tools used in implementation](#tools-used-in-implementation)
* [Tools used in testing](#tools-used-in-testing)

Where third-party libraries are used, their version numbers are specified in `build.gradle` and `package.json` for server-side and client-side dependencies, respectively.

## Deployment environment

* **Google App Engine (GAE) Standard Environment**
* **Live site**: http://teammatesv4.appspot.com

## Development environment

* **Eclipse IDE for Java EE developers** (version Luna)
* **GAE Plugin for Eclipse** (version 4.4)
* **GAE SDK** (version specified in `build.gradle`)
* **Google Cloud SDK** (latest stable version): A set of tools for managing resources and applications hosted on Google Cloud Platform. We use it to run client scripts on GAE remotely. This is not used unless you need to run scripts against a production server.
* **Gradle** (version 2.12): Build and dependency management tool.
* **Node.js** (version 4.0.0 or later): We use Node Package Manager (NPM) from Node.js as a dependency management tool.
* **CheckStyle, PMD, FindBugs, Macker, ESLint, stylelint**: Static analysis tools for code quality check. The details of these tools can be found in [this document](staticAnalysis.md).
* [**PowerPointLabs**](http://powerpointlabs.info) (Sister project): Used for creating demo videos.
* (Optional) [**HubTurbo**](https://github.com/HubTurbo/HubTurbo/wiki/Getting-Started) (Sister project): Can be used as a client for accessing the GitHub issue tracker.
* (Optional) [**SourceTree**](https://www.sourcetreeapp.com) or [**GitHub for Windows/Mac**](https://desktop.github.com) or equivalent (latest stable version) to use as a GUI client for Git.

### Online services and integrations

* [**GitHub**](https://github.com): Used to host the repo, facilitate code review, track issues/bug reports/feature requests, and as a discussion board.
* [**Travis CI**](https://travis-ci.org): Used as a continuous integration server to build and test incoming pull requests and builds.
* [**VersionEye**](https://www.versioneye.com): Used to check for updates, license violations, and possible security loopholes for third-party libraries.

## Tools used in implementation

* **Java** (version 7, this is the highest version supported by GAE Standard Environment)
* **Java Server Pages (JSP)**: JSP technology provides a simplified way to create dynamic web content. A JSP page can be thought as an HTML page with embedded Java code snippets.
* **HTML5, CSS3, JavaScript ES5** (using later features of HTML5, CSS3, or later versions of JavaScript such as ES6 are discouraged due to lack of enough Browser support)
* **JSON (JavaScript Object Notation)**: JSON is a lightweight data-interchange format. It is easy for humans to read and write, and easy for machines to parse and generate. It is based on a subset of the JavaScript.

The following tools are provided by GAE SDK:
* **Java Servlets** (version 2.5): Java Servlet technology provides a simple, consistent mechanism for extending the functionality of a Web server and for accessing existing business systems. A servlet can almost be thought of as an applet that runs on the server side -- without a face.
* **Java Data Objects (JDO)** (version 2.3; while GAE supports JDO 3.0 as well, we continue to use JDO 2.3 because it is easier to set up):
  JDO is a standard interface for storing objects containing data into a database. The standard defines interfaces for annotating Java objects, retrieving objects with queries, and interacting with a database using transactions. An application that uses the JDO interface can work with different kinds of databases without using any database-specific code, including relational databases, hierarchical databases, and object databases.
* **DataNucleus Access Platform** (version 1; while GAE supports DataNucleus version 2 as well, the version that goes with JDO 2.3 is version 1):
  DataNucleus Access Platform provides persistence and retrieval of data to a range of datastores using a range of APIs, with a range of query languages.
* **Java Persistence API (JPA)** (version 1.0; while GAE supports JPA 2.0 as well, the version that goes with DataNucleus version 1 is JPA 1.0):
  JPA is a standard interface for accessing databases in Java, providing an automatic mapping between Java classes and database tables.

The following third-party libraries are used to perform certain server-side tasks:
* **JSP Standard Tag Library (JSTL)**: JSTL extends the JSP specification by providing a standard set of JSP tags for common tasks, and allows creation of custom tags for use in JSP files.
* **Gson**: A Java library that can be used to convert Java objects into their JSON representation. It can also be used to convert a JSON string to an equivalent Java object.
* **Xerces2 Java Parser**: A high performance, fully compliant XML parser. It is used to parse the XML config files. This library may not be needed on some platforms (particulary Windows) as it may already come packaged on some JREs.
* **Jsoup**: A Java library for working with real-world HTML. It provides a very convenient API for extracting and manipulating data, using the best of DOM, CSS, and jquery-like methods. It is needed by some email services to obtain the plain text component from the HTML component.
* **Joda-Time**: A de facto standard date and time library for Java prior to JDK 1.8.
* **OWASP HTML Sanitizer**: A fast and easy-to-configure HTML sanitizer which lets us include HTML authored by third-parties while protecting against XSS. It is needed to sanitize rich-text content from users of the application.
* **SendGrid, Mailgun, Mailjet**: Alternative frameworks to JavaMail for sending emails. The details of these tools can be found in [this document](emails.md).

The following third-party libraries are used to perform certain client-side tasks:
* **jQuery**: A fast, small, and feature-rich JavaScript library. It makes things like HTML document traversal and manipulation, event handling, animation, and AJAX much simpler with an easy-to-use API that works across a multitude of browsers.<br>
  Some plugins such as **highlight**, **guillotine**, and **printthis** are used to perform additional tasks.
* **Bootstrap**: A popular HTML, CSS, and JS framework for developing responsive, mobile first projects on the web.
* **TinyMCE**: A JavaScript library for platform independent "WYSIWYG" or rich-text editing.
* **Moment.js**: A JavaScript library to parse, validate, manipulate, and display dates.

## Tools used in testing

The following are the major testing frameworks used:
* **TestNG**: Java test automation framework.
* **Selenium**: Browser automation framework, for automating UI tests.
* **JaCoCo**: Java code coverage library.
* **EclEmma**: JaCoCo plugin and integration for Eclipse.
* **QUnit**: JavaScript unit test framework.
* **Blanket.js**: JavaScript code coverage library.

In addition, the following third-party libraries are used to perform certain tasks:
* **Jsoup**: A Java library for working with real-world HTML. It provides a very convenient API for extracting and manipulating data, using the best of DOM, CSS, and jquery-like methods. It is used during UI testing, for performing a logical comparison of the pages seen in browser against generated expected pages.
* **JavaMail**: Provides a platform-independent and protocol-independent framework to build mail and messaging applications. It is used for accessing test users' email accounts to examine emails sent by a production server.
* **HttpUnit**: A Java library for the automatic simulation and testing of web applications. We use the `ServletUnit` component to create servlet objects used for testing.
