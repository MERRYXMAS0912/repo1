# Connect to EKS Cluster using AWS CLI and kubectl

## Step 1: Download and Install AWS CLI

Follow the instructions to download and install the AWS CLI from the [official AWS documentation](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html).

## Step 2: Configure AWS CLI

Configure the AWS CLI with your credentials:

```sh
aws configure
```

You will be prompted to enter your AWS Access Key ID, Secret Access Key, region, and output format.

## Step 3: Update kubeconfig with EKS Cluster

Use the following command to update your kubeconfig file with the EKS cluster:

```sh
aws eks --region <your-region> update-kubeconfig --name <your-cluster-name>
```

Replace `<your-region>` with the AWS region where your EKS cluster is located and `<your-cluster-name>` with the name of your EKS cluster.

## Step 4: Verify the Configuration

Verify that your kubeconfig file is correctly configured and you can connect to your EKS cluster by running:

```sh
kubectl get nodes
```

You should see a list of nodes in your EKS cluster.
