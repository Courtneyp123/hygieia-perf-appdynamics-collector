---
title: AppDynamics Collector
tags:
keywords:
summary:
sidebar: hygieia_sidebar
permalink: appdynamics.html
---
Configure the AppDynamics Collector to display and monitor information (related to application performance management) on the Hygieia Dashboard, from AppDynamics. Hygieia uses Spring Boot to package the collector as an executable JAR file with dependencies.

### Setup Instructions

## Fork and Clone the Collector 

Fork and clone the AppDynamics Collector from the [GitHub repo](https://github.com/Hygieia/hygieia-perf-appdynamics-collector). 

To configure the AppDynamics Collector, execute the following steps:

*   **Step 1: Change Directory**

Change the current working directory to the `hygieia-perf-appdynamics-collector` directory of your Hygieia source code installation.

For example, in the Windows command prompt, run the following command:

```bash
cd C:\Users\[username]\hygieia-perf-appdynamics-collector
```

*   **Step 2: Run Maven Build**

Run the maven build to package the collector into an executable JAR file:

```bash
mvn install
```

The output file `[collector name].jar` is generated in the `hygieia-perf-appdynamics-collector\target` folder.

*   **Step 3: Set Parameters in Application Properties File**

Set the configurable parameters in the `application.properties` file to connect to the Dashboard MongoDB database instance, including properties required by the AppDynamics Collector.

To configure parameters for the AppDynamics Collector, refer to the sample [application.properties](#sample-application-properties-file) file.

For information about sourcing the application properties file, refer to the [Spring Boot Documentation](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#boot-features-external-config-application-property-files).

*   **Step 4: Deploy the Executable File**

To deploy the `[collector name].jar` file, change directory to `hygieia-perf-appdynamics-collector\target`, and then execute the following from the command prompt:

```bash
java -jar [collector name].jar --spring.config.name=appdynamics --spring.config.location=[path to application.properties file]
```

### Sample Application Properties File

The sample `application.properties` file lists parameters with sample values to configure the AppDynamics Collector. Set the parameters based on your environment setup.

```properties
		#Database Name
		database=dashboarddb

		#Database HostName - default is localhost
		dbhost=localhost

		#Database Port - default is 27017
		dbport=27017

		#Database Username - default is blank
		dbusername=dashboarduser

		#Database Password - default is blank
		dbpassword=dbpassword

		#Logging File
		logging.file=./logs/appd-collector.log

		#Collector schedule (required)
		appdynamics.cron=1 * * * * *

		#AppDynamics server (required)
		appdynamics.instanceUrls=http://appdynamics.company.com

		#AppDynamics Username (required)
		appdynamics.username=APPD_USERNAME (if multi-tenancy, then APPD_USERNAME@TENANT)

		#AppDynamics Password (required)
		appdynamics.password=APPD_PASSWORD
```
