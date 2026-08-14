# One Enterprise Platform - Microservices Learning Project
## Overview 
This project was developed as part of a Microservices
### the application consists of:
- User Service
- Order Service
- Eureka Service Registry
- API Gateway
- Service Discovery
- Inter-Service Communication using OpenFeign
## Architecture
                    +------------------+
                    |      Client      |
                    +---------+--------+
                              |
                              |
                              v

                    +------------------+
                    |   API Gateway    |
                    |     Port 9095    |
                    +---------+--------+
                              |
            -------------------------------------
            |                                   |
            |                                   |
            v                                   v

    +------------------+              +------------------+
    |   User Service   |              |  Order Service   |
    |    Port 9090     |<-------------|    Port 9091     |
    +------------------+    Feign     +------------------+
                                     Client
                    \                  /
                     \                /
                      \              /
                       v            v

                  +-------------------+
                  |   Eureka Server   |
                  |     Port 8761     |
                  +-------------------+
