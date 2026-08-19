# One Enterprise Platform - Microservices Learning Project
## Overview 
This project was developed as part of a Microservices
### the application consists of:
- User Service
- Order Service
- payment Service
- Eureka Service Registry
- API Gateway
- Service Discovery
- Inter-Service Communication using OpenFeign
## Architecture
 ```text
4
┌─────────────────────┐
5
│ CLIENT │
6
│ (Postman / Browser) │
7
└──────────┬──────────┘
8
│
9
│ HTTP Request
10
▼
11
┌─────────────────────┐
12
│ API GATEWAY │
13
│ Port 9095 │
14
└──────────┬──────────┘
15
│
16
│ Routes Request
17
▼
18
┌─────────────────────┐
19
│ ORDER SERVICE │
20
│ Port 8082 │
21
└──────────┬──────────┘
22
│
23
│ Feign Client
24
┌─────┴─────┐
│ │
▼ ▼
┌───────────┐ ┌─────────────┐
│USERSERVICE│ │PAYMENTSERVICE│
│ Port 8081 │ │ Port 8083    │
└───────────┘ └─────────────┘
```

## Circuit Breaker
Payment Service Down
        ↓
Feign Failure
        ↓
Circuit Breaker
        ↓
Fallback Method
