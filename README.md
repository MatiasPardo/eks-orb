# eks-orb
Orb for installing the tools to interact with Amazon Elastic Container Service for Kubernetes (EKS) from within a
CircleCI build job.

## View in the orb registry
See the [eks-orb in the registry](https://circleci.com/orbs/registry/orb/tiendanube/eks)
for more the full details of jobs, commands, and executors available in this
orb.

## Setup required to use this orb
The following **required** dependencies must be configured in CircleCI in order to use this orb:

* AWS_ACCESS_KEY_ID - environment variable for AWS login
* AWS_SECRET_ACCESS_KEY - environment variable for AWS login

For more information on how to properly set up environment variables on CircleCI, read the docs:
[environment-variable-in-a-project](https://circleci.com/docs/2.0/env-vars/#setting-an-environment-variable-in-a-project)

## Sample use in CircleCI config.yml

```yaml
version: 2.1
orbs:
  eks: tiendanube/eks@1.0.0
workflows:
  deploy:
    jobs:
      - eks/deploy:
          cluster_name: cluster_name
          region: region
          steps:
            - run:
                command: |
                  kubectl apply -f bundle.yml
                  kubectl apply -f deployment.yml
```

```yaml
version: 2.1
orbs:
  eks: tiendanube/eks@1.0.0
workflows:
  deploy:
    jobs:
      - eks/helm-deploy:
          cluster_name: cluster-region
          region: aws-region
          release-name: release-name
          values-file: values.yaml
          namespace: default
          chart: stable/chart
          image-tag: ${CIRCLE_SHA1:0:7}
```
