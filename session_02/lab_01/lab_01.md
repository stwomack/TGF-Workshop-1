![VMware Tanzu Gemfire](/images/vmware-tanzu.png)
# TGF-Workshop-1
TMC Workshop demonstrating caching and session offloading

= Lab 1 - Building and Pushing Your First Application

== Target

. If you haven't already, download the latest release of the PCF CLI for your operating system and install it.

. Use the API target and username/password provided by the instructor..
+
. Login to Pivotal Cloud Foundry (sso):
+
----
cf login -a https://api.sys.cloud-02.pcf.ascension.org --sso
----
+
Follow the prompts, choosing default organization and space.

== Create Application

. Go to http://start.spring.io/ in your browser
. Change the 'Group' field to 'com.workshop' .
. Change the artifact from demo to orders-service
. Add the following dependencies individually:
+
----
Spring Data JPA
Rest Repositories
MySQL
GCP Support
H2 Database
Spring Boot Actuator
Spring Security
Lombok
----
. Click 'Generate Project', and save the .zip file to this directory `$COURSE_HOME/session_03/lab_01` ($COURSE_HOME is a pointer to where you cloned this repo )
. Unzip the project
. Delete the .zip file
. Copy ( or move ) the `manifest.yml` file from this directory into the newly extracted project directory
. ```- name: orders-service-${initials}``` should be changed to reflect your actual initials. Otherwise everyone will clash
. For the following steps, use your favorite IDE or file editor
. Add the following properties to the file `src/main/resources/application.properties`
+
```
security.basic.enabled=false
management.security.enabled=false
spring.jpa.hibernate.ddl-auto=create
spring.jpa.database-platform=org.hibernate.dialect.MySQL55Dialect
management.endpoint.health.show-details=always
management.endpoints.web.exposure.include=*
```
. Create a class, `OrderItem.java`, in `src/main/java/com/workshop/ordersservice`, and paste in the following contents:
+
```
package com.workshop.ordersservice;

import lombok.Data;
import lombok.NoArgsConstructor;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;

@Entity
@Data
@NoArgsConstructor()
public class OrderItem {
    @Id
    @GeneratedValue
    private Long id;
    private String orderNumber;
    private String customerName;

    public OrderItem(String orderNumber, String customerName) {
        this.orderNumber = orderNumber;
        this.customerName = customerName;
    }
}


```
+
Note that project Lombok takes care of boilerplate code like getters & setters
. Finally, replace the contents of `/src/main/java/com/workshop/ordersservice/OrderServiceApplication.java` with the following
```
package com.workshop.ordersservice;

import org.springframework.beans.factory.annotation.Value;
import org.springframework.boot.CommandLineRunner;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.EnableAutoConfiguration;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.data.repository.PagingAndSortingRepository;
import org.springframework.data.repository.query.Param;
import org.springframework.data.rest.core.annotation.RepositoryRestResource;
import org.springframework.data.rest.core.annotation.RestResource;
import org.springframework.security.config.annotation.web.builders.WebSecurity;
import org.springframework.security.config.annotation.web.configuration.WebSecurityConfigurerAdapter;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.Collection;
import java.util.stream.Stream;

@RepositoryRestResource
interface OrderRepository extends PagingAndSortingRepository<OrderItem, Long> {

    @RestResource(path = "by-name")
    Collection<OrderItem> findByCustomerName(@Param("customerName") String customerName);
}

@SpringBootApplication
@EnableAutoConfiguration
public class OrdersServiceApplication {

    public static void main(String[] args) {
        SpringApplication.run(OrdersServiceApplication.class, args);
    }

    @Bean
    CommandLineRunner commandLineRunner(OrderRepository orderRepository) {
        return args -> {
            Stream.of("47774", "77333", "99333", "27772")
                    .forEach(orderNumber -> orderRepository.save(new OrderItem(orderNumber, "Customer1")));
            orderRepository.findAll().forEach(System.out::println);
        };
    }
    
    @Configuration
    public class ApplicationSecurity extends WebSecurityConfigurerAdapter {

        @Override
        public void configure(WebSecurity web) {
            web.ignoring().antMatchers("/**");
        }
    }
}
```


== Build and Push!

. You should still be in the _Orders Service_ application directory:
+
----
cd $COURSE_HOME/session_03/lab_01/orders-service
----

