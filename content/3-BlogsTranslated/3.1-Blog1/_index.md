---
title: "Blog 1"
date: 2025-10-08
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
---

# How iFood Built a Platform to Run Hundreds of Machine Learning Models with Amazon SageMaker Inference

*By Daniel Vieira, Debora Fanin, Gopi Mudiyala, and Saurabh Trikande – April 8, 2025, in the Advanced section (300), Amazon SageMaker Data & AI Governance, Customer Solutions.*

---

## Introduction

Headquartered in São Paulo, Brazil, **iFood** is a privately held national company and a leader in food tech in Latin America, processing millions of orders every month. iFood stands out for its strategy of integrating advanced technology into its operations. With the support of **AWS**, iFood has developed a powerful **machine learning (ML)** inference infrastructure using services like **Amazon SageMaker** to create and deploy ML models efficiently. This collaboration has allowed iFood to not only optimize internal processes but also provide innovative solutions for its delivery partners and restaurants.

iFood's ML platform includes a set of tools, processes, and workflows developed with the following main objectives:
- Accelerating the development and training of AI/ML models, making them more reliable and easier to reproduce.
- Ensuring that the deployment of these models into production is reliable, scalable, and traceable.
- Enabling transparent, accessible, and standardized testing, monitoring, and evaluation of models in production.

![Blog Image 1 - 1](/images/3-BlogImage/blog1-1.png)
> *Figure 1. Overview — iFood and the application of AI/ML in their product system.*

---

## Goals and Approach

To achieve these goals, iFood leverages **SageMaker** to streamline model training and deployment. By integrating SageMaker features into iFood's infrastructure, key steps are automated — from creating training datasets, training models, deploying them into production, to continuously monitoring their performance.

This article outlines how iFood uses SageMaker to enhance the entire ML lifecycle — from training to inference — and describes architectural changes and capabilities developed by the team.

---

## AI Inference at iFood

iFood leverages its AI/ML platform to enhance customer experience across various touchpoints. Some typical use cases include:

- **Personalized Recommendations** — Models analyze order history, preferences, and context to suggest appropriate restaurants and dishes, increasing customer satisfaction and order volume.
- **Smart Order Tracking** — The system predicts delivery times in real-time by combining traffic data, restaurant preparation times, and the location of the delivery driver, proactively notifying customers.
- **Automated Customer Service** — AI chatbots handle thousands of common requests daily, providing fast responses and retrieving relevant data to support personalization.
- **Grocery Shopping Support** — The app integrates language models that help customers create shopping lists from voice or text requests.

Thanks to these initiatives, iFood can forecast demand, optimize processes, and deliver consistent user experiences.

---

## Solution Overview (Legacy Architecture)

The diagram below illustrates iFood's legacy architecture, where Data Science and Engineering teams had separate workflows — leading to challenges when deploying real-time ML models into production.

![Blog Image 1 - 2](/images/3-BlogImage/blog1-2.jpg)
> *Figure 2. Legacy Architecture — Describing data flow and the barriers between teams.*

Previously, data scientists developed models in notebooks, fine-tuned, and published artifacts. Engineers then had to integrate these artifacts into the production system, causing delays and integration errors. To address this, iFood developed an internal ML platform to unify the process from development to deployment, creating a seamless experience for both teams.

---

## Updated Architecture and ML Go!

One of the core capabilities of iFood's ML platform is providing the infrastructure to serve predictions. The internal platform (called **ML Go!**) is responsible for managing the deployment process, overseeing SageMaker Endpoints and Jobs. ML Go! supports both offline (batch) and real-time (online) predictions, and manages the lifecycle of models (registry, versioning, monitoring).

![Blog Image 1 - 3](/images/3-BlogImage/blog1-3.jpg)
> *Figure 3. Updated Architecture — Including pipelines, model registry, and inference components.*

The platform provides:
- Automated ML pipelines (SageMaker Pipelines) for model training and retraining.
- ML Go! CI/CD to push artifacts, build Docker images, and trigger pipelines.
- SageMaker Model Registry for versioning and model management.
- Monitoring mechanisms to detect drift and performance degradation.

---

## Final Architecture: Inference Components & ML Go! Gateway

A significant improvement is the abstraction concept connecting with SageMaker (Endpoints & Jobs) called **ML Go! Gateway**, along with separating "inference components" in the endpoint — helping to divide concerns, accelerate delivery, and manage resources more efficiently. Endpoints now manage multiple inference components, and ML Go! CI/CD only focuses on model version promotion, without deep intervention in infrastructure.

![Blog Image 1 - 4](/images/3-BlogImage/blog1-4.jpg)
> *Figure 4. Final Architecture — Inference components, ML Go! Gateway, and integration with service accounts.*

In this new structure:
- Endpoints can contain multiple inference components, allowing load distribution by function or load.
- ML Go! Dispatcher/Gateway forwards requests to the appropriate endpoint or job.
- CI/CD handles artifacts (Docker images, configs), and SageMaker Pipeline orchestrates training → evaluation → registry → deployment.

