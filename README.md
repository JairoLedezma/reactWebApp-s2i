# reactWebApp-s2i

 
## Step 1 - Create a new namespace  
``` 
$ oc new-project react-s2i 
```


## Step 2 - Create a new project 
``` 
$ oc new-app nodeshift/ubi8-s2i-web-app:latest~https://github.com/lholmquist/react-web-app

example output:

--> Found container image 7118b10 (3 months old) from Docker Hub for "nodeshift/ubi8-s2i-web-app:latest"

    Node.js 14 
    ---------- 
    Web Application building with Node.js

    Tags: builder, nodejs

    * An image stream tag will be created as "ubi8-s2i-web-app:latest" that will track the source image
    * A source build using source code from https://github.com/lholmquist/react-web-app will be created
      * The resulting image will be pushed to image stream tag "react-web-app:latest"
      * Every time "ubi8-s2i-web-app:latest" changes a new build will be triggered

--> Creating resources ...
    imagestream.image.openshift.io "ubi8-s2i-web-app" created
    imagestream.image.openshift.io "react-web-app" created
    buildconfig.build.openshift.io "react-web-app" created
    deployment.apps "react-web-app" created
    service "react-web-app" created
--> Success
    Build scheduled, use 'oc logs -f buildconfig/react-web-app' to track its progress.
    Application is not exposed. You can expose services to the outside world by executing one or more of the commands below:
     'oc expose service/react-web-app' 
    Run 'oc status' to view your app.
```  


## step 3 - Check to see if your application is running
```
$ oc get pods

example output:

NAME                             READY   STATUS      RESTARTS   AGE
react-web-app-1-build            0/1     Completed   0          2m40s
react-web-app-59f95fc7cf-9gjj9   1/1     Running     0          88s
```

## step 4 - Get the service and then expose it
```
$ oc get svc
NAME            TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
react-web-app   ClusterIP   172.30.105.244   <none>        8080/TCP   2m45s


$ oc expose svc/react-web-app

route.route.openshift.io/react-web-app exposed
```

## step 5 - Check to see if your application is running
```

$ oc get route

NAME            HOST/PORT                                              PATH   SERVICES        PORT       TERMINATION   WILDCARD
react-web-app   react-web-app-react-s2i.apps.pfocp4.nvsconsulting.io          react-web-app   8080-tcp                 None

```


