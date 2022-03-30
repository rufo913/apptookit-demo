# Tanzu Community Edition Application Toolkit Sample Workload

This project is a simple spring boot web application. It was created by
visiting start.spring.io, choosing the Spring Web framework, and adding the
HelloController.

## Prerequisites

Installed Tanzu Community Edition Application Toolkit and its dependencies.

## Deploying Workload

Use the Tanzu CLI to create the Workload from the workload.yaml file. Assumes

```
tanzu apps workload create -f workload.yaml --yes
```

Watch kpack find the correct buildpack and build the workload. Look for the
"Build successful" message when complete.

```
tanzu apps workload tail tanzu-simple-web-app
```

In a short time Knative will host the workload. Check for it to be READY:

'kubectl get service.serving.knative.dev/tanzu-simple-web-app'


## Testing the workload

The workload should end up deployed on knative. 

Test the workload:

```
curl http://tanzu-simple-web-app.default.127-0-0-1.sslip.io 
```

## Revising the workload

For this test, you will need to put the sample workload code in your own git repo. Change
workload.yaml spec.source.git.url appropriately. Delete and recreate the workload.

Change the workload code. For example, 
open `src/main/java/com/example/demo/HelloController.java` and change the message.
Don't forget to change `src/text/java/com/example/demo/HelloControllerTest.java` if
you want your tests to pass!

Push your changes to git. Wait a minute or so - source controller has been watching git
and will rebuild the application. Watch for the knative service to increment the LATESTREADY
field.

curl the app again and see your new message.

