# RFID-Based Smart Toll Collection System

An IoT-based automated toll collection system using RFID technology, Arduino Uno, Node.js, MongoDB, and Servo Motor. Designed to reduce traffic congestion and manual errors at toll plazas by enabling seamless, cashless, and real-time toll payments.

---

## 📁 Project Structure
```
saimongu007-rfid_acces_control_system/
├── arduino.cpp                # Arduino firmware controlling hardware logic
├── balanceManager.js         # Handles balance deduction & management
├── db-connect.js             # MongoDB connection utility
├── index.html                # Optional UI (if applicable)
├── package.json              # Node.js project metadata
├── script.js                 # Client-side JavaScript
├── server.js                 # Main Node.js server handling RFID and API
├── style.css                 # Styling for web interface
└── data/
    └── balances.json         # Stores card balances (fallback to DB)
```

---

## 📡 Hardware Components
- Arduino Uno
- MFRC522 RFID Reader
- RFID Tags (Cards)
- Servo Motor (Barrier Gate)
- LCD (I2C, 16x2)
- Buzzer
- Jumper Wires & Breadboard

---

## 🚀 Features
- Real-time RFID tag detection
- Balance check and automatic toll deduction
- Gate control with servo motor
- Feedback via LCD display and buzzer
- Backend with REST API for admin use
- MongoDB for transaction & UID logging

---

## 🔧 Installation & Setup
### Backend Setup
1. Clone the repo:
   ```bash
   git clone https://github.com/your-username/saimongu007-rfid_acces_control_system.git
   cd saimongu007-rfid_acces_control_system
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Create a `.env` file:
   ```env
   MONGO_URI=mongodb://localhost:27017/rfid_db
   COM_PORT=COM3
   ```

4. Run the server:
   ```bash
   node server.js
   ```

Ensure Arduino is connected to the COM port specified in `.env`.

### Arduino Setup
1. Upload `arduino.cpp` to the Arduino Uno using the Arduino IDE.
2. Make sure the correct COM port is selected.
3. Power the hardware and monitor the LCD and servo action.

---

## 📘 API Documentation

### Base URL
`http://localhost:3000`

### 1. Get Latest UID
- **URL**: `/api/uid`
- **Method**: `GET`
- **Response**:
```json
{
  "latestUID": {
    "uid": "UID: 4A 3B 2C 1D",
    "timestamp": "2025-04-21T14:05:00.000Z",
    "access": "granted",
    "balance": 40,
    "message": "Access granted. Toll deducted."
  },
  "serialConnected": true
}
```

### 2. Get Scan Logs
- **URL**: `/api/logs`
- **Method**: `GET`
- **Response**: Array of last 50 RFID scan records

### 3. Get All Balances
- **URL**: `/api/balances`
- **Method**: `GET`
- **Response**:
```json
{
  "UID_1": 60,
  "UID_2": 100
}
```

### 4. Get Balance by UID
- **URL**: `/api/balance/:uid`
- **Method**: `GET`
- **Response**:
```json
{
  "uid": "4A3B2C1D",
  "balance": 60
}
```

### 5. Add Balance
- **URL**: `/api/balance/add`
- **Method**: `POST`
- **Body**:
```json
{
  "uid": "4A3B2C1D",
  "amount": 50
}
```
- **Response**:
```json
{
  "uid": "4A3B2C1D",
  "balance": 110,
  "message": "Balance added successfully"
}
```

### 6. Get Toll Amount
- **URL**: `/api/toll`
- **Method**: `GET`
- **Response**:
```json
{
  "amount": 10
}
```

### Error Format
```json
{
  "error": "Error message describing the issue."
}
```

---

## 🧠 Notes
- Ensure the `.env` file contains correct `MONGO_URI` and `COM_PORT`
- MongoDB must be running locally or on cloud
- Server listens to serial data from Arduino and responds accordingly
- RFID logs are stored in `rfid_logs` collection in MongoDB
- Balances are handled through both `balances.json` and MongoDB

---

## 🧪 Future Enhancements
- Add user-facing dashboard with login/authentication
- SMS/Email notifications on successful toll deduction
- Vehicle type-based dynamic toll rates
- Cloud-based remote admin panel

---

## 📄 License
This project is open-source and free to use for educational purposes.

---

## 🙌 Credits
Developed by *Badhan Das* , *Saimongu Marma* & *Prantika Chowdhury*  
IoT Based Project Development (CSE 342)  
East Delta University, Bangladesh

