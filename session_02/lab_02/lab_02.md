![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

### Lab 2 - Look-Aside Caching
* For full instructions on how this application is built, including the `@Cacheable` annotion required to make this work, visit the following link: 

https://docs.pivotal.io/cloud-cache-dev/spring-boot/basic-cache

#### Build Application
1. In your terminal window, switch to the following directory:
```
 cd ../look-aside-cache
```
2. Build the application using gradlew
```
./gradlew build
```
3. Edit the manifest file, adding your lastname to the app name, and <SERVICE-INSTANCE-NAME> with the TGF instance you created in the previous section
```
vi manifest.yaml
```
4. change **bikeincidents** to **bikeincidents-womack**, or whatever your last name is
5. change ``<SERVICE-INSTANCE-NAME>`` to **tgf-womack**, or whatever you named your service instance
6. Push the application
```
cf push
```

#### Verify Application
The TAS output will show where the application is running, for example `https://bikeincidents-womack.apps.fowler.cf-app.com`. You'll notice that the first time you hit the url and search using a zip code, it takes a bit of time, but once the incident-api data has been cached in TGF, further refreshes will show dramatically increased performance.

#### Move on to next lab

[Lab 3 - Session State Caching](../lab_03/lab_03.md)
