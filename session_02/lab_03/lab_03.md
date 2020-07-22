![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
*TMC Workshop demonstrating caching and session offloading*

### Lab 3 - Session-State Caching
* For full instructions on how this application is built, including the `request.getSession().setAttribute()` method required to make this work, visit the following link: 

https://docs.pivotal.io/cloud-cache-dev/spring-boot/guides/session-state

#### Build Application
1. In your terminal window, switch to the following directory:
```
 cd ../session-state
```
2. Build the application using gradlew
```
./gradlew build
```
3. Edit the manifest file, adding your lastname to the app name, and <SERVICE-INSTANCE-NAME> with the TGF instance you created in the previous section
```
vi manifest.yaml
```
4. change **session-state-womack** to **session-state- whatever your last name is
5. change `tgf-womack` to **tgf- whatever you named your service instance
6. Push the application
```
cf push
```

#### Verify Application
The TAS output will show where the application is running, for example `https://session-state-womack.apps.fowler.cf-app.com`. As you add items to your list, you'll see that they're cached in your session, so if you open a new browser window/tab, they're still there. But if you destroy that session, or open with a different browswer, you start a new session.

#### Move on to next lab

[Home](../../README.md)
