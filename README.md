![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

## Agenda

Time | Session
---- | -------
9:00 AM - 9:15 AM | _Workshop Kickoff And Intros_
9:15 AM - 10:00 AM | _Presentation: VMware Tanzu GemFire_
10:15 AM - 12:00 PM | _Developer Workshop (*LABS*)_
12:00 PM - ??? | _Lunch and Beers_

**Prerequisites**

Start by downloading and installing the appropriate prerequisite tools.
- Cloud Foundry CLI from package manager `brew install cloudfoundry/tap/cf-cli`
- [Cloud Foundry CLI for other operating systems](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
- [Git Client](https://git-scm.com/downloads) to clone Github repo or download and unzip
- *Optional* An IDE, like [Spring Tool Suite](https://spring.io/tools/sts/all) or [IntelliJ IDEA](https://www.jetbrains.com/idea/download/)
- [Java SE Development Kit](http://info.pivotal.io/n0I60i3021AN0JU0le10CRR)

**Download materials**

Next, download the course materials.  This can be accomplished either through the GitHub website by downloading a repository zip and unzipping locally, or if you have Git installed, use the following commands:

```
git clone https://github.com/stwomack/TGF-Workshop-1.git
cd TGF-Workshop-1
```

***NOTE***
When labs reference $COURSE_HOME, that's where you checked out this repository

**TAZ Environments**

In order to perform the labs, you must be connected or logged into a live TAS environment.

## Labs Materials

### _VMware Tanzu GemFire_ [(Slides)](session_01/Session_01-VMware-Tanzu-GemFire.pdf)

### _Enabling Continuous Delivery with 'cf push'_
  - [Lab 1 - Build, Push, Bind A Simple Caching Application](session_02/lab_01/lab_01.md)
  - [Lab 2 - Look-Aside Caching](session_02/lab_02/lab_02.md)
  - [Lab 3 - Session State Caching](session_02/lab_03/lab_03.md)

### _Lunch and Beer_

