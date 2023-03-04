# thinkon-take-home
Kubernetes Deployment for Users and Shifts APIs

This repository contains Kubernetes resources (yaml) for deploying two containers that scale independently from one another. One container runs code that runs a small API that returns users from a database hosted in the cluster, while the other container runs code that runs a small API that returns shifts from a database hosted in the cluster.

Overview

Each deployment file consists of an application and a database. The containers are deployed as Kubernetes Deployments with a minimum of two replicas. The number of replica is automatically scaled up or down based on the average CPU utilization or network latency across all pods in the deployment.

Deployment Steps

Create Namespace for Prod and staging kubectl create -n prod / kubectl create -n staging

Create ConfigMaps for storing the database connection information for the users and shifts APIs in both staging and prod environments



Create two Kubernetes Secrets for storing the database credentials for the users and shifts APIs:

Create Kubernetes Deployments for the users and shifts APIs:

Create a Kubernetes Service for the users and shifts APIs:

Deploy a metric server to collect and aggregate performance metrics from the cluster

Create a Kubernetes HorizontalPodAutoscaler for each deployment to automatically scale the number of replicas based on CPU utilization or network latency:

Verify that the deployments, services, and horizontal pod autoscalers have been created and are running:

kubectl get deploy / kubectl get svc / kubectl get hpa

IAM Controls

To prevent the development team from running certain commands on the Kubernetes cluster, we can create a Kubernetes  Group with a list of our developer team, Kubernetes RBAC Role object that allows the developers team to perform only certain actions on pods and deployments, such as creating, updating, and deleting them, as well as rolling back deployments. The RBAC Role object can then be bound to the group with a Kubernetes RoleBinding object that specifies which groups should have this role:

Create users and groups and setup certs based authentication
Create service accounts for applications
Create Roles and ClusterRoles to define authorizations
Map Roles and ClusterRoles to group and service accounts using RoleBingings and ClusterRoleBindings

Use helm to configure Prometheus for monitoring the cluster and grafana for visualisation
Configure prometheus to scrap latency metric from application.
apply prometheusRule object that defines a recording rule for the latency metric you want to use for scaling


Use helm to deploy EFK for log management and data analytics

Use Helm Charts to deploy Nginx-ingress to expose our application externally.
Use ingress.yml for routing rules: Host based / Pathbased


