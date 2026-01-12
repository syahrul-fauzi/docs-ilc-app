# 📊 System Diagrams

## High-Level Architecture
```mermaid
graph TD
    Mobile[Expo App] --> API[API Gateway]
    API --> AI[AI Service]
    API --> DB[(Main DB)]
    API --> Auth[Auth Service]
```
