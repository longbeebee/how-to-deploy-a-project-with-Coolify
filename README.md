<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
**Table of Contents**  *generated with [DocToc](https://github.com/thlorenz/doctoc)*

- [HOW TO DEPLOY A PROJECT BY COOLIFY PLATFORM](#how-to-deploy-a-project-by-coolify-platform)
  - [1. Overview](#1-overview)
  - [2. Why do we use Coolify?](#2-why-do-we-use-coolify)
    - [2.1. Benefits of Using Coolify](#21-benefits-of-using-coolify)
    - [2.2. Drawbacks of Using Coolify](#22-drawbacks-of-using-coolify)
  - [3. Deploying a Project by Coolify](#3-deploying-a-project-by-coolify)
    - [1. Architecture](#1-architecture)
    - [2. Installation](#2-installation)
    - [3. How to deploy a project in Coolify](#3-how-to-deploy-a-project-in-coolify)
      - [3.1 Using Nixpacks](#31-using-nixpacks)
      - [3.2 Using Docker Service Resource](#32-using-docker-service-resource)
    - [4 Conclusion](#4-conclusion)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

# HOW TO DEPLOY A PROJECT BY COOLIFY PLATFORM

## 1. Overview

Coolify is an open-source platform accepting that we deploy an application, a database, or anything else like a service at our VPS. It is designed as the solution instead of a cloud service such as Heroku, Vercel, etc., and we have full access that is not binding providers.

For more information: [Coolify](https://coolify.io)

## 2. Why do we use Coolify? 

We have many years of experience in deploying applications for small-scale enterprises, and one of the key challenges we often face is optimizing operational costs. Why is that? When we decide to launch a project, the factors that determine a product’s success are speed, simplicity, and the ability to solve real-world problems. Therefore, choosing the right technology and operational platform has helped us achieve both success and profitability in our tech business.

As a result, we always seek open-source platforms that allow us to operate with the lowest possible cost. Coolify is one of the platforms we have chosen to run the technology products we provide.

### 2.1. Benefits of Using Coolify

1. <strong>Cost-saving:</strong>

  - Avoid expensive fees from cloud service providers by using your own servers.

2. <strong>Security and privacy:</strong>

  - Your data is stored locally, minimizing risks related to security and privacy.

3. <strong>High customizability:</strong>

  - Freely configure and deploy services according to your specific needs without limitations from providers.

4. <strong>Strong community support:</strong>

  - Join the Coolify user community to receive support and share experiences.

### 2.2. Drawbacks of Using Coolify

1. <strong>Requires technical knowledge:</strong>

  - Self-hosted servers: You need to be familiar with Linux, SSH, Docker, domains, SSL, and network configurations.

  - Challenging for beginners: Not very beginner-friendly for those without a DevOps or sysadmin background.


2. <strong>You are fully responsible for security and maintenance.</strong>

  - No professional operations team like those at cloud providers.

  - You're responsible for security updates, patching vulnerabilities, preventing DDoS attacks, monitoring logs, and system supervision.


3. <strong>Limited horizontal scalability</strong>

  - Manual scale-out: Unlike Vercel or AWS, which offer auto-scaling, Coolify does not automatically scale containers under heavy load.

  - If you want to scale, you must:

    - Manually add nodes.

    - Manually configure load balancing (e.g., with Traefik, Nginx proxy, etc.).

4. <strong>Resources depend on the server you choose.</strong>

  - Using a weak VPS may result in poor performance, affecting your entire application.

  - No high-availability (HA) zones like premium cloud tiers.

5. <strong>Still under development</strong>

  - Some advanced features may be unstable (e.g., internal load balancing, advanced backups).

  - Updates can introduce bugs if not thoroughly tested before upgrading Coolify.

6. <strong>Limited disaster recovery capabilities</strong>

  - No built-in automatic snapshots by default; you must configure backups and restore strategies yourself (e.g., backups, volume mounts).

  - If the server crashes without a backup, all data may be lost.

7. <strong>Small community</strong>

  - Though growing quickly, Coolify’s community is still small compared to Docker, Kubernetes, or Netlify → less troubleshooting documentation.

  - For support, you often need to ask on Discord or GitHub and wait for assistance. 

## 3. Deploying a Project by Coolify

### 1. Architecture

  - Coolify is built on a Docker and GitOps architecture, designed to simplify the deployment, management, and monitoring of applications and databases on self-managed infrastructure.

  - ![coolify_architecture](coolify_architecture.png)

  - #### 1.1 Core Components in Coolify Architecture
    - <strong>Coolify App:</strong> The main application (web interface) that allows you to manage applications, services, logs, and deployment environments.

    - <strong>Docker Engine:</strong>: Coolify uses Docker to run applications, services, and databases as containers.

    - <strong>Docker Compose:</strong> Coolify initializes service stacks using Docker Compose, supporting multi-container setups (app + database + proxy).

    - <strong>Traefik:</strong> A built-in reverse proxy for routing and automatic SSL provisioning for applications.

    - <strong>Git Integration:</strong> Supports GitHub, GitLab, Bitbucket, etc., to automatically clone repositories, build, and deploy applications.

    - <strong>Internal API + WebSocket:</strong> Handles communication between the UI, backend, and agent to provide real-time deployment status updates.

  - #### 1.2 Deployment Architecture
    - ![coolify_deployment_architecture](coolify_deployment_architecture.png)
    - 1: Automatically pull source code from Git.
    - 2: Build Docker images.
    - 3: Deploy containers with internal networking.
    - 4: Assign routes via Traefik and provision SSL.

  - #### 1.3 Network & Security Management
    - <strong>Internal Docker Network:</strong> Coolify uses Docker networks to isolate containers.
    
    - <strong>Traefik Proxy:</strong> Handles internet access and automatically issues SSL certificates via Let's Encrypt.
    
    - <strong>Firewall:</strong> You should block all ports except for HTTP/HTTPS and SSH.

### 2. Installation
  - For this guide, we used Hostinger installing Coolify automatically.
  - Reference: [Install Document](https://coolify.io/docs/get-started/installation).

### 3. How to deploy a project in Coolify
#### 3.1 Using Nixpacks 

1. <strong>Create a Project</strong>

- 1: Click Projects.

- 2: Click Add.

    ![coolify_1](coolify_1.png)

- 3: Fill in the name.

- 4: Click continue.

    ![coolify_2](coolify_2.png)


2. <strong>Create a Resource</strong>

- 1: Click Add New Resource.

    ![coolify_3](coolify_3.png)

<strong>There are so many resources you could deploy (maybe we'll deploy a Bitcoin miner service in the future :D ).</strong>

- 2: In this guide, we choose the private repository.

    ![coolify_4](coolify_4.png)

<strong>You must be adding your SSH key of your Github in Security.</strong>

- Reference: [Setup SSH Key](https://coolify.io/docs/knowledge-base/git/github/integration).

    ![coolify_5](coolify_5.png)

- 3: Select Private Repository Resource, and your SSH key added.

    ![coolify_8](coolify_8.png)

    ![coolify_6](coolify_6.png)

- 4: Fill in the repo URL.

- 5: Fill the branch.

- 6: Use Nixpacks.

- 7: Select the public port.

- 8: If you want to deploy a static page, let's check the box (useful for front-end ).

    ![coolify_7](coolify_7.png)


- 9: Configure the name of the application.

- 10: Generate domain.

    ![coolify_9](coolify_9.png)

- 11: Maybe configure the container labels.

    ![coolify_10](coolify_10.png)


- 12: Maybe configure the container name for beautiful.

    ![coolify_11](coolify_11.png)


- 13: Set up environment variables for security (if you want to configure private variables ).

    ![coolify_12](coolify_12.png)

- 14: Set up the limited resources for VPS to ignore leak of memory or overload CPU.

    ![coolify_13](coolify_13.png)

<strong>For the other advanced features, please refer to the document.</strong>

3. <strong>Deployment</strong>

- 1: Let's create the nixpacks.toml file and push it to the branch used to deploy.

    ![coolify_14](coolify_14.png)


- 2: Click Deploy/Redeploy and check the deployment history. You can also check the logs and see that the application will be serving. It is a success!! :D.

    ![coolify_15](coolify_15.png)

    ![coolify_16](coolify_16.png)

<strong>The Big Problem: The application deployed by Nixpacks couldn't mount volumes to a VPS for saving. Therefore, the old container would be replaced, and volumes could be deleted. Coolify still doesn't support mount volumes now, you must save volumes manually :< . To address this problem, we navigate the deployment to Docker Service Resources. :D Let's begin the new journey!! </strong>  

#### 3.2 Using Docker Service Resource

<strong>We still create project is the same in the previous steps.</strong>

1. <strong>Create a Resource</strong>

- 1: Click Add New Resource.

    ![coolify_3](coolify_3.png)

- 2: Choose Docker File.

    ![coolify_17](coolify_17.png)

<strong>We will use the both Docker file and Docker Compose file.</>

2. <strong>Prepare Docker file and Docker Compose file</strong>

- 1: Example for Docker file

    ![coolify_18](coolify_18.png)

- 2: Example for Docker Compose file

    ![coolify_19](coolify_19.png)

<strong>Exactly!! We could make the Application more efficient for saving Data by configure the specific path in "volumes" :D</strong>

3. <strong>Configuration</strong>

- 1: Configure The resource such Nixpack resource but remember that you must load the docker compose files in below:

    ![coolify_20](coolify_20.png)

- 2: Now, let's click deploy and enjoy the moment :D

    ![coolify_21](coolify_21.png)

### 4 Conclusion

This guide shows you the easiest way to run an application on Coolify. In upcoming posts, we’ll cover more advanced features such as integrating Git Actions, connecting S3 storage, setting up SSL, configuring a reverse proxy or VPN, adding Metrics/Kibana, notifications, and more. Follow our Git account to stay updated.
<p>Author: <span style="color: red;">FunnyTrickyBeeBee</span> :D</p>

  

