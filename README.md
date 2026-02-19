[README.md](https://github.com/user-attachments/files/25407376/README.md)
# GY Salon - Complete Booking System with AI Consultant

ระบบจองคิวและบริหารจัดการร้านเสริมสวยครบวงจร พร้อม AI Consultant

## 🌟 Features

### สำหรับลูกค้า (Customer Portal)
- ✅ ลงทะเบียน/เข้าสู่ระบบ
- ✅ เลือกบริการ/ช่าง/เวลา (Real-time availability)
- ✅ อัพโหลดสลิปชำระเงิน
- ✅ ติดตามสถานะการจองผ่าน Line
- ✅ ดูประวัติการใช้บริการ

### AI Consultant 🤖
- 📸 อัพโหลดรูปหน้าเพื่อรับคำแนะนำ
- 💡 Gemini AI วิเคราะห์ใบหน้าและแนะนำทรงผม/สีผม
- 📝 บันทึกประวัติการปรึกษา
- 🎯 แนะนำบริการที่เหมาะสมจากร้าน

### สำหรับร้านค้า (Admin)
- 📊 Dashboard สรุปรายวัน/สัปดาห์/เดือน
- ✅ อนุมัติ/ปฏิเสธคิว พร้อมเหตุผล
- 📅 ดูคิวรายวัน พร้อมสถานะ
- 📈 รายงานรายได้และสถิติ

### ระบบ CRM
- 👤 ฐานข้อมูลลูกค้าครบวงจร
- 💇 บันทึกสภาพผม, นิสัย, การแพ้
- 📸 ระบบ Before/After Photos
- 📝 ประวัติการให้บริการย้อนหลัง

### Line Integration
- 💬 แจ้งเตือนสถานะการจอง
- 🤖 Chatbot ตอบคำถามเบื้องต้น
- 📱 ตรวจสอบคิวผ่าน Line

---

## 🗄️ Database Schema

### 1. Bookings (การจอง)
```
OrderID | Date | Time | StaffID | CustomerName | Phone
ServiceID | ServiceName | Design | Addons | Duration | Details
Location | Address | Price | Status | SlipURL | Timestamp
CustomerID | ApprovedBy | ApprovedAt | Notes
```

### 2. Customers (CRM)
```
CustomerID | Phone | Name | Password | LineUserID
Birthday | HairType | HairCondition | Allergies | Preferences
History | TotalVisits | TotalSpent | LastVisit | Notes
CreatedAt | UpdatedAt
```

### 3. Staffs (ช่าง)
```
StaffID | Name | Nickname | Specialties | Bio | ImageURL
Active | Rating | ReviewCount | WorkingDays | WorkingHours
```

### 4. Services (บริการ)
```
ServiceID | Name | Category | Price | Duration
Description | ImageURL | Active | SuitableFor
```

### 5. AIConsultations (ประวัติ AI)
```
ConsultationID | CustomerID | Date | Question | PhotoURL
Recommendations | SuggestedServices | RawResponse
```

---

## 🚀 Setup Instructions

### 1. Google Sheets Setup
```javascript
// แก้ไข SHEET_ID ใน Code.gs
const CONFIG = {
  SHEET_ID: 'YOUR_SHEET_ID_HERE'
};
```

### 2. Gemini API Setup
1. ไปที่ https://makersuite.google.com/app/apikey
2. สร้าง API Key
3. ใส่ใน CONFIG:
```javascript
GEMINI_API_KEY: 'YOUR_GEMINI_API_KEY'
```

### 3. Line Official Account Setup
1. สร้าง Line Official Account
2. ไปที่ https://developers.line.biz/
3. สร้าง Messaging API Channel
4. คัดลอก Channel Access Token และ Channel Secret
5. ใส่ใน CONFIG

### 4. Deploy Web App
1. ใน Apps Script Editor: Deploy → New deployment
2. Type: Web app
3. Execute as: Me
4. Access: Anyone
5. คัดลอก Web App URL

### 5. Initial Setup
```javascript
// รัน function นี้ 1 ครั้งใน Apps Script Editor
initialSetup()
```

---

## 📱 API Endpoints

### Customer API
| Endpoint | Method | Description |
|----------|--------|-------------|
| `customerRegister` | POST | ลงทะเบียน |
| `customerLogin` | POST | เข้าสู่ระบบ |
| `getServices` | GET | ดูรายการบริการ |
| `getStaffs` | GET | ดูรายชื่อช่าง |
| `getAvailableSlots` | GET | เช็คเวลาว่าง |
| `createBooking` | POST | สร้างการจอง |
| `uploadPaymentSlip` | POST | อัพโหลดสลิป |
| `getMyBookings` | POST | ดูประวัติจอง |
| `cancelBooking` | POST | ยกเลิกคิว |

### AI Consultant API
| Endpoint | Method | Description |
|----------|--------|-------------|
| `aiAnalyzePhoto` | POST | วิเคราะห์รูปด้วย AI |
| `getAIRecommendation` | POST | ขอคำแนะนำ AI |
| `getConsultationHistory` | POST | ประวัติการปรึกษา |

### Admin API
| Endpoint | Method | Description |
|----------|--------|-------------|
| `adminLogin` | POST | เข้าสู่ระบบ |
| `getAdminDashboard` | POST | Dashboard ข้อมูล |
| `getPendingApprovals` | GET | คิวรออนุมัติ |
| `approveBooking` | POST | อนุมัติคิว |
| `rejectBooking` | POST | ปฏิเสธคิว |
| `startService` | POST | เริ่มให้บริการ |
| `completeService` | POST | เสร็จสิ้น |

### CRM API
| Endpoint | Method | Description |
|----------|--------|-------------|
| `getCustomers` | POST | รายชื่อลูกค้า |
| `getCustomerProfile` | POST | โปรไฟล์ลูกค้า |
| `updateCustomerProfile` | POST | อัพเดทข้อมูล |
| `addServiceRecord` | POST | บันทึกการให้บริการ |
| `getServiceRecords` | POST | ประวัติการบริการ |

### Reporting API
| Endpoint | Method | Description |
|----------|--------|-------------|
| `getRevenueReport` | POST | รายงานรายได้ |
| `getStaffPerformance` | POST | ผลงานช่าง |
| `getDailySummary` | POST | สรุปรายวัน |

---

## 🤖 AI Consultant Usage

### Example: วิเคราะห์รูปหน้า
```javascript
{
  "action": "aiAnalyzePhoto",
  "customerId": "CUST-001",
  "imageBase64": "data:image/jpeg;base64,...",
  "question": "อยากได้ทรงผมที่เหมาะกับหน้า"
}
```

### Response
```json
{
  "status": "success",
  "analysis": "รูปหน้าเป็นแบบรี มีโหนกแก้มสูง...",
  "recommendations": [
    "ทรงผมซอยสไลด์ระดับคาง...",
    "สีผมโทนอุ่น เช่น ช็อกโกแลต..."
  ],
  "suggestedServices": [
    "ตัดผมสไตล์เกาหลี",
    "ทำสีผมโทนอุ่น"
  ],
  "hairCareTips": "ควรใช้แชมพูสูตรอ่อนโยน..."
}
```

---

## 💬 Line Bot Commands

ลูกค้าสามารถพิมพ์ใน Line:
- `สถานะคิว` - ตรวจสอบคิวล่าสุด
- `จอง` - ลิงก์ไปหน้าจอง
- `ติดต่อร้าน` - ข้อมูลติดต่อ

---

## 📊 Booking Status Flow

```
รอชำระเงิน → แจ้งชำระแล้ว → ยืนยันแล้ว → กำลังให้บริการ → เสร็จสิ้น
                ↓
            ยกเลิก / ไม่มาตามนัด
```

---

## 🔐 Security

- รหัสผ่าน Hash ด้วย SHA-256
- Lock Service ป้องกัน Race Condition
- สลิปเงินอัพโหลดไป Google Drive (Private)
- Token-based Authentication

---

## 🛠️ Customization

### เพิ่มบริการใหม่
```javascript
// ใน Sheet Services
ServiceID: S004
Name: สปาผม
Category: บำรุง
Price: 1200
Duration: 90
```

### ปรับเวลาทำการ
```javascript
// ใน Sheet Settings
Key: businessHours
Value: 10:00-20:00
```

### ตั้งค่า Gemini Prompt
แก้ไขฟังก์ชัน `aiAnalyzePhoto()` ใน Code.gs

---

## 📞 Support

มีปัญหาการใช้งานติดต่อ:
- Email: support@gysalon.com
- Line: @gysalon
- โทร: 081-234-5678

---

## 📝 License

MIT License - ใช้งานฟรี แก้ไขได้ตามต้องการ

---

## 🙏 Credits

- Google Apps Script
- Gemini AI by Google
- Line Messaging API
- Tailwind CSS
- Font Awesome

**สร้างด้วย ❤️ สำหรับ GY Salon**
