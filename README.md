# Cloud Developer

* [Credentials](#credentials)
* [Docker](#docker)
* [Kubernetes](#kubernetes)
* [Travis](#travis)


## credentials
First, you need to configure your variables in the next three files on the `deployments/k8s` directory:

- env-secret.yaml
- aws-secret.yaml
- env-configmap.yaml

## docker
To test the application in local with docker, you need to run the next commands:

```bash
docker-compose -f docker-compose-build.yaml build
docker-compose up
```

This will build the necessary images and then it will mount the application in local. You need to define the next variables in local, in order to run it correctly:

- POSTGRESS_USERNAME
- POSTGRESS_PASSWORD
- POSTGRESS_DB
- POSTGRESS_HOST
- AWS_REGION
- AWS_PROFILE
- AWS_BUCKET
- JWT_SECRET

Also, You can get the images from my docker hub account:

- https://hub.docker.com/repository/docker/guetteluis/reverseproxy
- https://hub.docker.com/repository/docker/guetteluis/udagram-frontend
- https://hub.docker.com/repository/docker/guetteluis/udagram-user
- https://hub.docker.com/repository/docker/guetteluis/udagram-feed


## kubernetes
To get kubernetes cluster working, first you need to configure the cluster on AWS, I used AWS EKS, then, you need to run the next command:
- aws eks --region <YOUR_REGION> update-kubeconfig --name <CLUSTER_NAME>
- kubectl get nodes

You can find some issues when tryin to authenticate to aws, so first remember to run:

- `aws configure`
- `aws sts get-caller-identity`
- And run again the previous steps

Once you have connected to kubernetes cluster, you need to appy the configurations in the `/deployments/k8s/` directory for all the deployments and services (remember to run first frontend, feed and user, before running reverseproxy):

- kubectl apply -f <service-file-names>
- kubectl apply -f <deployment-file-names>
- kubectl get pods
- kubectl get svc
- kubectl get deployments

## travis
In the root directory of the github repository, there is a `.travis.yml` that build all the containers and test that is working as expected.


