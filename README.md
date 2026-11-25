# Lab 8 - CST8915 Full-stack Cloud-native Development: Deploying and Managing the Algonquin Pet Store (On Steroids)

**Student Name**: Randa Omer

**Student ID**: 041079985

**Course**: CST8915 Full-stack Cloud-native Development

**Semester**: Fall 2026

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/xJTfSKhiFGI)

---

## Task 1: My Docker Images

I forked the 8 service repos, built a Docker image for each one, and pushed them to my Docker Hub account.

| Service | My Fork | My Docker Image |
| --- | --- | --- |
| `store-front` | [store-front-L8](https://github.com/RandaOmer92/store-front-L8) | [randaomer92/store-front:lab8](https://hub.docker.com/r/randaomer92/store-front) |
| `store-admin` | [store-admin-L8](https://github.com/RandaOmer92/store-admin-L8) | [randaomer92/store-admin:lab8](https://hub.docker.com/r/randaomer92/store-admin) |
| `order-service` | [order-service-L8](https://github.com/RandaOmer92/order-service-L8) | [randaomer92/order-service:lab8](https://hub.docker.com/r/randaomer92/order-service) |
| `product-service` | [product-service-L8](https://github.com/RandaOmer92/product-service-L8) | [randaomer92/product-service:lab8](https://hub.docker.com/r/randaomer92/product-service) |
| `makeline-service` | [makeline-service-L8](https://github.com/RandaOmer92/makeline-service-L8) | [randaomer92/makeline-service:lab8](https://hub.docker.com/r/randaomer92/makeline-service) |
| `ai-service` | [ai-service-L8](https://github.com/RandaOmer92/ai-service-L8) | [randaomer92/ai-service:lab8](https://hub.docker.com/r/randaomer92/ai-service) |
| `virtual-customer` | [virtual-customer-L8](https://github.com/RandaOmer92/virtual-customer-L8) | [randaomer92/virtual-customer:lab8](https://hub.docker.com/r/randaomer92/virtual-customer) |
| `virtual-worker` | [virtual-worker-L8](https://github.com/RandaOmer92/virtual-worker-L8) | [randaomer92/virtual-worker:lab8](https://hub.docker.com/r/randaomer92/virtual-worker) |

### Updated deployment files

- [`aps-all-in-one-Task1.yaml`](./aps-all-in-one-Task1.yaml): uses my images for the 6 app services.
- [`admin-tasks.yaml`](./admin-tasks.yaml): uses my images for the 2 simulators (virtual customer and virtual worker).

The `secrets.yaml` file with the OpenAI keys is **not** in this repo. It is listed in `.gitignore`.

---

## Task 2: Azure Managed Services

In this lab, we ran MongoDB and RabbitMQ ourselves, as StatefulSet pods in AKS. Azure has managed services that could replace them.

### 1. MongoDB → Azure Cosmos DB for MongoDB

**What it is:** A fully managed NoSQL database service. It runs MongoDB workloads in the cloud with minimal changes to the app code [1].

**Why it's a good fit:**
- It supports the MongoDB wire protocol, so existing MongoDB drivers and tools still work [1].
- Often, the only change is the connection string [1].
- In our app, `makeline-service` connects to MongoDB with one setting: `ORDER_DB_URI: "mongodb://mongodb:27017"`. We would change that to the Cosmos DB connection string.

**What problem it solves:**
- Azure handles the infrastructure, patching, scaling, and backups [1]. We don't have to run and look after the `mongodb-0` pod.
- Data is automatically spread out for performance and scale, with no manual sharding [1].
- Data can be placed in any Azure region for low-latency access and high availability [1].

### 2. RabbitMQ → Azure Service Bus

**What it is:** A fully managed message broker with message queues and publish-subscribe topics [2]. Queues store messages until the receiving app is ready to process them [2].

**Why it's a good fit:**
- It works the same way as our app: `order-service` puts orders in a queue, and `makeline-service` takes them out.
- The sender and receiver don't need to be online at the same time, and traffic spikes don't overload a service [2].
- Several consumers can read from one queue at the same time, and each message goes to only one of them [2]. This helps when we scale up.

**What problem it solves:**
- Messages are kept safe: once Service Bus accepts a message, it stores it durably in triple-redundant storage [2].
- Azure takes care of hardware failures, patching, logs and disk space, backups, and failing over to a reserve machine [2]. We don't have to run and look after the `rabbitmq-0` pod.

**Trade-off:** To switch from another broker, we need to create the queues again and change the client library and settings [2]. So `order-service` and `makeline-service` would need code changes.

---


