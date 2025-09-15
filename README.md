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

# Get Current Location & Destination

- Frontend uses browser/mobile geolocation for current lat/lng.

- Calls Google/GoMaps Geocoding to convert destination to destLat/destLng.

## Search Nearby Students
```
API:

GET /api/v1/rides/search?lat={curLat}&lng={curLng}&destLat={dLat}&destLng={dLng}&radius=5km

```
Backend queries MongoDB with $near on both currentLocation and destination.

Display Matches

- Frontend renders pins on the map and a side/bottom sheet list.

- Realtime updates stream over Socket.IO channels.

## Confirm Ride
```
API:

POST /api/v1/rides/{rideId}/confirm

```
Backend updates status and broadcasts ride:confirmed event.

## Frontend removes other matches and opens a private chat.

📡 REST / WebSocket API Overview
Method	Endpoint	Purpose

- POST	/api/v1/auth/signup	Register student, returns JWT + publicId

- POST	/api/v1/auth/login	Login, returns JWT

- POST	/api/v1/rides	Create ride offer/request

- GET	/api/v1/rides/search	Find nearby matching rides

- POST	/api/v1/rides/{rideId}/confirm	Confirm ride match

WS	ride:location:update	Push live location updates

WS	chat:message	Realtime chat messages

🌍 Google Maps API Endpoints Used
```
Geocoding (address → lat/lng):

https://maps.googleapis.com/maps/api/geocode/json?address={DESTINATION}&key=YOUR_API_KEY

```
```
Reverse Geocoding (lat/lng → address):

https://maps.googleapis.com/maps/api/geocode/json?latlng={LAT},{LNG}&key=YOUR_API_KEY

```
```
Nearby Search (optional for POIs):

https://maps.googleapis.com/maps/api/place/nearbysearch/json
   ?location={LAT},{LNG}&radius=5000&type=point_of_interest&key=YOUR_API_KEY

```
These URLs are called from the Map Provider Abstraction Service so you can swap Google ↔ GoMaps without frontend changes.

## 🚀 Deployment

Build Images
```
docker build -t student-rideshare-api .
docker build -t student-rideshare-web .
```

Push to Registry`
GitHub Actions pushes to DockerHub or ECR.

## Deploy to Kubernetes
```
kubectl apply -f k8s/
```
