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
# Microservices Architecture

```text
┌─────────────────────┐
│       CLIENT        │
│ (Postman / Browser) │
└──────────┬──────────┘
           │
           │ HTTP Request
           ▼
┌─────────────────────┐
│     API GATEWAY     │
│      Port 9095      │
└──────────┬──────────┘
           │
           │ Routes Request
           ▼
┌─────────────────────┐
│    ORDER SERVICE    │
│      Port 8082      │
└──────────┬──────────┘
           │
           │ Feign Client
     ┌─────┴─────┐
     │           │
     ▼           ▼
┌───────────┐ ┌─────────────┐
│USERSERVICE│ │PAYMENTSERVICE│
│ Port 8081 │ │  Port 8083   │
└───────────┘ └─────────────┘
```

---

# Service Discovery Architecture

```text
                    ┌──────────────────┐
                    │  EUREKA SERVER   │
                    │    Port 8761     │
                    └────────┬─────────┘
                             │
      ┌──────────────────────┼──────────────────────┐
      │                      │                      │
      ▼                      ▼                      ▼

┌─────────────┐      ┌─────────────┐      ┌─────────────┐
│ API GATEWAY │      │ USER SERVICE│      │ORDER SERVICE│
│    9095     │      │    8081     │      │    8082     │
└─────────────┘      └─────────────┘      └──────┬──────┘
                                                  │
                                                  │
                                                  ▼
                                          ┌─────────────┐
                                          │PAYMENT SRVC │
                                          │    8083     │
                                          └─────────────┘
```

---

# Order Creation Flow

```text
POST /api/orders
        │
        ▼
┌──────────────────┐
│   API GATEWAY    │
│      9095        │
└────────┬─────────┘
         │
         ▼
┌──────────────────┐
│  ORDER SERVICE   │
└────────┬─────────┘
         │
         ├──────────────► USER SERVICE
         │               (Feign Client)
         │
         └──────────────► PAYMENT SERVICE
                         (Feign Client)

         │
         ▼
 OrderResponseDto
```

---

# Circuit Breaker Flow

```text
               NORMAL FLOW

ORDER SERVICE
      │
      ▼
PAYMENT SERVICE
      │
      ▼
 SUCCESS RESPONSE


------------------------------------------------


         PAYMENT SERVICE DOWN

ORDER SERVICE
      │
      ▼
PAYMENT SERVICE
      │
      ▼
   FAILED
      │
      ▼
CIRCUIT BREAKER
      │
      ▼
FALLBACK METHOD
      │
      ▼
"Payment Service Temporarily Unavailable"
```
## Circuit Breaker
Payment Service Down
        ↓
Feign Failure
        ↓
Circuit Breaker
        ↓
Fallback Method
