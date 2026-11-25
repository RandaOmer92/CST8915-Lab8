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
