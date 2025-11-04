# 🐳 Docker Container – Interview Questions & Answers

This document contains frequently asked **Docker Container interview questions** with clear, concise answers — perfect for DevOps and Cloud Engineer interviews.

---

## 🧩 **1. Basic Level (Fundamentals)**

### 1. What is Docker?

Docker is a platform that automates the deployment of applications inside lightweight, portable containers. It ensures consistency across multiple environments by packaging code and dependencies together.

### 2. What is a Docker container?

A **container** is an isolated environment that runs an application and all its dependencies. It’s lightweight, fast, and uses the host OS kernel.

### 3. What is the difference between a container and a virtual machine?

| Feature | Virtual Machine | Container         |
| ------- | --------------- | ----------------- |
| OS      | Full OS per VM  | Shared host OS    |
| Speed   | Slower          | Faster            |
| Size    | Heavy (GBs)     | Lightweight (MBs) |

### 4. What are Docker images?

Images are **read-only templates** used to create containers. They include the application, libraries, and environment configuration.

### 5. What is Docker Hub?

Docker Hub is a **cloud-based registry** for finding, storing, and sharing Docker images.

### 6. What is the difference between `docker run` and `docker start`?

* `docker run`: Creates and starts a new container.
* `docker start`: Starts an existing stopped container.

### 7. How do you list running containers?

```bash
docker ps        # Running containers
docker ps -a     # All containers
```

### 8. How do you stop and remove a container?

```bash
docker stop <container_id>
docker rm <container_id>
```

---

## ⚙️ **2. Intermediate Level (Usage & Configuration)**

### 9. What is a Dockerfile?

A **Dockerfile** is a text file with instructions for building a Docker image.

### 10. Common Dockerfile instructions

| Instruction          | Description                     |
| -------------------- | ------------------------------- |
| `FROM`               | Sets base image                 |
| `RUN`                | Executes commands               |
| `COPY` / `ADD`       | Copies files into image         |
| `CMD` / `ENTRYPOINT` | Defines container start command |
| `EXPOSE`             | Opens ports                     |
| `WORKDIR`            | Sets working directory          |

### 11. Difference between CMD and ENTRYPOINT

* **CMD**: Default command (can be overridden).
* **ENTRYPOINT**: Fixed main command (cannot be easily overridden).

### 12. How do you persist data in Docker?

Use **volumes** or **bind mounts**:

```bash
docker run -v /host/path:/container/path myimage
```

### 13. How can you check container logs?

```bash
docker logs <container_id>
```

### 14. What is Docker Compose?

Docker Compose helps you **define and manage multi-container applications** with a `docker-compose.yml` file.

### 15. How do containers share data?

* Shared **volumes**
* **Networking**
* Linking (legacy)

### 16. How do you expose ports?

```bash
docker run -p 8080:80 nginx
```

Maps host port `8080` to container port `80`.

---

## 🚀 **3. Advanced Level (Deployment & Optimization)**

### 17. Difference between COPY and ADD

* `COPY`: Only copies local files.
* `ADD`: Copies local files **and** can extract `.tar` or download from URLs.

### 18. How to optimize image size?

* Use lightweight base images (e.g., `alpine`).
* Combine commands with `&&`.
* Clean up temp files.
* Use `.dockerignore`.

### 19. What are namespaces and cgroups?

* **Namespaces**: Provide isolation for process, network, and filesystem.
* **Cgroups**: Limit and manage resource usage (CPU, memory).

### 20. How do you inspect a container?

```bash
docker inspect <container_id>
```

### 21. How to connect multiple containers?

```bash
docker network create mynet
docker run --network=mynet myapp
```

### 22. How to build an image?

```bash
docker build -t myapp:1.0 .
```

### 23. What is a multi-stage build?

A technique to **reduce image size** by using multiple `FROM` stages — one for building, one for runtime.

### 24. Docker Swarm vs Kubernetes

| Feature   | Docker Swarm     | Kubernetes        |
| --------- | ---------------- | ----------------- |
| Setup     | Easy             | Complex           |
| Scaling   | Quick            | Advanced          |
| Ecosystem | Native to Docker | Industry standard |

### 25. What is `docker system prune`?

Used to remove unused containers, images, and volumes:

```bash
docker system prune
```

---

## 🔒 **4. Security & Best Practices**

### 26. How do you scan Docker images for vulnerabilities?

Use:

