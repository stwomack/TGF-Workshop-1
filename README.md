![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
TMC Workshop demonstrating caching and session offloading

## Agenda

Time | Session
---- | -------
9:00 AM - 9:15 AM | _Workshop Kickoff And Intros_
9:15 AM - 10:00 AM | _Presentation: Tanzu Gemfire by VMare_
10:15 AM - 12:00 PM | _Developer Workshop (*LABS*)_
12:00 PM - 1:00 PM | _Lunch_

**Prerequisites**

Start by downloading and installing the appropriate prerequisite tools.
- [Cloud Foundry CLI](MAC: https://cli.run.pivotal.io/stable?release=macosx64&source=pws, Windows: https://cli.run.pivotal.io/stable?release=windows64&source=pws) to interact with a cloud foundry instance
- [Git Client](https://git-scm.com/downloads) to clone Github repo or download and unzip
- An IDE, like [Spring Tool Suite](https://spring.io/tools/sts/all) or [IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
- [Java SE Development Kit](http://info.pivotal.io/n0I60i3021AN0JU0le10CRR)

**Download materials**

Next, download the course materials.  This can be accomplished either through the GitHub website by downloading a repository zip and unzipping locally, or if you have Git installed, use the following commands:

```
git clone https://github.com/stwomack/at-cloud-native-workshop.git
cd at-cloud-native-spring-workshop
```

```
$ git clone git@github.com:stwomack/at-cloud-native-workshop.git
$ cd at-cloud-native-spring-workshop/
```

***NOTE***
When labs reference $COURSE_HOME, that's where you checked out this repository

**PCF Environments**

In order to perform the labs, you must be connected or logged into a live PCF environment.
## Labs Materials

### _Cloud Native Architectures and Frameworks( Microservices, 12Factor Apps )_ [(Slides)](session_02/Session_02-Cloud_Native_Architectures_and_Frameworks.pptx)

### _Enabling Continuous Delivery with 'cf push'_
  - [Lab 1 - Building and Pushing Your First Application](session_03/lab_01/lab_01.adoc)
  - [Lab 2 - Binding to Cloud Foundry Services](session_03/lab_02/lab_02.adoc)
  - [Lab 3 - Scaling Applications](session_03/lab_03/lab_03.adoc)
  - [Lab 4 - Monitoring Applications](session_03/lab_04/lab_04.adoc)

### _Lunch:_
  
### _Spring Boot and Actuator_ [(Slides)](session_05/Session_05-Spring_Boot_Actuator-2xpg.pdf)
  - [Lab 5 - Introspection, Monitoring, and Metrics using Spring Boot Actuator](session_05/lab_05/lab_05.adoc)
  
### _Spring Cloud Services_  [(Slides)](session_06/Session_06-Spring-Cloud-Services-2xpg.pdf)
  - [Lab 6 - Spring Cloud Config Server](session_06/lab_06/lab_06.adoc)

