# 🌐 Understanding What Happens When You Visit https://www.google.com

When we type a URL like `https://www.google.com` into our browser and press Enter, a lot of things happen behind the scenes before the web page is displayed. This exercise aims to visualize and explain the journey of that request through a simplified architecture. Below is a Mermaid diagram that illustrates each step involved in the request and response process, including DNS resolution, encryption, load balancing, server interaction, and database communication.

## 🧠 Request Flow Diagram

```mermaid
sequenceDiagram
    participant User as User
    participant Browser as Browser
    participant DNS as DNS Server
    participant FW as Firewall
    participant LB as Load Balancer
    participant WS as Web Server
    participant AS as Application Server
    participant DB as Database

    User->>Browser: Type https://www.google.com
    Browser->>DNS: Resolve domain name
    DNS-->>Browser: Return IP address
    Browser->>FW: Send HTTPS request (port 443)
    FW-->>Browser: Allow request
    Browser->>LB: Encrypted request (HTTPS)
    LB->>WS: Forward request
    WS->>AS: Ask for page generation
    AS->>DB: Query for data
    DB-->>AS: Return data
    AS-->>WS: Generated HTML page
    WS-->>Browser: Serve HTML response
    Browser-->>User: Display Google homepage
    