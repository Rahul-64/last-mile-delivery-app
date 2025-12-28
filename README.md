🚚 Last-Mile Delivery Confirmation System (LensKart Case Study)

A full-stack Last-Mile Delivery App that simulates how e-commerce companies like LensKart / Amazon / Flipkart confirm deliveries using Shipment ID + OTP verification.

This project demonstrates backend-driven business logic, OTP-based delivery validation, and mobile app integration using React Native.

📌 Problem Statement

In last-mile delivery systems, it is critical to ensure that:

A delivery is confirmed only once

The correct customer receives the order

Delivery partners cannot falsely mark orders as delivered

This project solves that problem using:

Unique Shipment ID

One-Time Password (OTP)

Backend-controlled verification and status tracking

Solution Overview
Flow:

Customer places an order

Backend generates:

Shipment ID

OTP

Delivery partner enters:

Shipment ID

OTP

Backend verifies:

Shipment existence

OTP correctness

Delivery status

Delivery result is returned with proper status

🛠 Tech Stack
Backend

Node.js

Express.js

MySQL

mysql2 (Promise-based)

dotenv

Frontend (Mobile App)

React Native

Expo (Expo Go)

TypeScript


🗂 Project Structure
LENSKART_LAST_MILE_DELIVERY/
│
├── backend/
│   ├── src/
│   │   ├── controllers/
│   │   │   └── deliveryController.js
│   │   ├── services/
│   │   │   └── deliveryService.js
│   │   ├── routes/
│   │   │   └── deliveryRoutes.js
│   │   ├── config/
│   │   │   ├── db.js
│   │   │   └── env.js
│   │   └── server.js
│   ├── .env.example
│   └── package.json
│
├── mobile-app/
│   ├── app/
│   │   └── (tabs)/
│   │       └── index.tsx
│   ├── src/
│   │   ├── config/
│   │   │   └── api.ts
│   │   ├── utils/
│   │   │   └── formatTime.ts
│   │   └── services/
│   │       └── deliveryApi.ts
│   └── package.json
│
└── README.md


🗄 Database Design
Database
CREATE DATABASE last_mile_delivery;

Table: shipments
CREATE TABLE shipments (
  id INT AUTO_INCREMENT PRIMARY KEY,
  shipment_id VARCHAR(50) UNIQUE NOT NULL,
  customer_name VARCHAR(100),
  otp_code VARCHAR(10),
  status ENUM('Pending', 'Delivered') DEFAULT 'Pending',
  delivered_at TIMESTAMP NULL,
  delivered_by VARCHAR(100)
);

Purpose

Tracks shipment lifecycle

Prevents duplicate delivery

Stores OTP and delivery metadata


🔗 Backend API Endpoints
1️⃣ Place Order
POST /api/place-order


Request

{
  "customer_name": "Rahul"
}


Response

{
  "shipment_id": "SHIP12345",
  "otp_code": "482193"
}

2️⃣ Confirm Delivery
POST /api/confirm-delivery


Request

{
  "shipment_id": "SHIP12345",
  "otp": "482193",
  "delivered_by": "DeliveryBoy01"
}

📡 HTTP Status Codes Used
Status Code	Meaning
200 OK	Successful delivery
400 Bad Request	Missing required fields
401 Unauthorized	Invalid OTP
404 Not Found	Shipment ID not found
409 Conflict	Shipment already delivered
500 Internal Server Error	Server error

🧠 Backend Business Logic

Shipment ID must exist

OTP must match

Delivery can happen only once

Re-verification returns already_delivered

Backend controls all delivery rules (frontend is thin)

📱 Mobile App UI Flow
Step 1

Enter customer name 

Place order - means you are placing order in frontend

Step 2

Shipment ID & OTP displayed (demo purpose)

Step 3

Delivery partner enters:

Shipment ID (alphanumeric)

OTP (numeric)

Step 4

Verify delivery

Result shown in human-readable format

App interfaces

Intro
<img width="499" height="622" alt="image" src="https://github.com/user-attachments/assets/06e34a6c-5612-4f04-97f9-6bffecff2ca0" />

Placing order from frontend
<img width="497" height="759" alt="image" src="https://github.com/user-attachments/assets/236f6f23-dc64-411f-b60f-0bfb0603f81b" />

✅ Successful Delivery

<img width="474" height="913" alt="image" src="https://github.com/user-attachments/assets/55f58639-d22f-40e8-9a2b-38122f12f0fa" />

⚠️ Already Delivered
<img width="480" height="929" alt="image" src="https://github.com/user-attachments/assets/940e51af-7e55-4bee-813a-4b4723076f28" />

⚠️ Missing Fields

#shipmentID missing
<img width="481" height="870" alt="image" src="https://github.com/user-attachments/assets/9a1ed0a7-24f7-4c76-8c25-a3a187492ca2" />

#OTP missing
<img width="501" height="897" alt="image" src="https://github.com/user-attachments/assets/bca44e20-2026-46c9-8fec-ec2ee19be53f" />

❌ Wrong OTP
<img width="493" height="896" alt="image" src="https://github.com/user-attachments/assets/c2af1660-16fb-4e90-9f84-7d09365b9597" />



⚙️ Setup Instructions
🔹 Backend Setup
cd backend
npm install
cp .env.example .env
npm run dev

🔹 Mobile App Setup
cd mobile-app
npm install
npx expo start


📌 Use Expo Go on a physical Android device for best results.

⚠️ Important Notes

localhost works only for emulator

For physical device, update API base URL with system IP

.env file is ignored for security

OTP is shown only for demo/testing

🧪 Test Scenarios Covered

✔ Correct OTP
✔ Wrong OTP
✔ Already delivered shipment
✔ Missing shipment ID
✔ Missing OTP
✔ Network / server error handling

🏆 Key Learnings & Highlights

Separation of concerns (Controller / Service / Config)

Proper HTTP status code usage

Backend-driven business logic

React Native ↔ Node.js integration

Real-world debugging and edge-case handling





