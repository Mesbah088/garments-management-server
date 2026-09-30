# 🏭 GarmentsTracker - Garments Order & Production Tracker System (Server API)

High-performance Express.js and MongoDB backend server for the Garments Order & Production Tracker System, featuring JWT authentication, role authorization, tracking timelines, and manufacturing analytics.

---

## 🌐 Live API & Repository Links
- **Live API Endpoint**: `https://your-server-domain.com` (or `http://localhost:5000`)
- **Server GitHub Repository**: `https://github.com/Mesbah088/garments-management-server`
- **Client GitHub Repository**: `https://github.com/Mesbah088/garments-management-client`

---

## 🔑 System Accounts (Admin & Manager)

| Role | Email | Responsibilities |
| :--- | :--- | :--- |
| **Admin** | `admin@garmentstracker.com` | System oversight, role management, suspensions, analytics |
| **Manager** | `manager@garmentstracker.com` | Product catalog publishing, order approvals, milestone tracking |
| **Buyer** | `buyer@garmentstracker.com` | Booking creation, tracking orders, account profile |

---

## 🌟 Key Backend Features

1. **Authentication & Token Management**:
   - `POST /jwt`: Issues 7-day signed JWT token stored in secure HTTP-only cookies and Authorization headers.
   - `POST /logout`: Clears authentication session cookies.

2. **User Management & Role Access (`/users`)**:
   - `GET /users`: Paginated user list with full-text search, role filters, and status filters.
   - `GET /users/:email`: Single user profile fetch.
   - `POST /users`: Upserts registered or Google OAuth users.
   - `PATCH /users/:id/status`: Updates user role & status. If suspending, mandates storing `suspendReason` & `suspendFeedback`.
   - `DELETE /users/:id`: Permanently removes user.

3. **Products API (`/products`)**:
   - `GET /products`: Supports search, category filters, price sorting, home page filtering (`?showOnHome=true`), and pagination.
   - `GET /products/:id`: Fetches product specs, images, video links, and MOQ.
   - `POST /products`: Validates stock, MOQ, and verifies that the creating manager is not suspended.
   - `PUT /products/:id`: Modifies apparel specs and descriptions.
   - `PATCH /products/:id/toggle-home`: Toggles home page highlight visibility.
   - `DELETE /products/:id`: Removes product from inventory.

4. **Orders & Tracking API (`/orders`)**:
   - `GET /orders`: Filter by buyer email, status (`Pending`, `Approved`, `Rejected`, `Cancelled`), or search.
   - `GET /orders/:id`: Full order object with complete tracking timeline.
   - `POST /orders`: Validates buyer suspension status, MOQ, stock availability, and automatically decrements inventory.
   - `PATCH /orders/:id/status`: Manager marks order as `Approved` (logs `approvedAt`) or `Rejected`.
   - `PATCH /orders/:id/cancel`: Allows buyers to cancel pending bookings and automatically restores stock.
   - `POST /orders/:id/tracking`: Appends real-time production milestone updates (`Cutting Completed`, `Sewing Started`, `Finishing`, `QC Checked`, `Packed`, `Shipped / Out for Delivery`).

5. **Analytics Engine (`/stats/admin`)**:
   - Aggregates total products, total orders, total users, active managers, monthly volume, and revenue.
   - Dynamic time-series generator for Bar, Line, and Pie charts across Today, 7-Day, and 30-Day scopes.

---

## 📦 NPM Packages Used (Server)

| Package | Purpose |
| :--- | :--- |
| `express` (v5) | Fast, unopinionated web framework |
| `mongodb` | Official MongoDB native driver |
| `jsonwebtoken` | Secure JSON Web Token creation & verification |
| `cookie-parser` | Cookie header parsing for JWT sessions |
| `cors` | Cross-Origin Resource Sharing with credentials support |
| `dotenv` | Environment variable management |

---

## ⚙️ Environment Configuration (`.env`)

```env
PORT=5000
DB_USER=your_mongodb_username
DB_PASS=your_mongodb_password
MONGODB_URI=mongodb+srv://<username>:<password>@cluster0.mongodb.net/garmentsTrackerDB?retryWrites=true&w=majority
ACCESS_TOKEN_SECRET=garments_production_tracker_secret_key_2026
NODE_ENV=development
```

---

## 🚀 Setup & Execution

```bash
# 1. Clone server repository
git clone https://github.com/your-username/garments-management-server.git

# 2. Install dependencies
cd garments-management-server
npm install

# 3. Start server
npm start
# or with nodemon
node index.js
```
