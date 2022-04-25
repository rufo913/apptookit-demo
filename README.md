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

## Create apps based on your own Git Repo

1. Fork the repo or create your git repo with the source code. 
2. Update the `workload.yaml` with the corresponding git URL
3. Run `tanzu apps workload create` using the updated `workload.yaml` 

## Updating your workload

1. Compile and run your source code
`./mvnw spring-boot:run`

2. Once the changes are complete, push your changes to git repo. 
3. Wait a minute or so - source controller has been watching git and will rebuild the application. 
4. Watch for the knative service to increment the LATESTREADY
field.

5. curl the app again and see your new message.
