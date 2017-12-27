
# Creating a S2I Tomcat builder image  

## Getting started  

#### Creating the application image
The application image combines the builder image with your applications source code, which is served using whatever application is installed via the *Dockerfile*, compiled using the *assemble* script, and run using the *run* script.
The following command will create the application image:
```
s2i build test/test-app s2i-tomcat s2i-tomcat-app
---> Building and installing application from source...
```

#### Running the application image
Running the application image is as simple as invoking the docker run command:
```
docker run -d -p 8080:8080 s2i-tomcat-app
```
The application, which consists of a simple static web page, should now be accessible at  [http://localhost:8080](http://localhost:8080).

#### How to use in a openshift cluster

##### 1. import s2i-tomcat image to openshift
```
oc import-image you repository host/s2i-tomcat:lastest -n openshift --confirm --insecure
```
##### 2. edit image stream ,add annotation tags 
```
oc edit is/tomcat-s2i -n openshift
```

```$yaml
tags:
    - annotations:
        tags: builder
```


