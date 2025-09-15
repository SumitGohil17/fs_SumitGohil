# Student Ride-Sharing Platform  
**Realtime Chat + Maps Integration + Anonymous Ride Matching**

A scalable full-stack web and mobile platform that allows students to share rides by matching nearby users who are heading to the same destination.  
Features include **live location tracking**, **real-time chat**, and **map-based ride discovery** with privacy-friendly unique IDs.

---

## 🌐 Live Demo
Coming soon…

---

## ✨ Key Features
- **Map-based Matching**: Students enter their destination; the app finds other nearby students going to the same place.
- **Realtime Location**: Updates every few seconds using Socket.IO + Redis Pub/Sub.
- **Anonymous IDs**: Public IDs hide personal info until both sides confirm.
- **Realtime Chat**: Secure one-to-one chat once a ride is confirmed.
- **Dual Map Providers**:  
  - **Google Maps (Paid)** for unlimited usage.  
  - **GoMaps/Leaflet (Free)** for up to 500 requests/day.

---

## 🏗️ Tech Stack

| Layer                  | Technology                                      |
|------------------------|--------------------------------------------------|
| Frontend (Web)         | **React 18**, **Next.js 14**, Tailwind CSS       |
| Mobile (Optional)      | React Native + Expo                              |
| Backend Services       | **Node.js + NestJS** (TypeScript)                |
| Database               | **MongoDB Atlas** with 2dsphere geo indexes      |
| Cache / Pub-Sub        | Redis Cluster                                    |
| Realtime Gateway       | Socket.IO over WebSockets                        |
| Maps / Geocoding       | Google Maps JS API OR GoMaps/Leaflet             |
| Infrastructure         | Docker, Kubernetes (EKS/GKE), Nginx Ingress      |
| CI/CD                  | GitHub Actions → Docker Registry → K8s Deploy    |
| Monitoring & Logs      | Prometheus + Grafana, ELK / OpenTelemetry        |

---

## 🗺️ High-Level Architecture

