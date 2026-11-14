# NeXora Backend

The backend service powering **NeXora**, a developer networking platform that helps developers connect, collaborate, and grow.

Built with Node.js, Express.js, and MongoDB, it provides REST APIs, authentication, connection management, real-time messaging, file uploads, and premium subscriptions.

## Repositories

- **Frontend:** [NeXora Frontend](https://github.com/143sumit05/NeXora-frontend)
- **Backend:** [NeXora Backend](https://github.com/143sumit05/NeXora-backend)
- **Main Project:** [NeXora](https://github.com/143sumit05/NeXora)

## Tech Stack

| Technology | Purpose |
|---|---|
| Node.js | JavaScript runtime |
| Express.js | Backend framework |
| MongoDB | NoSQL database |
| Mongoose | Database modeling |
| JWT | Authentication |
| bcrypt | Password hashing |
| Socket.IO | Real-time communication |
| Cloudinary | Image storage |
| Multer | File upload handling |
| Razorpay | Payment integration |
| AWS SES | Email notifications |

## Features

- User registration, login, and logout
- JWT-based authentication
- Secure password hashing
- Developer profile management
- Profile photo uploads
- Developer discovery and feed
- Connection requests and management
- Real-time messaging using Socket.IO
- Premium subscription payments through Razorpay
- Razorpay webhook handling and payment status updates
- Email notifications using AWS SES

## Project Structure

```text
NeXora-backend/
│
├── src/
│   ├── config/
│   │   ├── cloudinary.js
│   │   └── database.js
│   │
│   ├── middlewares/
│   │   ├── auth.js
│   │   └── upload.js
│   │
│   ├── models/
│   │   ├── user.js
│   │   ├── connectionRequest.js
│   │   ├── message.js
│   │   ├── payment.js
│   │   └── webhookEvent.js
│   │
│   ├── routes/
│   │   ├── authRouter.js
│   │   ├── profileRouter.js
│   │   ├── requestRouter.js
│   │   ├── userRoute.js
│   │   ├── messageRouter.js
│   │   ├── paymentRouter.js
│   │   └── uploadRouter.js
│   │
│   ├── utils/
│   │   ├── sendEmails.js
│   │   ├── socket.js
│   │   └── validate.js
│   │
│   └── app.js
│
├── scripts/
├── .gitignore
├── package.json
└── README.md
```

## API Endpoints

All routes are mounted at the root (`/`).

### Authentication

| Method | Endpoint | Description |
|---|---|---|
| POST | `/signup` | Register a new user |
| POST | `/login` | Login |
| POST | `/logout` | Logout |

### Profile

| Method | Endpoint | Description |
|---|---|---|
| GET | `/profile` | Get logged-in user's profile |
| PATCH | `/profile/edit` | Update profile |
| PATCH | `/profile/edit/password` | Change password |

### Developer Feed & Connections

| Method | Endpoint | Description |
|---|---|---|
| GET | `/feed` | Discover developers |
| POST | `/request/:status/:toUserId` | Send a connection request |
| PATCH | `/recieve/:status/:requestId` | Review a connection request |
| GET | `/user/pendingRequest` | Get pending requests |
| GET | `/user/connections` | Get accepted connections |

Supported request statuses: `interested`, `ignored`, `accepted`, `rejected`.

### Messaging

| Method | Endpoint | Description |
|---|---|---|
| GET | `/messages/:userId` | Retrieve conversation messages |

Real-time communication is handled through Socket.IO.

### Payments

| Method | Endpoint | Description |
|---|---|---|
| POST | `/payment/create-order` | Create a Razorpay order |
| POST | `/payment/verify` | Verify payment |
| POST | `/payment/webhook` | Handle Razorpay webhook events |

### File Uploads

| Method | Endpoint | Description |
|---|---|---|
| POST | `/upload/profile-photo` | Upload a profile photo |

## Database Models

The application uses MongoDB with Mongoose schemas.

- **User:** Stores account details, profile information, skills, and premium subscription status.
- **ConnectionRequest:** Stores sender, receiver, and request status.
- **Message:** Stores sender, receiver, conversation ID, and message content.
- **Payment:** Stores Razorpay order details, payment ID, amount, currency, and payment status.
- **WebhookEvent:** Stores processed webhook event IDs to help prevent duplicate event processing.

## Payment Flow

1. The frontend requests an order from the backend.
2. The backend creates a Razorpay order and stores its payment record.
3. The user completes checkout through Razorpay.
4. The frontend sends payment details for verification.
5. The backend verifies the payment.
6. Razorpay webhook events are validated using an HMAC signature.
7. Successful payment events update the payment and user's premium status.
8. Webhook event IDs are stored to support duplicate-event handling.

## Environment Variables

Create a `.env` file in the project root.

```env
PORT=3000
NODE_ENV=development

FRONTEND_URL=

MONGODB_URI=
JWT_SECRET=

CLOUDINARY_CLOUD_NAME=
CLOUDINARY_API_KEY=
CLOUDINARY_API_SECRET=

RAZORPAY_KEY_ID=
RAZORPAY_KEY_SECRET=
RAZORPAY_WEBHOOK_SECRET=

AWS_REGION=
AWS_ACCESS_KEY_ID=
AWS_SECRET_ACCESS_KEY=
SES_FROM_EMAIL=
```

Add your own credentials. Never commit your `.env` file or expose secret keys publicly.

## Installation & Setup

**1. Clone the repository**

```bash
git clone https://github.com/143sumit05/NeXora-backend.git
cd NeXora-backend
```

**2. Install dependencies**

```bash
npm install
```

**3. Configure environment variables**

Create a `.env` file and add the required credentials.

**4. Start the server**

```bash
npm start
```

The server runs on port `3000` by default, unless another port is configured.

For development:

```bash
npm run dev
```

## Scripts

| Command | Description |
|---|---|
| `npm start` | Start the backend server |
| `npm run dev` | Start with Nodemon |

## Author

**Sumit Dhiman**

[GitHub Profile](https://github.com/143sumit05)