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
┌─────────────────────┐
│        CLIENT       |
│                     |
└──────────┬──────────┘
           │
           |
           │ HTTP Request
           ▼
┌─────────────────────┐
│ API GATEWAY         │
│ Port 9095           │
└──────────┬──────────┘
           │ 
           │ Routes Request 
           ▼
┌─────────────────────┐
│ ORDER SERVICE       │
│ Port 8082           │
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
