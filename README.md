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
<img width="2310" height="1111" alt="diagram-export-9-15-2025-1_45_37-PM" src="https://github.com/user-attachments/assets/5f08be05-43a6-4523-979c-6a0cc2408e34" />


## 🔄 Core User Flow

### 1. Get Current Location & Destination
- Frontend uses browser/mobile geolocation to get the current `lat/lng`.
- Calls Google Maps / GoMaps Geocoding API to convert the destination address into `destLat/destLng`.

### 2. Search Nearby Students
- **API Request:**
```http
GET /api/v1/rides/search?lat={curLat}&lng={curLng}&destLat={dLat}&destLng={dLng}&radius=5km
