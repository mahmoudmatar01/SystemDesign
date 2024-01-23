# How To Scale Your System To Millions Of Users README
Welcome to the world of System Design! It's like being the architect of a digital building, where we plan and organize how everything will work together. Imagine you're creating a recipe for a dish – you need the right ingredients, the right steps, and a way to make sure it turns out great every time. That's what system design is all about for computers and software.

## Table of Contents
1. [System Design Components](#system-design-components)
   - [Frontend](#frontend)
   - [DNS (Domain Name System)](#dns-domain-name-system)
   - [Web Server](#web-server)
   - [Database](#database)
2. [Scaling the System](#scaling-the-system)
   - [Vertical Scaling](#vertical-scaling)
   - [Horizontal Scaling](#horizontal-scaling)
   - [Load Balancer Clusters (Active-Passive)](#load-balancer-clusters-active-passive)
   - [Replication (Leader-Based Replication)](#replication-leader-based-replication)
3. [In-Memory Database (Cache)](#in-memory-database-cache)
   - [In-Memory Database (Cache)](#1-in-memory-database-cache)
   - [Write Strategies](#2-write-strategies)
   - [Cache Limitations](#3-cache-limitations)
   - [Expiration Policy](#4-expiration-policy)
   - [Eviction Policy](#5-eviction-policy)
   - [What Happens If Cache Goes Down?](#6-what-happens-if-cache-goes-down)
4. [Content Delivery Networks (CDN)](#content-delivery-networks-cdn)
   - [Cache Busting](#cache-busting)
   - [Time to Live (TTL)](#time-to-live-ttl)
5. [Conclusion](#conclusion)

## System Design Components
### Frontend
The frontend is like the face of the system, where users see and interact with everything. It includes:
- `User Interface (UI)`: This is how things look on the application – what users click, type, and see.
- `User Experience (UX)`: It's how users feel when they use the application, the overall experience.
- `Client-side Code`: This is the behind-the-scenes code (HTML, CSS, JavaScript) that runs in users' web browsers.
- `Frontend Frameworks`: These are tools that make it easier to build and organize the frontend (like React, Angular, or Vue.js).

### DNS (Domain Name System)
DNS is like the phonebook of the internet, turning easy-to-remember names into computer-friendly numbers. It involves:
- `Domain Registrar`: This is like the store where you buy and manage your website's name.
- `Name Servers`: These are servers that keep important info about website names.
- `DNS Records`: They're like cards with details about a website – where it is, where emails go, and more.
- `DNS Resolver`: This is a helpful service that finds out the numbers (IP addresses) when you give it a website name.

DNS is a hierarchical system involving various servers that work together to translate user-friendly domain names into the numeric IP addresses that computers use to communicate on the internet. This process happens behind the scenes every time you access a website.

### Web Server
The web server is like the waiter at a restaurant, taking orders and bringing back what's requested. It does things like:
- `HTTP Server`: It handles requests from web browsers and sends back what's needed.
- `Load Balancer`: It's like making sure no waiter is too busy – spreading the work between servers.
- `SSL/TLS` Certificates: These are like secret codes that keep information safe when it travels between the user and the server.
- `Web Application Firewall (WAF)`: It's like a bouncer at a club, keeping out trouble from the website.

### Database
The database is like the storage room where we keep all the information. It's made up of:
- `Database Management System (DBMS)`: This is like the librarian who helps you find and organize books.
- `Relational Database`: Think of this like a well-organized spreadsheet with different tables of information (like MySQL or PostgreSQL).
- `NoSQL Database`: This is a more flexible way of storing information, like using a big notebook with different pages (like MongoDB or Cassandra).
- `Data Replication`: This is like making copies of important books in case one gets lost, helping the system stay strong and work smoothly.

## Scaling the System
Welcome to the Scaling Guide! This section will walk you through different strategies for scaling a system to handle more traffic, users, and data. Scaling is crucial for ensuring that your system stays responsive and performs well as it grows.

### Vertical Scaling
Vertical scaling involves increasing the power of a single server to handle more load. Here's what you need to know:
- `Description`: You upgrade the existing server by adding more resources like CPU, RAM, or storage.

### Horizontal Scaling
Horizontal scaling involves adding more servers to distribute the load. Let's dive into the details:
- `Description`: You add more servers to your system, spreading the load across them.

### Load Balancer Clusters (Active-Passive)
Load balancers distribute incoming traffic across multiple servers, ensuring efficient use of resources and preventing overload. In an active-passive configuration:
- `Description`: One load balancer (active) handles the traffic, while others (passive) remain on standby.

### Replication (Leader-Based Replication)
Replication involves creating and maintaining copies of data across multiple servers. In leader-based replication:
- `Description`: One server (leader) handles write operations, while others (followers) replicate the data.


## In-Memory Database (Cache)
Welcome to the In-Memory Database (Cache) section! This guide will provide insights into using in-memory databases as caches, covering various aspects such as write strategies, limitations, expiration and eviction policies, and what happens in case of cache downs.

### 1. In-Memory Database (Cache)
In-memory databases store and retrieve data in the system's main memory (RAM), providing faster access compared to traditional disk-based databases. Caching frequently accessed data in memory can significantly improve application performance.

### 2. Write Strategies
- `Write Behind`: Write behind strategy involves writing data to the cache and acknowledging the write operation before updating the underlying data store asynchronously.
- `Write Around`: Write around strategy involves bypassing the cache and writing directly to the underlying data store. The data is brought into the cache on-demand.
- `Write Through`: Write through strategy involves writing data both to the cache and the underlying data store synchronously.

### 3. Cache Limitations
- `Size Limitation`: Caches have a finite size, and managing data that exceeds this size can lead to performance issues.
- `Data Volatility`: Data in the cache is temporary and may be lost if the system restarts or the cache is cleared.
- `Data Freshness`: Caches may not always contain the most up-to-date information from the underlying data store.

### 4. Expiration Policy
Expiration policies define how long data remains in the cache before it is considered stale and needs to be refreshed. Common expiration policies include time-based expiration or a fixed duration.

### 5. Eviction Policy
Eviction policies determine which data is removed from the cache when it reaches its size limit. Two common eviction policies are:
- `LRU (Least Recently Used)`: Removes the least recently accessed items first.
Pros: Simple and effective.
Cons: May not consider the actual importance or frequency of data access.
- `LFU (Least Frequently Used)`: Removes items with the least frequent accesses.
Pros: Focuses on the importance of data access.
Cons: Requires maintaining and updating access frequency counters for each item.

### 6. What Happens If Cache Goes Down?
- If the cache goes down:
`Reads`: Applications may experience slower response times as they need to fetch data from the main data store.
`Writes`: Write strategies (write behind, write around, or write through) will determine the impact on write operations.


## Content Delivery Networks (CDN)
- Optimizing performance in a distributed environment involves not only effective caching strategies within the application (in-memory database) but also leveraging Content Delivery Networks (CDN) for efficient content delivery. Understanding concepts like cache busting and time to live ensures that your system delivers a seamless and up-to-date user experience. 
- Content Delivery Networks (CDN) are distributed networks of servers that work together to deliver web content quickly to users based on their geographical location.

### Cache Busting
Cache busting is a technique used to force the browser to download the latest version of a file by changing its name or appending a query string. This ensures that users always receive the most recent content

### Time to Live (TTL)
Time to Live (TTL) is a setting that defines the lifespan of content in a cache, specifying how long it should be stored before being considered outdated. It is commonly expressed in seconds.

## Conclusion

Congratulations on navigating through the world of system design and scaling strategies! By understanding the key components of system design, exploring scaling techniques, delving into in-memory database caching, and appreciating the role of Content Delivery Networks (CDN), you've gained valuable insights into architecting robust and scalable systems.

Remember, the key to success lies in selecting the right ingredients for your digital building – the frontend, DNS, web server, and database – and applying scaling strategies that suit your specific needs. The journey doesn't end here; continuous learning and adaptation are essential in the ever-evolving landscape of technology.

Whether you're building a system to accommodate millions of users or optimizing content delivery with CDN, the principles outlined in this guide will serve as a foundation for creating efficient, responsive, and reliable digital experiences. Best of luck on your system design endeavors, and may your systems scale seamlessly to meet the demands of the digital world!
