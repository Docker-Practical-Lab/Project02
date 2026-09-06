# 🐳 Project 02 — Docker Versioning & Docker Hub

> 🚀 A simple **Node.js + Express** API that fetches posts from
> [JSONPlaceholder](https://jsonplaceholder.typicode.com), fully containerized with **Docker**.
> This project demonstrates how to **version Docker images with tags** and **push/pull images
> to/from Docker Hub**.

---

## 📦 Tech Stack

| 🧰 Technology | 📝 Purpose |
|---|---|
| 🟢 Node.js (Alpine) | Runtime for the API |
| ⚡ Express | Web framework |
| 🐳 Docker | Containerization & deployment |
| 📦 Docker Hub | Cloud image registry |

---

## 🧱 Project Structure

```
Project02/
├── 🐳 Dockerfile        # Builds the container image
├── 📦 package.json      # Dependencies & start script
├── 🔒 .dockerignore     # Files excluded from the image build
├── ⚙️  .env              # Environment variables (never committed)
└── 🗄️  server.js         # Express application entry point
```

---

## 🚦 Prerequisites

Before you begin, make sure you have the following installed:

- ✅ [Docker](https://docs.docker.com/get-docker/) (includes **Docker Desktop**)
- ✅ [Node.js](https://nodejs.org/) *(optional — only needed to run without Docker)*
- ✅ A [Docker Hub](https://hub.docker.com) account *(required for pushing images)*

---

## 🏃 Getting Started

### 1️⃣ Run locally without Docker *(optional)*

```bash
# Install dependencies
npm install

# Start the server (uses nodemon)
npm start
```

The API will be available at **http://localhost:5000** 🟢

| 🔗 Endpoint | 📋 Description |
|---|---|
| `GET /health` | ⚕️ Health check — returns status & uptime |
| `GET /posts` | 📰 Fetch a list of posts |
| `GET /posts/:id` | 🔎 Fetch a single post by ID |

---

## 🐳 Dockerize the Application

### 2️⃣ Build the image

```bash
docker build -t project02 .
```

---

## 🏷️ Versioning Images ⚖️

> In Docker we can **manage versions** by adding a **tag** to our images. Tags let us keep
> multiple releases of the same image and switch between them easily.

### ➕ Build an image with a version tag

```bash
# Syntax: image_name:tag
docker build -t project02:1.0.0 .
```

You can create multiple versions with different tags:

```bash
docker build -t project02:1.0.0 .
docker build -t project02:1.1.0 .
docker build -t project02:latest .
```

### 🖥️ Run a container from a specific version (tag)

```bash
# Syntax: docker run -p 5000:5000 image_name:tag
docker run --name project02-container -p 5000:5000 project02:1.0.0
```

🔍 Now open **http://localhost:5000** in your browser to see the app running inside the container.

### 🧹 Useful container commands

```bash
# List running containers
docker ps

# Stop the container
docker stop project02-container

# Remove the container
docker rm project02-container

# List all local images
docker images
```

---

## ☁️ Push Images to Docker Hub

> 📦 **Docker Hub** is a cloud-based registry service provided by Docker, Inc. It lets you
> **store, manage, and distribute Docker images**. It's a central repository where you can find
> official Docker images, share your own images, and collaborate with others. 🌍

### 1️⃣ Log in to Docker Hub

```bash
docker login
```

> 🔑 Enter your **Docker Hub username** and **password** when prompted.

### 2️⃣ Tag the image with your Docker Hub username

```bash
# Syntax: docker tag image_name dockerhub_username/image_name:tag
docker tag project02 your_dockerhub_username/project02:1.0.0
```

Replace `your_dockerhub_username` with your actual **Docker Hub username** 🙋

### 3️⃣ Push the tagged image to Docker Hub

```bash
# Syntax: docker push dockerhub_username/image_name:tag
docker push your_dockerhub_username/project02:1.0.0
```

✅ Once uploaded, your image is publicly available on Docker Hub at:
`https://hub.docker.com/r/your_dockerhub_username/project02`

---

## ⬇️ Pull an Image from Docker Hub

> 📥 Any developer (or any machine) can now **download and run** your image from anywhere:

```bash
# Syntax: docker pull image_name:tag
docker pull your_dockerhub_username/project02:1.0.0
```

### ▶️ Run the pulled image

```bash
docker run -d --name project02-container -p 5000:5000 your_dockerhub_username/project02:1.0.0
```

---

## 🎯 Summary — What I Learned 📚

| 📌 Topic | 💡 Key Takeaway |
|---|---|
| **Versioning Images** 🏷️ | Add a **tag** to an image to manage versions, e.g. `project02:1.0.0` |
| **Running a version** 🖥️ | `docker run -p 5000:5000 project02:1.0.0` starts a specific tagged version |
| **Docker Hub** ☁️ | A cloud **registry** to store, manage, and share Docker images |
| **Pushing** 📤 | `docker login` → `docker tag` → `docker push` |
| **Pulling** 📥 | `docker pull image_name:tag` downloads an image from Docker Hub |

---

## 🛡️ Security Notes 🔐

- The `.dockerignore` file ensures `node_modules` and `.env` are **not** copied into the image.
- Never commit your `.env` file — keep secrets out of version control. 🕵️

---

## 🗂️ Useful Docker Commands Cheat-Sheet 🧰

| 📋 Command | 🎯 Action |
|---|---|
| `docker build -t name:tag .` | 🏗️ Build an image with a tag |
| `docker images` | 👀 List local images |
| `docker run -p 5000:5000 name:tag` | 🚀 Run a container |
| `docker ps` | 📋 List running containers |
| `docker login` | 🔑 Log in to Docker Hub |
| `docker tag img user/img:tag` | 🏷️ Tag image with username |
| `docker push user/img:tag` | 📤 Push to Docker Hub |
| `docker pull user/img:tag` | 📥 Pull from Docker Hub |

---

## 📄 License

This project is licensed under the **ISC** license. ⚖️

---

Made with ❤️ for the 🐳 Docker Practical Lab