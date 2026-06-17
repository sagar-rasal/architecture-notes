# Architecture Notes

A collection of architecture decisions, system design discussions, performance optimization strategies, and engineering learnings gathered from solving real-world enterprise software challenges.

## Topics

- System Design
- Software Architecture
- Java & Spring Boot
- Caching Strategies
- Performance Optimization
- Distributed Systems
- Design Patterns
- Database Design
- Scalability
- Architecture Decision Records (ADRs)



#Recommended Structure:
architecture-notes/
architecture-notes/
│
├── README.md
│
├── architecture-decisions/
│   ├── ADR-001-Dynamic-Office-Rule-Framework.md
│   ├── ADR-002-Cache-Refresh-Strategy.md
│   └── ADR-003-Configuration-vs-Hardcoding.md
│
├── system-design/
│   ├── Dynamic-Configuration-Service.md
│   ├── Distributed-Cache-Patterns.md
│   └── Event-Driven-Cache-Invalidation.md
│
├── performance/
│   ├── GWT-RPC-Optimization.md
│   ├── Login-Flow-Optimization.md
│   └── Cache-vs-Database-Lookups.md
│
├── poc-projects/
│   │
│   ├── spring-cloud-eureka/
│   │   ├── README.md
│   │   ├── discovery-server/
│   │   ├── user-service/
│   │   └── order-service/
│   │
│   ├── api-gateway/
│   │   ├── README.md
│   │   ├── gateway-service/
│   │   └── sample-services/
│   │
│   ├── distributed-cache/
│   │   ├── README.md
│   │   ├── redis-demo/
│   │   └── cache-client/
│   │
│   ├── kafka-event-driven/
│   │   ├── README.md
│   │   ├── producer/
│   │   └── consumer/
│   │
│   └── dynamic-rule-engine/
│       ├── README.md
│       ├── rule-service/
│       └── sample-ui/
│
└── diagrams/
    ├── eureka-architecture.png
    ├── api-gateway-flow.png
    └── cache-refresh-flow.png
