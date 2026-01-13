# Kafka-based Analytics Dashboard (Backend)

A Kafka-powered event analytics system that captures user activity events, processes them asynchronously, stores analytics data, handles failures using a Dead Letter Queue (DLQ), and exposes data for visualization through an Angular dashboard.

This project is designed as a learning-focused yet real-world Kafka system, demonstrating core messaging concepts, fault tolerance, and end-to-end data flow.

---

## Overview

This system tracks user activity events (e.g., LOGIN) using Apache Kafka as the messaging backbone.

- Events are produced by a Spring Boot producer
- Events are consumed and validated by a Spring Boot consumer
- Valid events are stored in MongoDB
- Invalid events are redirected to a Kafka Dead Letter Queue (DLQ)
- Processed data is consumed by an Angular-based dashboard

---

## Features

- Kafka Producer & Consumer (Spring Boot)
- Asynchronous event processing
- MongoDB persistence
- Dead Letter Queue (DLQ) for faulty events
- Dockerized Kafka & MongoDB
- Clean separation of services

---

## System Architecture
<br/> <br/>
<p align="center">
  <img src="SystemArchitecture.png" width="700" alt="System Architecture">
</p>
<br/> <br/>

---

## Event Flow

1. User triggers an event (LOGIN) from UI
2. Producer publishes event to Kafka topic user-activity
3. Kafka persists the event
4. Consumer validates the event
5. Valid event → MongoDB
6. Invalid event → DLQ topic
7. DLQ events visible in UI

---

## Dead Letter Queue (DLQ)

### Why DLQ?

DLQ ensures:
- No message loss
- Consumers don’t crash on bad data
- Faulty events can be inspected later

### Example DLQ Event

```json
{
  "userId": "u111",
  "eventType": null,
  "timestamp": "2026-01-13T16:37:42Z"
}
```

Stored in MongoDB collection: dlq_event

---

## Tech Stack
- Backend
  * Java
  * Spring Boot
  * Spring Kafka
  * MongoDB
  * Gradle

- Messaging
  * Apache Kafka
  * Zookeeper

- Infrastructure
  * Docker
  * Docker Compose
 
---

# Frontend Repository

The Angular dashboard is maintained in a separate repository:
- https://github.com/04Marsha/Kafka-based-Analytics-Dashboard-Frontend

---

