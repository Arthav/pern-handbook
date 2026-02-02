# Server Fundamentals & Terminology

Before diving into Docker and Deployment, let's clarify the infrastructure terms.

## 1. What is a "Server"?
In the context of web apps, "Server" can mean two things:

### A. The Hardware (The Machine)
A physical computer running in a datacenter. It has a CPU, RAM, Disk, and an Internet connection.
*   **Bare Metal**: A dedicated physical box.
*   **Virtual**: A slice of a physical box (see VPS via Hypervisor).

### B. The Software (The Program)
A process that listens for network requests.
*   **Web Server**: Nginx, Apache.
*   **App Server**: Node.js, Python.
*   **DB Server**: PostgreSQL.

---

## 2. The Operating System (OS)
The software that manages the hardware.

### Linux (The Standard)
Over 90% of the web runs on Linux.
*   **Why?**: Open-source, stable, secure, resource-efficient, and scriptable.
*   **Distributions (Distros)**: Variations of Linux.
    *   **Ubuntu**: Most popular, easy to use. Recommended for beginners.
    *   **Debian**: The rock-stable parent of Ubuntu.
    *   **Alpine**: Extremely lightweight (5MB), used heavily in Docker.
    *   **CentOS/RHEL**: Enterprise-focused.

### Windows Server
Used for .NET/C# applications. Rarely used for Node/Postgres stacks unless mandated by corporate policy.

---

## 3. VPS (Virtual Private Server)
Ideally, you want your own server. But buying a $5000 Dell PowerEdge is overkill.

### How it works (Virtualization)
Cloud providers (AWS, DigitalOcean) take a massive physical server (e.g., 64 CPUs, 512GB RAM) and use software (Hypervisor) to split it into 100 smaller "Virtual" servers.

*   **You get**: A "Droplet" or "Instance" with 1 vCPU and 1GB RAM.
*   **You see**: A fully independent OS. You have root access. It looks and feels exactly like a dedicated machine.

### VPS vs. Shared Hosting
*   **Shared Hosting (GoDaddy, Bluehost)**: You upload files to a shared folder. You don't have root access. You can't install custom software easily. **Don't use this for PERN.**
*   **VPS**: You are the admin. You install Node, Postgres, Nginx yourself.

---

## 4. Web Server vs. Application Server
This is the most common point of confusion.

### The Application Server (Node.js)
*   **Role**: Executes logic.
*   **Example**: "User logged in -> Check password hash -> Query DB -> Return JSON."
*   **Protocols**: Usually HTTP, but not optimized for static files or SSL.

### The Web Server (Nginx)
*   **Role**: Traffic Controller & Guard.
*   **Example**: "Request for `/api`? Send to Node. Request for `image.png`? Send file directly from disk."
*   **Key Features**:
    1.  **Reverse Proxy**: Hides your internal Node app from the public internet.
    2.  **SSL Termination**: Handles HTTPS encryption/decryption (Node is slow at this).
    3.  **Load Balancing**: Distribute traffic to multiple Node instances.
    4.  **Static Files**: Serves HTML/CSS/Images 50x faster than Node.

### Variations
*   **Nginx**: Event-driven, asynchronous. The gold standard for high performance.
*   **Apache**: Process-driven. Older, very flexible (.htaccess), but memory-heavy.
*   **Caddy**: Modern, written in Go. Automatic HTTPS (Zero config SSL). Gaining popularity.

---
[← Previous Section](../04-full-stack-integration/03-security.md) | [Next Section →](./03-dockerization.md)
