![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

### Lab 1 - Building and Pushing Your First Application

#### Target Tanzu Appliction Service Instance
1. If you haven't already, download the latest release of the PCF CLI for your operating system and install it.
2. Use the API target and username/password provided by the instructor..
3. Login to Tanzu Application Service:
```
cf api api.sys.fowler.cf-app.com --skip-ssl-validation
```
4. Follow the prompts, choosing default organization and space.

#### Create an instance of Tanzu Gemfire
1. Execute the following command, but substute your last name for *womack*
```
cf create-service p-cloudcache small tgf-womack
```
2. The service will take a while to provision, so take a break or help a neighbor who's stuck
3. If you'd like to watch the status of the service being provisioned, execute the following until it is complete. 
```
watch cf service tgf-womack
```
4. You'll know it's complete when you see the following:
```
Last Operation
Status: create succeeded
Message: Instance provisioning completed
```
5. When that is complete, move on to the following section

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

[Lab 2 - Look-Aside Caching](session_02/lab_02/lab_02.md)
