# Docker Bake - Multi-Platform Image Builder

## Repository: **Packer-Bakery-Foundation**
### Description:
This repository automates the building of multi-platform Docker images using **Docker Bake**. It allows parallel builds and supports multiple architectures like **AMD64** and **ARM64**, making it ideal for scalable CI/CD pipelines.

---

## 🚀 How Docker Bake Works
Instead of manually running multiple `docker build` commands, Docker Bake allows you to define build targets in a **docker-bake.hcl** file and execute them together using:

```sh
docker buildx bake
```

### **✨ Benefits of Docker Bake:**
✅ **Multi-Platform Builds** (e.g., Linux/AMD64 & Linux/ARM64)  
✅ **Parallel Builds** (faster builds using BuildKit)  
✅ **Centralized Build Config** (uses YAML/HCL format)  
✅ **CI/CD Friendly** (easily integrates into pipelines)  

---

## 🛠 Example Workflow
### **Step 1: Define Build Targets in `docker-bake.hcl`**
Create a `docker-bake.hcl` file in the root directory:

```hcl
group "default" {
    targets = ["python-bakery"]
}

target "python-bakery" {
    context    = "."
    dockerfile = "Dockerfile"
    platforms  = ["linux/amd64", "linux/arm64"]
    tags       = ["yourusername/python-bakery:latest"]
}
```

### **Step 2: Create a Dockerfile**
Write the `Dockerfile` for your Python 3.9 image:

```dockerfile
FROM ubuntu:20.04

RUN apt-get update && apt-get install -y \
    python3.9 python3.9-venv python3.9-dev \
    && rm -rf /var/lib/apt/lists/*

CMD ["python3"]
```

### **Step 3: Build and Push Using Docker Bake**
Run the following command to **build and push** the image:

```sh
docker buildx bake --push
```

✅ **Builds Python 3.9 images** for both **AMD64** and **ARM64**  
✅ **Pushes the images** to Docker Hub automatically  

---

## 🔥 Why Use Docker Bake?
| Feature                 | `docker build` | `docker buildx bake` |
|------------------------|---------------|------------------|
| Multi-platform builds  | ❌ No         | ✅ Yes           |
| Parallel builds       | ❌ No         | ✅ Yes           |
| Centralized config     | ❌ No         | ✅ Yes           |
| YAML/HCL support       | ❌ No         | ✅ Yes           |
| CI/CD pipeline support | ✅ Yes        | ✅ Yes           |

---

## 🚀 Conclusion
Docker Bake simplifies **multi-platform** and **parallel builds**, making it a **powerful tool for CI/CD pipelines** and **scalable Docker environments**.

Would you like help integrating Docker Bake into a **CI/CD workflow**? 🤖 Let’s discuss!

