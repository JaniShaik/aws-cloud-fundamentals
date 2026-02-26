# AWS Global Infrastructure – Regions, AZs & Edge Locations

AWS global infrastructure is designed for:

- High availability
- Fault tolerance
- Low latency
- Global scalability

Understanding this is fundamental before deploying production workloads.

---

## AWS Global Infrastructure Layers

AWS is built using four major layers:

1. Regions
2. Availability Zones (AZs)
3. Data Centers
4. Edge Locations (Points of Presence)

---

# AWS Regions

A Region is a geographical cluster of data centers.

Examples:
- us-east-1
- eu-west-3
- ap-southeast-2

Most AWS services are **region-scoped**, meaning resources created exist inside a specific region.

---

## How to Choose an AWS Region?

When launching a new application, consider:

### 1. Compliance Requirements
Data should not leave a region without explicit permission.

### 2. Proximity to Customers
Closer region = lower latency.

### 3. Service Availability
New services are not available in every region.

### 4. Pricing
Pricing varies by region.

Region selection is an architectural decision.

---

# AWS Availability Zones (AZs)

Each region contains multiple AZs (minimum 3, up to 6).

Example:
- ap-southeast-2a
- ap-southeast-2b
- ap-southeast-2c

Each AZ:

- Contains one or more discrete data centers
- Has independent power and networking
- Is isolated from other AZs
- Connected via ultra-low latency fiber network

This enables:

- Multi-AZ deployments
- Disaster recovery strategies
- High availability architectures

---

# AWS Edge Locations (Points of Presence)

AWS has:

- 400+ Edge Locations
- 10+ Regional Caches
- 90+ cities
- 40+ countries

Edge locations reduce latency by delivering content closer to users.

Services that use Edge Locations:

- CloudFront (CDN)
- Route 53
- AWS Shield

---

# Global vs Region-Scoped Services

## Global Services
- IAM
- Route 53
- CloudFront
- WAF

These are globally distributed.

---

## Region-Scoped Services
- EC2
- RDS
- Lambda
- Elastic Beanstalk
- Rekognition

These operate within a selected region.

Understanding this distinction is critical when designing distributed systems.

---

# Architectural Insight

Production-grade systems typically:

- Deploy across multiple AZs
- Use region-based redundancy
- Leverage edge locations for latency optimization

AWS infrastructure enables global-scale systems by design.

Understanding this structure is the first step toward architect-level cloud engineering.
