# Kubernetes Service Account

## What is a Service Account in Kubernetes?

A Service Account in Kubernetes is an identity that pods can use to interact with the Kubernetes API. It provides a way for applications running in pods to authenticate and authorize themselves to perform actions within the cluster.

## Why is it Important?

Service Accounts are important for several reasons:
- **Security**: They provide a secure way for applications to interact with the Kubernetes API without using user credentials.
- **Granular Access Control**: Service Accounts can be assigned specific roles and permissions, allowing fine-grained control over what actions a pod can perform.
- **Isolation**: Different applications or components can use different Service Accounts, ensuring that they only have access to the resources they need.

## Default Service Account

If a user does not specify a Service Account for a pod, Kubernetes automatically assigns the default Service Account in the namespace. This default Service Account has limited permissions and is intended for general use. However, for more secure and controlled access, it is recommended to create and use custom Service Accounts with appropriate roles and permissions.

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: example-pod
spec:
    serviceAccountName: custom-service-account
    containers:
    - name: example-container
        image: example-image
```

In the above example, the `serviceAccountName` field specifies the Service Account to be used by the pod. If this field is omitted, the default Service Account in the namespace will be used.