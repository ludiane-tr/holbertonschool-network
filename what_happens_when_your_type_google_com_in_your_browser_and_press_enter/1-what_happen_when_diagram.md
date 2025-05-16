# 🌐 Understanding What Happens When You Visit https://www.google.com

When we type a URL like `https://www.google.com` into our browser and press Enter, a lot of things happen behind the scenes before the web page is displayed. This exercise aims to visualize and explain the journey of that request through a simplified architecture. Below is a Mermaid diagram that illustrates each step involved in the request and response process, including DNS resolution, encryption, load balancing, server interaction, and database communication.

## 🧠 Request Flow Diagram

```mermaid
graph TD
    A[User types https://www.google.com in browser] --> B[DNS resolution: Get IP address]
    B --> C[Firewall: Allow outbound HTTPS traffic (port 443)]
    C --> D[Encrypted HTTPS request to Load Balancer]
    D --> E[Load Balancer distributes request]
    E --> F[Web Server receives request]
    F --> G[Web Server contacts Application Server]
    G --> H[Application Server queries Database]
    H --> I[Database returns data]
    I --> J[Application Server generates web page]
    J --> K[Web Server serves HTML page]
    K --> L[Browser displays Google homepage]
```