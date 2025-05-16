# What Happens When You Type https://www.google.com in Your Browser and Press Enter?

This blog post explains the detailed workflow that happens when you type `https://www.google.com` into your browser and press Enter. This includes everything from DNS resolution to database querying, focusing on the major components of the web stack.

---

## 1. DNS Request

The process starts when your browser needs to translate the human-readable domain `www.google.com` into an IP address. This is done via a **DNS (Domain Name System) request**:

- Your computer checks the local DNS cache.
- If not found, it sends a DNS query to the configured DNS server.
- The DNS server responds with the IP address of the server hosting Google.

---

## 2. TCP/IP Connection

Once the IP address is known, your browser initiates a **TCP/IP connection** to the Google server:

- It performs a TCP handshake (SYN, SYN-ACK, ACK) to establish a reliable connection.
- This ensures packets are delivered in order and without loss.

---

## 3. Firewall

The request passes through any **firewalls** on your network or on the server side, which enforce security policies:

- Firewalls inspect packets and decide whether to allow or block them.
- Only legitimate traffic is permitted to reach the Google servers.

---

## 4. HTTPS/SSL Encryption

Since the URL starts with `https://`, the connection is secured using **SSL/TLS encryption**:

- The browser and server perform an SSL handshake.
- This involves exchanging certificates and establishing encryption keys.
- All data transmitted is encrypted to protect confidentiality and integrity.

---

## 5. Load Balancer

Google uses **load balancers** to distribute incoming requests efficiently:

- The load balancer receives the encrypted request.
- It decides which backend web server will handle the request based on load, availability, and other metrics.
- This ensures scalability and fault tolerance.

---

## 6. Web Server

The selected **web server** receives the request:

- It handles HTTP(s) traffic and serves static content like HTML, CSS, and images.
- For dynamic content, it forwards the request to the application server.

---

## 7. Application Server

The **application server** is responsible for:

- Running the business logic to generate the web page dynamically.
- Processing user requests, applying backend logic, and preparing the response.

---

## 8. Database

To provide dynamic content, the application server queries the **database**:

- It retrieves, updates, or stores data needed to generate the requested page.
- The database responds with the requested data.

---

## Publishing the Blog Post

This blog post is published on [Linkedin](https://www.linkedin.com/feed/update/urn:li:activity:7329048264962473985/).

---

# Diagram of the Request Flow

```mermaid
flowchart TD
    A[User types https://www.google.com] --> B[DNS Resolution]
    B --> C[Get IP address of Google server]
    C --> D[TCP/IP Connection Established]
    D --> E[Traffic passes through Firewall]
    E --> F[Traffic encrypted with HTTPS/SSL]
    F --> G[Load Balancer distributes request]
    G --> H[Web Server receives request]
    H --> I[Web Server forwards request to Application Server]
    I --> J[Application Server processes request]
    J --> K[Application Server queries Database]
    K --> L[Database returns data]
    L --> J
    J --> H
    H --> M[Web Server sends web page response]
    M --> N[Browser renders the page]

The diagram illustrates:

- DNS resolution
- Request hitting server IP and port
- Encrypted traffic flow
- Firewall traversal
- Load balancer distribution
- Web server answering with a web page
- Application server generating the page
- Database queries for content

---

## 1. Everything's Better with a Pretty Diagram

To better understand the complex flow of what happens when you type `https://www.google.com` in your browser and press Enter, it is helpful to visualize the sequence of events and interactions between different components involved in processing this request.

The following sequence diagram illustrates the detailed step-by-step communication between the user, browser, DNS server, firewall, load balancer, web server, application server, and database. It highlights how the request is resolved, secured, routed, and fulfilled to deliver the final web page back to the user.

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant DNS_Server
    participant Firewall
    participant Load_Balancer
    participant Web_Server
    participant App_Server
    participant Database

    User->>Browser: Types https://www.google.com and presses Enter
    Browser->>DNS_Server: DNS request for www.google.com
    DNS_Server-->>Browser: Returns IP address
    Browser->>Firewall: Sends TCP/IP request (encrypted HTTPS)
    Firewall->>Load_Balancer: Forwards encrypted request
    Load_Balancer->>Web_Server: Distributes request to web server
    Web_Server->>App_Server: Forwards request for dynamic content
    App_Server->>Database: Queries database
    Database-->>App_Server: Returns data
    App_Server-->>Web_Server: Sends generated web page
    Web_Server-->>Browser: Responds with web page
    Browser-->>User: Renders page

