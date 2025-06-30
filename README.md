# How to manage at scale EKS Pod Identities when deploying with ArgoCD and AWS Controllers for Kubernetes (ACK)

This repository contains sample code for implementing GitOps with Argo CD and AWS Controllers for Kubernetes (ACK) on Amazon EKS, including a validation mechanism for the EKS Pod Identity Association eventually consistent api. This is for demonstration purposes only.

## Overview

This project demonstrates how to use Argo CD to manage AWS resources through AWS Controllers for Kubernetes (ACK), specifically showcasing EKS Pod Identity Association. It provides a practical example of implementing GitOps principles with AWS services.

## Architecture

The sample application includes:

- Argo CD Application definitions (template)
- Helm chart for deploying:
  - EKS Pod Identity Association (using ACK)
  - Service Account configuration
  - Sample deployment and job to validate AWS credential injection

## Prerequisites

- Amazon EKS cluster (v1.24+)
- Argo CD installed on your cluster
- AWS Controllers for Kubernetes (ACK) installed, specifically the EKS controller
- IAM role with appropriate permissions

## Getting Started

1. Clone this repository
2. Update the `application.yaml` or `application-with-job.yaml` with your specific values:
   - Update the `repoURL` to point to your Git repository
   - Set the appropriate `roleArn` for your IAM role
   - Configure the `clusterName` to match your EKS cluster

3. Apply the Argo CD application:
   ```bash
   kubectl apply -f application.yaml
   ```

## Configuration Options

The Helm chart supports the following values:

- `app`: Name of the application to be deployed
- `clusterName`: EKS cluster name
- `namespace`: Kubernetes namespace for deployment
- `roleArn`: IAM role ARN to be linked to the service account
- `jobWorkaround`: Enable/disable the validation job (set to "enabled" or "disabled")
- `image`: Container image for the validation job

## Validation

When `jobWorkaround` is set to "enabled", a job will run to validate that AWS credentials are properly injected into the pod environment.

## Related Resources

For more information, check out the AWS blog post: [How to manage at scale EKS Pod Identities when deploying with ArgoCD and AWS ACK](TBD)

## License

This library is licensed under the MIT-0 License. See the LICENSE file.
