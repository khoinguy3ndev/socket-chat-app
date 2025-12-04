# WebSocket Chat Application

Ứng dụng chat thời gian thực được xây dựng với Node.js, Express, WebSocket và MongoDB.

## 🚀 Tính năng

- **Đăng ký / Đăng nhập** - Xác thực người dùng với JWT
- **Chat thời gian thực** - Sử dụng WebSocket để gửi/nhận tin nhắn tức thì
- **Quên mật khẩu** - Reset mật khẩu qua email
- **Đổi mật khẩu** - Người dùng có thể thay đổi mật khẩu
- **Quản lý người dùng** - CRUD operations cho user (Admin)
- **Lịch sử tin nhắn** - Lưu trữ và truy xuất lịch sử chat

## 🛠️ Công nghệ sử dụng

- **Backend**: Node.js, Express 5
- **Database**: MongoDB với Mongoose
- **Real-time**: WebSocket (ws)
- **Authentication**: JWT (JSON Web Token)
- **Password Hashing**: bcryptjs
- **Email**: Nodemailer
- **Frontend**: HTML, CSS, JavaScript (Vanilla)

## 📁 Cấu trúc thư mục

```
websocket-chat/
├── public/                 # Frontend files
│   ├── html/              # HTML pages
│   │   ├── index.html     # Trang đăng nhập
│   │   ├── register.html  # Trang đăng ký
│   │   ├── chat.html      # Trang chat chính
│   │   ├── change-password.html
│   │   └── forgot-reset.html
│   ├── js/                # JavaScript files
│   │   ├── auth.js
│   │   ├── chat.js
│   │   ├── change-password.js
│   │   └── forgot.js
│   └── styles/            # CSS files
│       ├── main.css
│       ├── login.css
│       ├── chat.css
│       └── forgot.css
├── src/                   # Backend source code
│   ├── app.js            # Entry point
│   ├── config/
│   │   └── db.config.js  # MongoDB configuration
│   ├── controllers/      # Route controllers
│   │   ├── auth.controller.js
│   │   ├── message.controller.js
│   │   └── user.controller.js
│   ├── handler/          # Error & response handlers
│   │   ├── error-handler.js
│   │   ├── error-response.js
│   │   └── success-response.js
│   ├── middleware/       # Express middleware
│   │   ├── asyncHandle.js
│   │   └── authMiddleware.js
│   ├── models/           # Mongoose models
│   │   ├── message.model.js
│   │   └── user.model.js
│   ├── routes/           # API routes
│   │   ├── auth.route.js
│   │   ├── message.route.js
│   │   └── user.route.js
│   ├── services/         # Business logic
│   │   ├── auth.service.js
│   │   ├── message.service.js
│   │   └── user.service.js
│   └── ws/
│       └── websocket.js  # WebSocket setup
├── package.json
└── .env
```

## ⚙️ Cài đặt

### Yêu cầu

- Node.js >= 18.x
- MongoDB
- npm hoặc yarn

### Các bước cài đặt

1. **Clone repository**
   ```bash
   git clone https://github.com/khoinguyen2010hihihi/SocketChatDemo.git
   cd websocket-chat
   ```

2. **Cài đặt dependencies**
   ```bash
   npm install
   ```

3. **Tạo file .env**
   ```env
   PORT=9000
   MONGODB_URI=mongodb://localhost:27017/chatRealtime
   JWT_SECRET=your_jwt_secret_key
   JWT_SECRET_KEY=your_jwt_secret_key
   SMTP_HOST=smtp.gmail.com
   SMTP_PORT=587
   SMTP_USER=your_email@gmail.com
   SMTP_PASS=your_app_password
   ```

4. **Khởi động MongoDB**
   ```bash
   mongod
   ```

5. **Chạy ứng dụng**
   ```bash
   # Development mode (với nodemon)
   npm run dev

   # Production mode
   npm start
   ```

6. **Truy cập ứng dụng**
   - Mở trình duyệt và truy cập: `http://localhost:9000`

## 📚 API Endpoints

### Authentication (`/auth`)

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| POST | `/auth/register` | Đăng ký tài khoản mới |
| POST | `/auth/login` | Đăng nhập |
| POST | `/auth/logout` | Đăng xuất |
| POST | `/auth/refresh-token` | Làm mới token |
| POST | `/auth/forgot-password` | Yêu cầu reset mật khẩu |
| POST | `/auth/reset-password` | Reset mật khẩu |
| POST | `/auth/change-password` | Đổi mật khẩu (cần auth) |

### User (`/user`)

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| POST | `/user/create` | Tạo user mới |
| GET | `/user/me` | Lấy thông tin user hiện tại |
| PUT | `/user/updateMe` | Cập nhật thông tin cá nhân |
| GET | `/user/getAll` | Lấy danh sách tất cả users |
| GET | `/user/:id` | Lấy thông tin user theo ID |
| PUT | `/user/:id` | Cập nhật user theo ID |
| DELETE | `/user/:id` | Xóa user (Admin only) |

### Message (`/message`)

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| GET | `/message/:receiverId` | Lấy lịch sử tin nhắn với user |

## 🔌 WebSocket

### Kết nối WebSocket

```javascript
const ws = new WebSocket(`ws://localhost:9000?token=${accessToken}`);
```

### Gửi tin nhắn

```javascript
ws.send(JSON.stringify({
  to: 'receiverUserId',
  content: 'Nội dung tin nhắn'
}));
```

### Nhận tin nhắn

```javascript
ws.onmessage = (event) => {
  const data = JSON.parse(event.data);
  // data: { fromId, fromUsername, content, timestamp }
};
```

## 📝 Scripts

```bash
# Chạy development server với hot reload
npm run dev

# Chạy production server
npm start

# Seed dữ liệu mẫu
npm run seed
```

## 🔐 Bảo mật

- Mật khẩu được hash bằng bcrypt với salt rounds = 10
- JWT được sử dụng cho authentication
- CORS được cấu hình để chỉ cho phép các origin được chỉ định
- WebSocket connection yêu cầu valid JWT token

## 📄 License

ISC

## 👤 Tác giả

- GitHub: [@khoinguyen2010hihihi](https://github.com/khoinguyen2010hihihi)