. Using Maven, build and package the application (note, windows users will use ./mvnw.bat :
+
----
./mvnw install
----

. Push the application!
+
----
cf push
----
+
You should see output similar to the following listing. Take a look at the listing callouts for a play-by-play of what's happening:
+
====
----
➜  orders-service git:(master) ✗ cf push
Using manifest file /Users/swomack/workspace-workshops/cloud-native-spring-workshop/session_03/lab_01/orders-service/manifest.yml

Creating app orders-service-brideless-subhero in org myorg / space Workshop as swomack@pivotal.io...
OK

Creating route orders-service-anachronous-glycoprotein.cfapps.io...
OK

Binding orders-service-anachronous-glycoprotein.cfapps.io to orders-service-brideless-subhero...
OK

Uploading orders-service-brideless-subhero...
Uploading app files from: /var/folders/gx/chs6597d31n1v5ns2r6954040000gn/T/unzipped-app422178702
Uploading 461K, 95 files
Done uploading
OK

Starting app orders-service-brideless-subhero in org myorg / space Workshop as swomack@pivotal.io...
Downloading binary_buildpack...
Downloading nodejs_buildpack...
Downloading go_buildpack...
Downloading dotnet_core_buildpack...
Downloading python_buildpack...
Downloaded dotnet_core_buildpack
Downloading php_buildpack...
Downloaded nodejs_buildpack
Downloading dotnet_core_buildpack_beta...
Downloading java_buildpack...
Downloaded python_buildpack
Downloaded dotnet_core_buildpack_beta
Downloading staticfile_buildpack...
Downloaded php_buildpack
Downloading ruby_buildpack...
Downloaded go_buildpack
Downloaded binary_buildpack
Downloaded ruby_buildpack
Downloaded staticfile_buildpack
Downloaded java_buildpack
Creating container
Successfully created container
Downloading app package...
Downloaded app package (25.6M)
-----> Java Buildpack Version: v3.14 (offline) | https://github.com/cloudfoundry/java-buildpack.git#d5d58c6
-----> Downloading Open Jdk JRE 1.8.0_121 from https://java-buildpack.cloudfoundry.org/openjdk/trusty/x86_64/openjdk-1.8.0_121.tar.gz (found in cache)
       Expanding Open Jdk JRE to .java-buildpack/open_jdk_jre (1.2s)
-----> Downloading Open JDK Like Memory Calculator 2.0.2_RELEASE from https://java-buildpack.cloudfoundry.org/memory-calculator/trusty/x86_64/memory-calculator-2.0.2_RELEASE.tar.gz (found in cache)
       Memory Settings: -XX:MaxMetaspaceSize=104857K -Xms681574K -XX:MetaspaceSize=104857K -Xss349K -Xmx681574K
-----> Downloading Container Certificate Trust Store 2.0.0_RELEASE from https://java-buildpack.cloudfoundry.org/container-certificate-trust-store/container-certificate-trust-store-2.0.0_RELEASE.jar (found in cache)
       Adding certificates to .java-buildpack/container_certificate_trust_store/truststore.jks (0.4s)
-----> Downloading Spring Auto Reconfiguration 1.10.0_RELEASE from https://java-buildpack.cloudfoundry.org/auto-reconfiguration/auto-reconfiguration-1.10.0_RELEASE.jar (found in cache)
Exit status 0
Uploading droplet, build artifacts cache...
Uploading build artifacts cache...
Uploading droplet...
Uploaded build artifacts cache (109B)
Uploaded droplet (71M)
Uploading complete
Destroying container
Successfully destroyed container

0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting
0 of 1 instances running, 1 starting

1 of 1 instances running

App started


OK

App orders-service-brideless-subhero was started using this command `CALCULATED_MEMORY=$($PWD/.java-buildpack/open_jdk_jre/bin/java-buildpack-memory-calculator-2.0.2_RELEASE -memorySizes=metaspace:64m..,stack:228k.. -memoryWeights=heap:65,metaspace:10,native:15,stack:10 -memoryInitials=heap:100%,metaspace:100% -stackThreads=300 -totMemory=$MEMORY_LIMIT) && JAVA_OPTS="-Djava.io.tmpdir=$TMPDIR -XX:OnOutOfMemoryError=$PWD/.java-buildpack/open_jdk_jre/bin/killjava.sh $CALCULATED_MEMORY -Djavax.net.ssl.trustStore=$PWD/.java-buildpack/container_certificate_trust_store/truststore.jks -Djavax.net.ssl.trustStorePassword=java-buildpack-trust-store-password" && SERVER_PORT=$PORT eval exec $PWD/.java-buildpack/open_jdk_jre/bin/java $JAVA_OPTS -cp $PWD/. org.springframework.boot.loader.JarLauncher`

Showing health and status for app orders-service-brideless-subhero in org Express-Scripts / space Workshop as swomack@pivotal.io...
OK

requested state: started
instances: 1/1
usage: 512M x 1 instances
urls: orders-service-anachronous-glycoprotein.cfapps.io
last uploaded: Wed Mar 15 18:09:48 UTC 2017
stack: cflinuxfs2
buildpack: container-certificate-trust-store=2.0.0_RELEASE java-buildpack=v3.14-offline-https://github.com/cloudfoundry/java-buildpack.git#d5d58c6 java-main open-jdk-like-jre=1.8.0_121 open-jdk-like-memory-calculator=2.0.2_RELEASE spring-auto-reconfiguration=1.10...

     state     since                    cpu      memory         disk         details
#0   running   2017-03-15 01:10:53 PM   103.0%   329M of 512M   152M of 1G
➜  orders-service git:(master) ✗

----
<1> The CLI is using a manifest to provide necessary configuration details such as application name, memory to be allocated, and path to the application artifact.
Take a look at `manifest.yml` to see how.
<2> In most cases, the CLI indicates each Cloud Foundry API call as it happens.
In this case, the CLI has created an application record for _Orders Service_ in your assigned space.
<3> All HTTP/HTTPS requests to applications will flow through Cloud Foundry's front-end router called http://docs.cloudfoundry.org/concepts/architecture/router.html[(Go)Router].
Here the CLI is creating a route with random word tokens inserted (again, see `manifest.yml` for a hint!) to prevent route collisions across the default Cloud Foundry domain.
<4> Now the CLI is _binding_ the created route to the application.
Routes can actually be bound to multiple applications to support techniques such as http://www.mattstine.com/2013/07/10/blue-green-deployments-on-cloudfoundry[blue-green deployments].
<5> The CLI finally uploads the application bits to Cloud Foundry. Notice that it's uploading _90 files_! This is because Cloud Foundry actually explodes a ZIP artifact before uploading it for caching purposes.
<6> Now we begin the staging process. The https://github.com/cloudfoundry/java-buildpack[Java Buildpack] is responsible for assembling the runtime components necessary to run the application.
<7> Here we see the version of the JRE that has been chosen and installed.
<8> And here we see the version of Tomcat that has been chosen and installed.
<9> The complete package of your application and all of its necessary runtime components is called a _droplet_.
Here the droplet is being uploaded to Cloud Foundry's internal blobstore so that it can be easily copied to one or more _https://docs.cloudfoundry.org/concepts/diego/diego-architecture.html#cell-components[Diego Cells]_ for execution.
<10> The CLI tells you exactly what command and argument set was used to start your application.
<11> Finally the CLI reports the current status of your application's health.
You can get the same output at any time by typing `cf app orders-service-brideless-subhero`. Note that your random-word will be different
====

. Visit the application in your browser by hitting the route that was generated by the CLI.
+
In the example `cf push` above, the `urls:` section of the application health reports `orders-service-brideless-subhero.cfapps.io`, so http://orders-service-brideless-subhero.cfapps.io would have been used to examine this example deployed application. But use the url from your application deployment health report.

. We've just built out the most simple of RESTful APIs, with hypermedia support included. 

. View the `/orderItems` endpoint of your application to see what has already been added in the database

Because our application knows nothing about any backing databases, and h2 is on the classpath, h2's in memory database will be used when this application starts up. Look at the `/actuator/health` actuator endpoint of your application to see that there's no backing database reported. In the next lab, we'll bind a backing database
```
{"status":"UP","details":{"diskSpace":{"status":"UP","details":{"total":1073741824,"free":904355840,"threshold":10485760}},
"db":{"status":"UP","details":{"database":"H2","hello":1}}}}
```

link:/README.md#course-materials[Course Materials home] | link:/session_03/lab_02/lab_02.adoc[Lab 2 - Binding to Cloud Foundry Services]
