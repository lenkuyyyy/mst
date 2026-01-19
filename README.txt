# tra_mst_2026 (Extension + License Server)

## 1) Chạy server (bắt buộc để password tự đổi)
Yêu cầu: Node.js 18+

### Cài & chạy local
1. Mở terminal trong thư mục `server/`
2. Chạy:
   - `npm install`
   - (tuỳ chọn) set ENV:
     - `ADMIN_KEY=...`
     - `TELEGRAM_BOT_TOKEN=...`
     - `TELEGRAM_CHAT_ID=...`
   - `npm start`

3. Test: mở `http://localhost:3000/health` thấy `{ ok: true }`.

### Telegram (tuỳ chọn nhưng khuyên dùng)
- Tạo bot qua @BotFather lấy TELEGRAM_BOT_TOKEN
- Lấy chat id (có thể dùng bot @userinfobot hoặc tự log updates)
- Set ENV:
  - TELEGRAM_BOT_TOKEN
  - TELEGRAM_CHAT_ID

Nếu Telegram chưa set, server sẽ in password mới ra console log.

## 2) Deploy server lên HTTPS
Bạn cần deploy server lên domain có HTTPS (Render/Railway/VPS + Nginx, v.v.).

Giả sử domain là: https://YOUR-SERVER-DOMAIN

## 3) Cấu hình extension trỏ về server
Mở file `extension/popup.js` và sửa:
- LICENSE_SERVER_BASE = "https://YOUR-SERVER-DOMAIN"

Mở file `extension/manifest.json` và sửa host_permissions:
- "https://YOUR-SERVER-DOMAIN/*"

## 4) Cài extension
1. Chrome -> chrome://extensions
2. Bật Developer mode
3. Load unpacked -> chọn thư mục `extension/`

## 5) Dùng
- Mở popup extension -> nhập mật khẩu hiện tại (trong server/db.json hoặc /admin/get)
- Nhập đúng -> máy đó được mở khóa vĩnh viễn
- Server sẽ tự rotate password sang 8 ký tự mới và gửi cho chủ sở hữu (Telegram/console)

## 6) Xem / đặt mật khẩu thủ công (Admin)
Gọi API với header `x-admin-key: ADMIN_KEY`

- GET /admin/get
- POST /admin/set  body: { "password":"Abcdef12" }
