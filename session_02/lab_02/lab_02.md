![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

### Lab 2 - Look-Aside Caching

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
5. change ``<SERVICE-INSTANCE-NAME>`` to **tgf-womack**, or whatever you named your service instance
6. Push the application
```
cf push
```

#### Verify Application
The TAS output will show where the application is running, for example `https://helloworld-womack.apps.fowler.cf-app.com` . add /hello to the path to view the application. You'll notice that the first time you hit the url, it take a bit of time, but once the key/value are in TGF, further refreshes will show dramatically increased performance.

#### Move on to next lab

[Lab 2 - Session State Caching](../lab_03/lab_03.md)
