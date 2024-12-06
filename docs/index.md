# SubQuery Network Node Operators Deployment Guide

This tutorial provides a step-by-step guide to deploy SubQuery Network Node Operators using Alibaba Cloud Compute Nest and ECS. 

## Introduction

## Prerequisites
Before starting, ensure you have:

An active Alibaba Cloud account.
Familiarity with cloud services.

## Step 1: Alibaba Cloud Account Setup
If you haven't already, sign up for an Alibaba Cloud account: Sign up (https://www.alibabacloud.com).

## Step 2: Access Compute Nest
Navigate to Compute Nest and locate the service for SubQuery Network Node Operators

## Step 3: Set Up an Instance and Its Parameters
Configure the necessary parameters for the instance

Service Instance Name: Provide a meaningful name for the instance.
Instance Password: Create a secure password for the instance.

## Step 4: Deploy Your Service
Review all configurations and accept the Terms of Service. Click Create Now to deploy your service.

## Step 5: What to do after creating the ECS instance

### 1. Log in to the server

The node operator services are already configured to start automatically along with the server. You can log in to the server with the following command:

```shell
ssh username@ip_address -L 8000:localhost:8000
```

And then you can access the subquery node operator coordinator by opening a browser and going to `http://localhost:8000`.

### 2. Register new node operator

On the coordinator page, you can register as a new node operator by following the instructions and start to behave as a node operator.

> Refer to the [Register in the Node Operator Admin App](https://academy.subquery.network/subquery_network/node_operators/setup/becoming-a-node-operator.html#_3-register-in-the-node-operator-admin-app) and the steps after that for more information.

## What to consider in docker-compose.yml [v2]

The `/home/subquery-indexer/docker-compose.yml` file is pre-configured for immediate use. However, you may need to adjust some settings like secret key, network endpoint, and other configurations.

> Refer to the [Port configurations](https://academy.subquery.network/subquery_network/node_operators/setup/becoming-a-node-operator.html#port-configurations) and [Running Node Operator Services](https://academy.subquery.network/subquery_network/node_operators/setup/becoming-a-node-operator.html#running-node-operator-services) for more information.

## What to consider in docker-compose.yml [v1]

The `/home/subquery-indexer/docker-compose.yml` file is pre-configured for immediate use. However, you may need to adjust the following settings:

**Coordinator and Proxy Services:**

- `--secret-key`: Replace with a secure secret key. Ensure it is the same for both the coordinator and proxy services.
- `--network-endpoint`: Update to a higher rate-limited endpoint if necessary.

**Coordinator Service:**

- `ports:` Ensure the coordinator service is not exposed to the public network. This can be managed through Docker Compose configuration or firewall settings.

**Proxy Service:**

- `ports:` Ensure the proxy service is exposed to the public network. This requires configuration in both Docker Compose and firewall settings.
- SSL Support: Consider adding a reverse proxy service like Nginx to support SSL.

**Postgres Service:**

- `POSTGRES_PASSWORD`: Replace with a secure password. Ensure it matches the `--postgres-password` in the coordinator service.

Remember to restart the services after making any changes:

```shell
cd /home/subquery-indexer
docker compose up -d
```

## Conclusion
This tutorial has guided you through the comprehensive process of building a SubQuery Network Node Operators service using Alibaba Cloud Compute Nest and ECS. Following these steps will help you to quickly deploy SubQuery Network Node Operators services on Alibaba Cloud.
