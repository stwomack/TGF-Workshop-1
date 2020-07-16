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

#### Create an instance of Tanzu Gemfire
1.
2.
3.

#### Build Application
1. In a terminal window, from the directory you checked out this repo, change to the following directory:
```
cd cloud-cache-examples/hello-world
```
2. Build the application using gradlew
```
./gradlew build
```
3. Edit the manifest file, replacing name with your last name, and <SERVICE-INSTANCE-NAME> with the TGF instance you created in the previous section
```
vi manifest.yaml
```
4. change **helloworld** to **helloworld-womack**, or whatever your last name is
5. change **/<SERVICE-INSTANCE-NAME/>** with **tgf-womack**, or whatever you named your service instance
6. Push the application
```
cf push
```


link:/README.md#course-materials[Course Materials home] | link:/session_03/lab_02/lab_02.adoc[Lab 2 - Binding to Cloud Foundry Services]
