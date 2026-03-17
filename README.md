# Transcendence Game Backend & Monolith

This repository showcases the core game infrastructure and procedural generation systems developed for the **Transcendence** project.

## Key Technical Contributions

### 1. High-Performance Microservices Architecture
Designed and implemented a scalable backend using a microservices approach to manage game lifecycles, matchmaking, and tournaments.
- **Game Manager**: Orchestrates session creation and lifecycle management.
- **Lobby Manager**: Handles real-time matchmaking and game room orchestration.
- **Tournament Service**: Manages complex tournament brackets and progression logic.

### 2. Real-Time Binary Communication
Implemented a low-latency communication layer using **NATS** and **Protobuf**.
- **Protobuf Serialization**: All internal service communication and client-server state updates use binary serialization to minimize bandwidth and CPU overhead.
- **NATS Message Bus**: Leverages NATS for high-throughput, asynchronous communication between microservices.
- **WebSocket Gateway**: Built a custom gateway using `uWebSockets.js` to bridge client WebSockets with the internal NATS bus, ensuring sub-millisecond message distribution.

### 3. Custom Physics Engines
Developed server-side physics engines in Node.js to ensure authoritative game state.
- **Pong Physics**: Deterministic physics engine for standard multiplayer Pong.
- **PongBR (Battle Royale)**: A specialized engine capable of handling up to 100 players in a single game instance, featuring circle shrinking and high-frequency state broadcasts.

### 4. Monolith: SDF-based Procedural Generation
Created an innovative 3D asset generation system based on **Signed Distance Functions (SDF)**.
- **Procedural Voxel Engine**: A custom script that uses mathematical definitions (SDFs) to generate complex 3D structures like the "Temple Monolith".
- **Pre-build Optimization**: Generates optimized voxel data in TypeScript, allowing for efficient rendering of massive 3D structures in the frontend.

## Tech Stack
- **Languages**: TypeScript, JavaScript (Node.js)
- **Messaging**: NATS, WebSockets (uWebSockets.js)
- **Data Serialization**: Protocol Buffers (Protobuf)
- **Containerization**: Docker, Docker Compose
- **Procedural Generation**: Signed Distance Functions (SDF), Voxel-based rendering

## Architecture Overview
```text
[ Clients ] <--> [ WebSocket Gateway (uWS) ]
                        |
                        v
                 [ NATS Message Bus ]
                        |
      ------------------------------------------
      |                 |                      |
[ Game Manager ] [ Lobby Manager ] [ Tournament Service ]
      |                 |                      |
      ------------------------------------------
                        |
              [ Physics Engines (Pong/BR) ]
```
