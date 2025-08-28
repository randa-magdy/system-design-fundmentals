# Networking Fundamentals: IP, OSI, TCP/UDP, and DNS

## 1. IP Addresses (Internet Protocol)

An IP address is a unique identifier that allows devices to communicate on the internet or local networks. It's like a postal address for digital devices.

### IP Versions

**IPv4 (32-bit)**
- Format: Four decimal numbers separated by dots
- Address space: ~4 billion addresses
- Example: `192.168.1.1` or `8.8.8.8` (Google DNS)
- Status: Nearly exhausted due to internet growth

**IPv6 (128-bit)**
- Format: Eight groups of hexadecimal numbers separated by colons
- Address space: ~340 undecillion addresses (340 × 10³⁶)
- Example: `2001:0db8:85a3:0000:0000:8a2e:0370:7334`
- Simplified: `2001:db8:85a3::8a2e:370:7334` (zeros can be omitted)

### IP Address Types

| Type | Description | Example Use Case |
|------|-------------|------------------|
| **Public** | Globally routable, assigned by ISP | Your home router's external IP |
| **Private** | Local network only, not internet-routable | Devices in your home (192.168.x.x) |
| **Static** | Never changes, manually configured | Web servers, email servers |
| **Dynamic** | Changes periodically, assigned by DHCP | Most home internet connections |

**Private IP Ranges:**
- `10.0.0.0` - `10.255.255.255`
- `172.16.0.0` - `172.31.255.255`
- `192.168.0.0` - `192.168.255.255`

---

## 2. OSI Model (Open Systems Interconnection)

The OSI model is a 7-layer framework that standardizes how network communication works. Think of it as a universal language for networking.

### The Seven Layers

| Layer | Name | Function | Examples |
|-------|------|----------|----------|
| **7** | Application | User interface, network services | HTTP, SMTP, FTP, web browsers |
| **6** | Presentation | Data translation, encryption, compression | SSL/TLS, JPEG, MP3 |
| **5** | Session | Establishes, manages, terminates connections | NetBIOS, RPC, SQL sessions |
| **4** | Transport | End-to-end data delivery, error recovery | TCP, UDP |
| **3** | Network | Routing between different networks | IP, ICMP, routers |
| **2** | Data Link | Node-to-node delivery on same network | Ethernet, Wi-Fi, switches |
| **1** | Physical | Electrical signals, cables, hardware | Cables, hubs, repeaters |

### Why OSI Matters

- **Troubleshooting**: Isolate problems to specific layers
- **Standardization**: Ensures different vendors' equipment works together
- **Security**: Understand where threats can occur at each layer
- **Education**: Breaks complex networking into manageable concepts

**Real-world Example**: When you visit a website:
1. **Physical**: Electrical signals travel through cables
2. **Data Link**: Your network card handles local network communication
3. **Network**: Your router finds the path to the web server
4. **Transport**: TCP ensures all data arrives correctly
5. **Session**: Your browser maintains a session with the server
6. **Presentation**: HTTPS encrypts the data
7. **Application**: Your browser displays the webpage

---

## 3. TCP vs UDP (Transport Protocols)

### TCP (Transmission Control Protocol)
- **Connection-oriented**: Establishes a connection before sending data
- **Reliable**: Guarantees data delivery and correct order
- **Error checking**: Retransmits lost packets
- **Slower**: Due to overhead from reliability features

**Use Cases**: Web browsing (HTTP/HTTPS), email (SMTP), file transfer (FTP)

### UDP (User Datagram Protocol)
- **Connectionless**: Sends data without establishing a connection
- **Fast**: Minimal overhead
- **No guarantees**: No delivery confirmation or error correction
- **Fire-and-forget**: Sends data whether receiver is ready or not

**Use Cases**: Live video streaming, online gaming, DNS queries, VoIP calls

### TCP vs UDP Comparison

| Feature | TCP | UDP |
|---------|-----|-----|
| **Speed** | Slower (reliable) | Faster (minimal overhead) |
| **Reliability** | Guaranteed delivery | No guarantees |
| **Connection** | Connection-oriented | Connectionless |
| **Data Order** | Maintains order | No order guarantee |
| **Error Handling** | Built-in error correction | Basic error detection only |
| **Use When** | Accuracy is critical | Speed is more important than accuracy |

**Analogy**: 
- **TCP** is like registered mail - slower but guaranteed delivery
- **UDP** is like shouting across a room - fast but no guarantee everyone heard

---

## 4. Domain Name System (DNS)

DNS translates human-readable domain names (like `google.com`) into IP addresses that computers use. It's like the internet's phonebook.

### How DNS Works
![dns work](./images/dns-work.png)

### DNS Server Types

**DNS Resolver (Recursive Resolver)**
- First stop for DNS queries
- Acts as middleman between client and nameservers
- Caches responses for faster future lookups
- Example: Your ISP's DNS server (8.8.8.8 for Google)

**Root Nameservers**
- 13 types worldwide (A through M)
- Direct queries to appropriate TLD servers
- Managed by ICANN

**TLD Nameservers**
- Handle specific extensions (.com, .org, .net)
- Two types: Generic (gTLD) and Country Code (ccTLD)
- Examples: `.com`, `.uk`, `.edu`, `.gov`

**Authoritative Nameservers**
- Final authority for specific domains
- Contains actual DNS records
- Returns IP addresses or CNAME records

### DNS Query Types

| Query Type | Description | When Used |
|------------|-------------|-----------|
| **Recursive** | Resolver does all the work, returns final answer | Most client queries |
| **Iterative** | Client follows referrals to find answer | Between DNS servers |
| **Non-recursive** | Answer already known/cached | Cached responses |

### Common DNS Record Types

| Record | Purpose | Example |
|--------|---------|---------|
| **A** | Maps domain to IPv4 address | `google.com → 172.217.164.142` |
| **AAAA** | Maps domain to IPv6 address | `google.com → 2607:f8b0:4004:c1b::65` |
| **CNAME** | Alias to another domain | `www.example.com → example.com` |
| **MX** | Mail server for domain | `example.com → mail.example.com` |
| **TXT** | Text information | SPF, DKIM for email security |
| **NS** | Nameserver for domain | `example.com → ns1.example.com` |

### DNS Concepts

**Subdomains**
- Additional parts of main domain
- Examples: `blog.example.com`, `mail.example.com`, `api.example.com`
- Used for organizing services and content

**DNS Zones**
- Administrative divisions of domain namespace
- Allow granular control over DNS records
- Can delegate authority to different entities

**DNS Caching & TTL**
- **TTL (Time To Live)**: How long records can be cached
- **Caching**: Improves performance by storing recent lookups
- When TTL expires, new lookup required

**Reverse DNS**
- Maps IP addresses back to domain names
- Uses PTR records
- Important for email servers to verify legitimacy

### Popular DNS Providers

- **Cloud Providers**: AWS Route53, Google Cloud DNS, Azure DNS
- **CDN/Security**: Cloudflare DNS (1.1.1.1)
- **Public DNS**: Google (8.8.8.8), Quad9 (9.9.9.9)
- **Specialized**: NS1 for advanced DNS management

---

## Summary

These four networking fundamentals work together to enable internet communication:

1. **IP addresses** provide unique identifiers for devices
2. **OSI model** standardizes how network communication is structured
3. **TCP/UDP** handle data transport with different reliability/speed tradeoffs
4. **DNS** translates human-readable names to IP addresses

Understanding these concepts is essential for network troubleshooting, security implementation, and system design.
