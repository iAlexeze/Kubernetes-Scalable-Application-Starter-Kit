# Kubernetes Scalable Application Starter Kit

Welcome to the Kubernetes Scalable Application Starter Kit repository! This repository provides a comprehensive set of files and configurations to help you quickly deploy and manage scalable applications on Kubernetes. Whether you're a developer, system administrator, or someone interested in building robust application infrastructures, this starter kit is your gateway to success.

## Table of Contents

- [Introduction](#introduction)
- [Getting Started](#getting-started)
- [Cluster Configuration](#cluster-configuration)
- [MetalLB](#metallb)
- [Metrics](#metrics)
- [Dashboard](#dashboard)
- [Pod Configuration](#pod-configuration)
- [ReplicaSet](#replicaset)
- [Deployment](#deployment)
- [Horizontal Pod Autoscaler](#horizontal-pod-autoscaler)
- [Contributing](#contributing)
- [License](#license)

## Introduction<a name="introduction"></a>

The Kubernetes Scalable Application Starter Kit provides a solid foundation for building and deploying scalable applications on Kubernetes. It includes essential configuration files and deployment templates that adhere to best practices, enabling you to leverage Kubernetes' power and flexibility.

## Getting Started<a name="getting-started"></a>

To get started with this starter kit, follow these steps:

1. Clone the repository to your local machine:
        
        git clone https://github.com/your-username/kubernetes-scalable-app-starter-kit.git


2. Ensure that you have a Kubernetes cluster up and running. If you don't have a cluster, you can create one using [Kind](https://kind.sigs.k8s.io/). I have provided a configuration to setup a multi-node [Kind Kubernetes Cluster](#cluster-configuration).

3. Navigate to the cloned repository:

        cd kubernetes-scalable-app-starter-kit


4. Modify the configuration files in the respective directories to suit your application requirements.

5. Deploy the components using the provided deployment files and commands. For example, to deploy the NGINX application, run:
        
        kubectl apply -f deployment/nginx_deploy.yml


## Cluster Configuration<a name="cluster-configuration"></a>

The `cluster` directory contains the `cluster-config.yaml` file, which holds the configuration for your Kubernetes cluster. Modify this file to define the desired state of your cluster, including settings such as network policies, authentication, and RBAC.

To create your cluster, run:

        kind create cluster --name=<cluster-name> --config=<path/to/config.yaml>

In this case, run:

        kind create cluster --name=my-cluster --config=cluster/config.yaml>

This will create your multi-node Kubernetes cluster named `my-cluster`, with `1 control-plane` and `2 worker nodes`.

To confirm the availability and readiness of the nodes, run:

        kubectl get nodes

The output should look like this:

        NAME                       STATUS   ROLES           AGE   VERSION
        my-cluster-control-plane   Ready    control-plane   31d   v1.26.3
        my-cluster                 Ready    <none>          31d   v1.26.3
        my-cluster2                Ready    <none>          31d   v1.26.3


<p align="center">
  <strong><em style="text-align:center;">ENJOY 😃</em></strong>
  <br>
</p>


## MetalLB<a name="metallb"></a>

The `metallb` directory provides two essential files: `config.yml` and `metallb-native.yaml`. MetalLB is a load balancer implementation for Kubernetes, designed to enable bare metal services. The `config.yml` file allows you to configure MetalLB, while the `metallb-native.yaml` file provides an example of how to deploy MetalLB in your cluster.

To deploy MetalLB in your cluster, run:

       kubectl apply -f metallb/metallb-native.yaml

## Metrics<a name="metrics"></a>

The `metrics` directory contains the `components.yaml` file, which sets up the necessary components for collecting and exporting metrics from your cluster. These metrics can be visualized and analyzed using various monitoring solutions, allowing you to gain insights into the performance and health of your applications.

To deploy the metrics components, run:

       kubectl apply -f metrics/components.yaml

## Dashboard<a name="dashboard"></a>

The `dashboard` directory contains the `dash.yml` file, which allows you to deploy the Kubernetes Dashboard. The Dashboard provides a web-based user interface to monitor and manage your cluster. Once deployed, you can access the Dashboard and gain insights into your cluster's health and performance.

### *Follow these steps to setup your dashboard*


**STEP I** - To deploy the Kubernetes Dashboard, run:

        kubectl apply -f dashboard/dash.yml

This will create a `Kubernetes-dahboard namespace`, `admin-user` serviceaccount with cluster-admin privilege, as well as other necessary objects.


**STEP II** - To generate login token, run:

        kubectl token create admin-user -n kubernetes-dashboard

You can also specify the desired duration of the token with the `duration` flag. To do this, run:

        kubectl token create admin-user -n kubernetes-dashboard --duration 60m

This will keep the login token active for `60minutes`


**STEP III** - To expose the Kubernetes Dashboard to external access, run:

        kubectl proxy &


**STEP IV** - To access the Kubernetes Dashboard, copy and paste this url on your favorite browser:

        http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/workloads?namespace=_all


<p align="center">
  <strong style="text-align:center;"> Congratulations!!! You have setup your Kubernetes Dashboard successfully</strong>
  <br>
  <strong><em style="text-align:center;">😃😃  ENJOY THE BEAUTIFUL VIEW   😃😃</em></strong>
  <br>
</p>


## Pod Configuration<a name="pod-configuration"></a>

The `pod` directory holds example pod configuration files, such as `nginx_pod.yml`, which demonstrate how to define and deploy individual pods on Kubernetes. You can modify these files to create pods for your specific application components and customize them according to your requirements.

To deploy a pod, run:

       kubectl apply -f pod/nginx_pod.yml

This will create a pod and its Loadbalancer service for external access.

## ReplicaSet<a name="replicaset"></a>

The `replicaset` directory provides example ReplicaSet files, such as `nginx_rs.yml`, which showcase the usage of ReplicaSets in Kubernetes. ReplicaSets ensure that a specified number of pod replicas are running at any given time, allowing you to maintain high availability and scalability for your application.

To deploy a ReplicaSet, run:

       kubectl apply -f replicaset/nginx_rs.yml

This will create a replicaset, corresponding number of specified pods, and its Loadbalancer service for external access.

## Deployment<a name="deployment"></a>

The `deployment` directory contains example deployment files, such as `nginx_deploy.yml`, which demonstrate how to deploy applications on Kubernetes. Modify these files to define your application's deployment strategy, including the number of replicas, resource limits, and networking settings.

To deploy the NGINX application, run:

        kubectl apply -f deployment/nginx_deploy.yml

This will create a Deployment object, a replicaset, corresponding number of specified pods, and its Loadbalancer service for external access.

## Horizontal Pod Autoscaler<a name="horizontal-pod-autoscaler"></a>

The `hpa` directory contains two important files: `hpa_config.yaml` and `load_generator.sh`. The `hpa_config.yaml` file defines the autoscaling behavior for your application based on CPU utilization or other metrics. The `load_generator.sh` script helps simulate load on your application, allowing you to observe the autoscaling in action.

To deploy the Horizontal Pod Autoscaler, run:

        kubectl apply -f hpa/hpa_config.yaml
        ./load_generator.sh
        


You can also configure the Horizontal Pod Autoscaler, by modifying the `hpa_config.yaml` file according to your requirements.

## Contributing<a name="contributing"></a>

Contributions are welcome! If you have any ideas, suggestions, or improvements for this starter kit, please feel free to open issues or submit pull requests.

## License<a name="license"></a>

This project is licensed under the [MIT License](license).

Let's Connect,
- <a href="https://github.com/ialexeze" target="_blank">GitHub</a>
- <a href="https://linkedin.com/in/alexeze" target="_blank">LinkedIn</a>
- <a href="https://twitter.com/ialexeze" target="_blank">Twitter</a>