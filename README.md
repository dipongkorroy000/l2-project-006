### Parcel Delivery Web Application

This project is a **Parcel Delivery Application** where users can create accounts to send and receive parcels.  
Delivery agents must meet certain requirements to register, and customers can book them for secure and timely deliveries.  
The system manages parcel tracking, pickup requests, and delivery confirmations, making the process smooth and reliable for both senders and receivers.A unique feature allows **receivers to claim parcels using just their phone number**, with or without a website account.

---

#### 🛠 Tech Stack

- **Backend**

  - **Node.js** → Server-side runtime for building scalable APIs
  - **Express.js** → Web framework for routing and middleware
  - **MongoDB** → Database for storing users, parcels, and delivery records
  - **Mongoose** → ODM for managing MongoDB models
  - **SSLCommerz/Payment Gateway** → (if integrated) for handling delivery payments

- **Frontend**
  - **React** → Client-side UI for customers and delivery agents
  - **Redux** → State management for authentication, parcel tracking, and real-time updates
  - **TailwindCSS** → Styling and responsive design

---

#### 🔗 Roles & Features

- **Sender**
  - Create an account and log in securely
  - Book delivery agents for parcel pickup and delivery
  - Track parcels in real time
  - Receive delivery confirmations
  - Provide receiver's phone number during booking

- **Receiver**
  - **No account required** → Receive parcel using only phone number verification
  - Can optionally create an account to view delivery history
  - Receive SMS notifications with tracking links
  - Confirm parcel receipt with OTP (One-Time Password)

- **Admin**
  - Manage users (senders and delivery agents)
  - **Update parcel status** (pending, picked up, in transit, out for delivery, delivered)
  - Monitor all deliveries and system activity
  - Handle disputes or issues

---

#### 🔐 Authentication Flow

1. **Sender/Admin/Agent** registers with email/password; password is hashed using **bcrypt** before storage.  
2. Upon login, server validates credentials and generates a **JWT**.  
3. Client stores the JWT and includes it in subsequent API requests.  
4. Backend verifies the JWT and assigns role (Sender, Agent, Admin) for access control.  
5. **Receiver authentication** is handled via phone number and OTP, no JWT required for basic claiming.

---

#### 📦 Parcel Management Flow

1. **Sender** creates a new parcel delivery request with receiver's name and phone number (stored in **MongoDB** via **Mongoose**).  
2. **Admin** reviews and assigns a delivery agent, or **Agent** accepts the request.  
3. **Admin** updates parcel status during transit (picked up → in transit → out for delivery).  
4. **Receiver** receives SMS notification with tracking link when parcel is out for delivery.  
5. **Receiver claims parcel**:
   - **With account**: Log in and confirm receipt
   - **Without account**: Enter phone number, receive OTP, verify, and confirm receipt
6. Upon confirmation, **Admin** marks parcel as delivered and system updates record.

---

#### 💳 Payment Flow (SSLCommerz)

1. During checkout, **Sender** selects SSLCommerz as payment method.  
2. Backend creates a payment session and redirects to SSLCommerz gateway.  
3. Sender completes payment on SSLCommerz hosted page.  
4. SSLCommerz sends confirmation webhook to backend.  
5. Backend verifies payment and updates order status accordingly.  

---

#### 📊 Benefits of This System

- **Security** → JWT with bcrypt hashing ensures robust authentication and data protection.
- **Reliability** → Real-time parcel tracking and status updates
- **Scalability** → Mongoose + MongoDB handle large numbers of users and parcels
- **Transparency** → Customers and agents can monitor delivery progress

---

#### ✅ Summary

- Built with **Express.js**, **Mongoose**, **MongoDB**, **React**, **Redux**, and more modern tools
- Supports three roles: **Sender**, **Receiver**, **Admin**
- Provides secure authentication, parcel tracking, and delivery confirmations
- Ensures smooth and reliable parcel delivery workflow

---

#### 🚀 Future Improvements

- Add push notifications for parcel status updates
- Implement rating/review system for delivery agents
- Enhance admin dashboard with analytics and reporting
