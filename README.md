# RESTful API Design – Room Booking System

## Base URL
/api

yaml
คัดลอกโค้ด

---

## 1. Rooms (ห้องประชุม)

### Get All Rooms
GET /api/rooms

yaml
คัดลอกโค้ด
ดึงรายการห้องประชุมทั้งหมด

**Status Code**
- 200 OK

---

### Get Room by ID
GET /api/rooms/:id

yaml
คัดลอกโค้ด
ดึงข้อมูลห้องประชุมเพียงห้องเดียว

**Status Code**
- 200 OK
- 404 Not Found

---

### Create Room
POST /api/rooms

css
คัดลอกโค้ด
สร้างห้องประชุมใหม่ (เฉพาะเจ้าหน้าที่)

**Request Body**
```json
{
  "roomname": "Meeting Room A",
  "capacity": 20,
  "location": "Building A",
  "status": "available"
}
Status Code

201 Created

403 Forbidden

Update Room
bash
คัดลอกโค้ด
PUT /api/rooms/:id
แก้ไขข้อมูลห้องประชุม (เฉพาะเจ้าหน้าที่)

Request Body

json
คัดลอกโค้ด
{
  "roomname": "Meeting Room A",
  "capacity": 25,
  "location": "Building A",
  "status": "available"
}
Status Code

200 OK

404 Not Found

Delete Room
bash
คัดลอกโค้ด
DELETE /api/rooms/:id
ลบห้องประชุม (เฉพาะเจ้าหน้าที่)

Status Code

204 No Content

404 Not Found

2. Bookings (การจอง)
Get All Bookings
bash
คัดลอกโค้ด
GET /api/bookings
ดึงรายการการจองทั้งหมด (เจ้าหน้าที่)

Status Code

200 OK

Get My Bookings
bash
คัดลอกโค้ด
GET /api/bookings/my
ดึงรายการการจองของผู้ใช้ที่ login อยู่

Status Code

200 OK

401 Unauthorized

Create Booking
bash
คัดลอกโค้ด
POST /api/bookings
สร้างการจองห้องใหม่

Request Body

json
คัดลอกโค้ด
{
  "room_id": 1,
  "booking_date": "2026-02-01",
  "start_time": "09:00",
  "end_time": "11:00",
  "purpose": "Project Meeting"
}
Status Code

201 Created

409 Conflict (เวลาจองซ้อน)

Cancel Booking
bash
คัดลอกโค้ด
DELETE /api/bookings/:id
ยกเลิกการจอง (เจ้าของการจองหรือเจ้าหน้าที่)

Status Code

204 No Content

403 Forbidden

Approve Booking
bash
คัดลอกโค้ด
PATCH /api/bookings/:id/approve
อนุมัติการจอง (เฉพาะเจ้าหน้าที่)

Request Body

json
คัดลอกโค้ด
{
  "status": "approved"
}
Status Code

200 OK

403 Forbidden

3. Authentication & Users
Login
bash
คัดลอกโค้ด
POST /api/auth/login
Request Body

json
คัดลอกโค้ด
{
  "username": "user01",
  "password": "123456"
}
Response

json
คัดลอกโค้ด
{
  "access_token": "jwt_token"
}
Status Code

200 OK

401 Unauthorized

Register
arduino
คัดลอกโค้ด
POST /api/auth/register
Request Body

json
คัดลอกโค้ด
{
  "username": "user01",
  "password": "123456",
  "full_name": "Somchai Jaidee",
  "email": "somchai@email.com"
}
Status Code

201 Created

Get User Profile
bash
คัดลอกโค้ด
GET /api/users/profile
ดูข้อมูลผู้ใช้ของตนเอง

Status Code

200 OK

401 Unauthorized

4. HTTP Status Codes Summary
Status Code	Description
200	OK
201	Created
204	No Content
401	Unauthorized
403	Forbidden
404	Not Found
409	Conflict
