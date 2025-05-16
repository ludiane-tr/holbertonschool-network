# What's Happening When You Type `google.com` in Your Browser and Press Enter?

![Google homepage](https://media.licdn.com/dms/image/v2/D4D12AQE2WRLZL6KJSA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1676283849130?e=1752710400&v=beta&t=YRdnIVnOYuvQlIlUWA-5vTZiPyeMQgNcXRS7P-ZqzYo)



This blog post aims to unveil the mechanics behind this seemingly simple process by explaining, step by step, what happens when you type `https://www.google.com` and press Enter. We'll walk through the key technologies involved—from the DNS request to the database—such as:

- TCP/IP  
- Firewalls  
- HTTPS/SSL  
- Load balancers  
- Web servers  
- Application servers  

---

## Step 1: DNS Request – Resolving the IP Address

When you enter a URL like `www.google.com`, your computer can't communicate directly with this human-readable name. It needs the corresponding **IP address**—like a physical address for a building.

This is where the **Domain Name System (DNS)** comes in. DNS acts like the phonebook of the internet, converting domain names (like `www.google.com`) into machine-understandable IP addresses (e.g., `172.217.12.46`).

### DNS Resolution Process

1. **Check local cache**  
   The browser first checks if it has previously resolved this domain and cached the IP. If so, it uses the cached IP, skipping the rest.

2. **Query recursive DNS server**  
   If not cached, the system sends a query to a recursive DNS server—usually provided by your ISP or a third-party service like Google DNS.

3. **Contact root servers**  
   The recursive server contacts one of the 13 root DNS server sets to locate the Top-Level Domain (TLD) servers (like `.com`, `.org`).

4. **Query TLD name servers**  
   Based on the domain extension, the recursive server queries the TLD server responsible (e.g., `.com`).

5. **Query authoritative name servers**  
   Then it queries the **authoritative DNS server** that holds the domain's records and fetches the IP address.

6. **Return IP address**  
   The resolved IP is returned to your browser so it can initiate a connection.

7. **Cache the result**  
   The result is cached for a period (defined by TTL—Time To Live) to speed up future queries.

---

## Step 2: Establishing the Connection – TCP/IP

Now with the IP address, your browser must establish a connection to exchange data. This is where **TCP/IP** comes in—the foundational communication protocol suite of the internet.

- **IP (Internet Protocol)** handles addressing and routing packets.
- **TCP (Transmission Control Protocol)** ensures reliable, ordered communication.

### The TCP 3-Way Handshake

To establish a TCP connection, the client and server perform a three-step handshake:

1. **SYN** (Synchronize)  
   The client sends a SYN packet with an initial sequence number to start a connection.

2. **SYN-ACK**  
   The server replies with its own sequence number and acknowledges the client's SYN.

3. **ACK**  
   The client sends a final ACK to confirm, and the connection is established.

This process ensures:

- Reliable connection setup  
- Sequence synchronization  
- Safe delivery and retransmission if needed  

> **Layered Communication**:  
> - TCP = Transport Layer  
> - IP = Network Layer  
> Their separation ensures robust, modular design in internet communication.

---

## Step 3: Network Security – The Role of Firewalls

Once a TCP connection is established, the request must pass through a **firewall**—a network security system that monitors and filters traffic based on predefined rules.

Firewalls protect against unauthorized access, malware, and cyberattacks by analyzing each packet.

### Types of Firewall Inspection

- **Packet Filtering**  
  Simple rule-based filtering on IP, port, and protocol.

- **Stateful Inspection**  
  Tracks active connections and only allows response traffic that matches a known request.

- **Proxy Services**  
  Acts as an intermediary between your browser and the web, hiding your IP and adding an extra security layer.

Firewalls can be:

- **Hardware-based** (often in routers)  
- **Software-based** (like Windows Firewall)

Your request likely passes through your local router’s firewall and Google’s infrastructure firewalls. For HTTPS, port `443` must be open.

Firewalls on both ends ensure a layered approach to cybersecurity.

---

## Step 4: Secure Communication – HTTPS/SSL

Since the URL starts with `https://`, you're initiating a **secure connection** with Google. HTTPS is the secure version of HTTP.

The “S” stands for “Secure” and indicates encryption of all communication between your browser and the server, made possible by **SSL/TLS** protocols.

- **SSL** = Secure Sockets Layer (legacy)  
- **TLS** = Transport Layer Security (modern)

HTTPS ensures:

- Data confidentiality  
- Authentication of the website  
- Integrity of the transmitted data

### TLS/SSL Handshake

1. **ClientHello**  
   Your browser sends supported TLS versions, cipher suites, and a random number.

2. **ServerHello**  
   The server responds with its certificate, selected cipher, and its random number.

3. **Key Exchange**  
   Both sides generate a shared secret (symmetric key) using asymmetric cryptography.

4. **Session Keys & Encryption**  
   All future communication is encrypted using the established session key.

The handshake ensures that only you and the server can decrypt the transmitted data.

---