* `docker scan <image>`
* **Trivy**, **Clair**, **Anchore**

### 27. Why avoid running containers as root?

For security — prevents attackers from gaining host-level access.

### 28. What is `.dockerignore`?

A file to **exclude unnecessary files** (e.g., `.git`, logs, node_modules) from image build context.

### 29. How to manage environment variables?

```bash
docker run -e ENV=prod myapp
```

or define in `.env` for Compose.

### 30. How do you handle secrets in Docker?

Use:

* **Docker secrets (Swarm)**
* External secret managers (AWS Secrets Manager, HashiCorp Vault)

---

## 🧠 **Quick Recap Commands**

| Task             | Command                          |
| ---------------- | -------------------------------- |
| List containers  | `docker ps -a`                   |
| Build image      | `docker build -t myapp .`        |
| Run container    | `docker run -d -p 8080:80 myapp` |
| Logs             | `docker logs <id>`               |
| Stop container   | `docker stop <id>`               |
| Remove container | `docker rm <id>`                 |
| Clean up         | `docker system prune`            |

---

## 🖼️ **Docker Container Architecture Diagram (ASCII)**

```
+------------------------------------------------------+
|                   Docker Host                        |
|  +----------------------------------------------+   |
|  | Docker Daemon (dockerd)                      |   |
|  |----------------------------------------------|   |
|  |  - Image Management                          |   |
|  |  - Container Lifecycle                       |   |
|  +----------------------------------------------+   |
|         |                    |                     |
|         v                    v                     |
|  +--------------+    +-------------------+          |
|  |  Container 1 |    |   Container 2     |          |
|  | (App + Libs) |    |  (App + Libs)     |          |
|  +--------------+    +-------------------+          |
+------------------------------------------------------+
|                  Host Operating System               |
+------------------------------------------------------+
|                   Hardware (CPU, RAM)                |
+------------------------------------------------------+
```

**Key Components:**

* **Docker Client:** Sends CLI/API commands (e.g., `docker run`, `build`)
* **Docker Daemon:** Manages containers and images
* **Images:** Blueprints for containers
* **Containers:** Running instances of images
* **Registry (Docker Hub):** Stores and shares images

---

## 💡 **Real-time Interview Scenario Questions**

### 1. A container keeps restarting in production. How do you troubleshoot?

* Check logs: `docker logs <container>`
* Inspect events: `docker inspect <container>`
* Verify health checks and restart policy.
* Review application error logs inside the container.

### 2. Your container is using too much disk space. How do you fix it?

* Run `docker system df` to identify large images.
* Clean unused images/volumes: `docker system prune`.
* Use lightweight base images.

### 3. How would you debug a container that stops immediately after running?

* Use interactive mode: `docker run -it <image> /bin/bash`
* Check CMD/ENTRYPOINT correctness in Dockerfile.

### 4. You updated your app code but container still runs old version. Why?

* Image cache may not be rebuilt.
* Use `--no-cache` with `docker build`.
* Confirm Dockerfile `COPY` instruction correctly includes new files.

### 5. A container fails to connect to another service. Steps to fix?

* Check container network: `docker network ls`
* Ping target container by name.
* Verify exposed and published ports.
* Use custom bridge network instead of default.

### 6. How do you recover data from a deleted container?

* If volume used: reattach to new container `docker run -v <volume>:/data`.
* If no volume: data lost permanently.

### 7. You need zero downtime deployment. What’s your approach?

* Run new container version alongside existing one.
* Use load balancer or reverse proxy.
* Stop old container after verification.

### 8. Container shows ‘permission denied’ accessing file. Fix?

* Verify file permissions and UID mapping.
* Use `--user` flag to match container user.
* Mount with correct permissions.

### 9. Container crashes due to OOM (Out of Memory). Solution?

* Limit memory: `docker run -m 512m ...`
* Optimize app memory usage.
* Enable swap if appropriate.

### 10. How would you monitor Docker container performance?

* Use `docker stats` for live metrics.
* Integrate with Prometheus, Grafana, or cAdvisor.
* Use AWS CloudWatch or Datadog for large-scale setups.

---

## 🏁 **Conclusion**

Mastering Docker container concepts is essential for any DevOps or Cloud Engineer role.
Understanding **images, volumes, networking, and Dockerfiles** forms the foundation for advanced tools like **Kubernetes, Jenkins CI/CD, and AWS ECS**.