---

## Using SageMaker Inference Model Serving Containers

Standardizing the environment through containers is a crucial element of modern ML platforms. SageMaker provides built-in containers for TensorFlow, PyTorch, XGBoost, and more, as well as the ability to use custom containers.

iFood focuses on using **custom containers** to:
- Standardize ML code (not directly using notebooks in production).
- Package dependencies, libraries, and inference logic in an image (e.g., BruceML scaffolding).
- Easily recreate training and serving environments, monitor results, and debug.

BruceML helps standardize the way training and serving code is written, creating a scaffold compatible with SageMaker (autotuning, deployment hooks, monitoring).

---

## Automating Deployment and Retraining (ML Pipelines & CI/CD)

iFood uses **SageMaker Pipelines** to build CI/CD for ML: pipelines are responsible for orchestrating the entire data flow — from preprocessing, training, evaluation, to promotion in the Model Registry and deployment. ML Go! CI/CD integrates with the organization’s CI/CD system to:
- Push artifacts (code + container image).
- Trigger training and evaluation pipelines.
- Automatically register models into the Model Registry.
- Deploy or promote models to the appropriate endpoint (online / batch).

Depending on SLA:
- **Batch inference**: Uses SageMaker Transform jobs for large-scale predictions.
- **Real-time inference**: Deploys models to SageMaker Endpoint with the appropriate container/instance configuration.

SageMaker Pipelines helps automate and coordinate complex workflows, reducing errors and shortening development cycles.

---

## Running Inference at Different SLA Formats

iFood uses multiple inference methods to meet different requirements:
- **Real-time endpoints** for low-latency tasks (user-facing).
- **Batch transform jobs** for large-scale data processing, periodic recommendations.
- **Asynchronous inference** (SageMaker Asynchronous Inference) for time-consuming inference tasks.
- **Multi-model endpoints (GPU)** to host multiple models on the same GPU endpoint, optimizing resource use.

The improvements in collaboration between iFood and the SageMaker Inference team include:
- Optimizing cost and performance for inference (reducing ~50% of cost for some workloads, lowering ~20% average latency when using inference components).
- Improving autoscaling to handle spikes more effectively (shortening scaling time, enhancing detection of scale events).
- Easier deployment of LLM / Foundation Models (FM).
- **Scale-to-zero** feature for endpoints helps save costs when there is no traffic.
- Multi-model GPU endpoints reduce infrastructure costs in multi-model scenarios.

---

## Model Optimization and Packaging

Some technical points iFood focuses on:
- Standardizing containers for both training and serving.
- Automating the build/publish of images to the registry (ECR).
- Packaging LLM / FM for faster deployment.
- Supporting autoscaling and scale-to-zero for dev/test environments and low-traffic workloads.

---

## Achieved Benefits & Impact

The benefits iFood has gained:
- Reduced time to get models into production (faster time-to-market).
- Increased pipeline & artifact reuse across teams.
- Lower operational costs through GPU/multi-model optimization and scale-to-zero.
- Improved stability and model management at scale.

---

## Conclusion

By leveraging SageMaker capabilities, iFood has transformed its approach to ML/AI: building a centralized ML platform (ML Go!), automating data flows, standardizing containers, and collaborating with the SageMaker Inference team to optimize efficiency, cost, and scalability. This has helped iFood:
- Bridge the gap between Data Science and Engineering.
- Deploy hundreds of ML models reliably.
- Create a reference platform for organizations wishing to apply inference at scale.

> *“At iFood, we are leading the way in applying AI and machine learning technologies to transform... The lessons learned have helped us create our internal platform, which can serve as a blueprint for other organizations...”*  
> – Daniel Vieira, Director of ML Platforms at iFood.

---

## About the Authors

![Daniel Vieira](/images/3-BlogImage/blog1-5.png)  
**Daniel Vieira** — Director of Machine Learning Engineering at iFood. He has a background in computer science (BSc & MSc, UFMG) and over a decade of experience in software engineering and ML platforms. He enjoys music, philosophy, and coffee.

---

![Debora Fanin](/images/3-BlogImage/blog1-6.png)  
**Debora Fanin** — Senior Customer Solutions Architect at AWS (Brazil). She specializes in managing enterprise customer transformation and designing effective cloud adoption strategies.

---

![Saurabh Trikande](/images/3-BlogImage/blog1-7.png)  
**Saurabh Trikande** — Senior Product Manager, Amazon Bedrock & SageMaker Inference. Focuses on democratizing AI and inference solutions at scale.

---

![Gopi Mudiyala](/images/3-BlogImage/blog1-8.jpg)  
**Gopi Mudiyala** — Senior Technical Account Manager at AWS. Supports clients in the financial services industry and is passionate about machine learning.

---