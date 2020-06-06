## JAVA content repository (JCR)
- suports structured and unstructured data
- CRX - Adobe's implementation of JCR
- Suppots namespace, (jcr:title)

## Repository structure
- /apps - all custom templates, components and any other custom code. (Sling Resource Merger - dupliocate the required /libs folder structure in /apps and modify the node or property)
- /libs - All libraries coming from AEM (foundation components)
- /conent - all site content
- /conf - all configuration files
- /etc - all rsources related to utilities and tools
- /var - files that change and are updated by the system

## Apache Sling
- A web application framework
	- REST
	- applications are built as OSGi bundles
	- resource oriented
- Apache Felix OSGi framework provides a dynamic runtime env. Code and content bundles can be loaded dynamically at runtime.
- Everything is a resource:
	- a request url is first resolved to a resource
	- selects the servlet or script to handle the request
	- everything is available from the ResourceResolver

## The functional building blocks of AEM (Granite)
- includes all the application layer functionalities


# Installation
- Author and Publish instance
- Dispatcher: A static web server (Apache httpd, IIS, etc)
	- caches webpages produced by the Publish instance

## Prerequisites
- AEM JAR file
- AEM license key properties file
- JDK 1.8
- 4GB hard disk and 4GB RAM (minimum)

## Installing
- place the JAR file and license keys under the same folder
- rename the JAR file to include run mode and port number
	- aem-author-p4502
	- aem-publish-p4503
- double click to install for the first time

## Start the AEM instance
- double click the JAR file
- Command Line
	- `java -jar aem-author-p4502.jar -h`
	- Xms -> assigns initial heap size
		- -Xms512
	- Xmx -> maximum heap size
		- -Xmx1024
	- Debug mode
		- `agentlib:jdwp=transport=dt_socket,address=8000,server=y,suspend=n`

# Developer toolset
## The Web Console
- localhost:4502/system/console
- The Web Console tab
	- Bundles: installing and managing bundles
	- Components: managing and controlling the sttaus of components
	- Configuration: configuring the OSGi bundles
- OSGi tab
	- Events: recording the events
	- Log Service - recording messages' output to the Web Console
	- Package Dependencies - recording packages and class names
	- Services: displaying and recording services

## CRXDE Lite
- Explorer pane: displays a tree of all the nodes in the repository
- Edit pane: edit and save he file
- Properties tab: Displays the properties of the node, add/delete/edit the properties

## Packages
- Package manager:
	- create, build, download content packages
	- uplaod and install packages
	- modify existing packages
	- view package info
- Package Share:
	- a centralized server that contains both public and private packages
- Creating and building new packages
	- Created by applying rules that will extract content from the repository
	- Rebuild
	- Edit
	- Test
	- Rewrap: recreates the package with additional info like thumbnails and icons.
- A typical content package includes:
	- jcr_root: root node of the repository, contains actual content of the package
	- META-INF: contains metadata regarding node definitions and also contains the filter.xml file
- Package Share:
	- Adobe official packages
	- public 3rd party packages
	- private packages from your organizations

## Configuring the development environment
- Maven, Eclipse, FileVault

- Working with Maven
	- Contents of a POM file
		- General project info
		- Build settings
		- Build environment: build profiles used for different envs
		- POM relationship and dependencies
			- groupId
			- artifactId
			- Version
			- Dependencies
		- Snapshot versions: projects under active development
		- Property references: refer to properties from another part of the POM file
		- Plugins: compiling source, packaging WAR file
	- The UberJar
		- all public Java APIs exposed by AEM
		- limited external libraries
		- interfaces and classes exported by an OSGi bundle
		- MANIFEST.MF with the correct package expoer versions for all exported packages

## Setting up project
- uisng maven archetype
	- ```mvn -B archetype:generate \
		-D archetypeGroupId=com.adobe.granite.archetypes \
		-D archetypeArtifactId=aem-project-archetype \
		-D archetypeVersion=23 \
		-D aemVersion=cloud \
		-D appTitle="My Site" \
		-D appId="mysite" \
		-D groupId="com.mysite" \
		-D frontendModule=general \
		-D includeExamples=n
		```

# Using OSGi Services
