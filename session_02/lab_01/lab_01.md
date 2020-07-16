![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

### Lab 1 - Building and Pushing Your First Application

#### Target Tanzu Appliction Service Instance
1. If you haven't already, download the latest release of the PCF CLI for your operating system and install it.
2. Use the API target and username/password provided by the instructor..
3. Login to Pivotal Cloud Foundry (sso):
```
cf api api.sys.fowler.cf-app.com --skip-ssl-validation
```
4. Follow the prompts, choosing default organization and space.

#### Build Application
`cd cloud-cache-examples/hello-world`

link:/README.md#course-materials[Course Materials home] | link:/session_03/lab_02/lab_02.adoc[Lab 2 - Binding to Cloud Foundry Services]
