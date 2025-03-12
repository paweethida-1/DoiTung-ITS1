# DoiTung-ITS1

# 🛠️ Web Issue Tracking System

A full-stack **Issue Tracking System** with:
- **Frontend:** Next.js (Admin Dashboard)
- **Backend:** Golang (Gin Framework)
- **Mobile:** React Native (User App)
- **Database:** MySQL

## 🚀 Features
- **Admin Dashboard** (View & manage issues)
- **REST API** (Golang backend using Gin)
- **Mobile App** (Users report & track issues)
- **Database** (MySQL for data storage)

---

## 🏗️ Project Structure

📌 1. สร้างโฟลเดอร์โปรเจคหลัก
sh
คัดลอก
แก้ไข
mkdir my-project && cd my-project
📂 โครงสร้างหลังจากสร้างโฟลเดอร์

perl
คัดลอก
แก้ไข
my-project/
🚀 2. สร้าง Backend (Golang)
sh
คัดลอก
แก้ไข
mkdir backend && cd backend
go mod init backend
go get -u github.com/gin-gonic/gin
สร้าง main.go

go
คัดลอก
แก้ไข
package main

import (
    "backend/routes"
    "github.com/gin-gonic/gin"
)

func main() {
    r := gin.Default()
    routes.SetupRoutes(r)
    r.Run(":8080")
}
สร้าง routes/routes.go

go
คัดลอก
แก้ไข
package routes

import (
    "backend/controllers"
    "github.com/gin-gonic/gin"
)

func SetupRoutes(r *gin.Engine) {
    r.GET("/ping", controllers.Ping)
}
สร้าง controllers/ping_controller.go

go
คัดลอก
แก้ไข
package controllers

import (
    "net/http"
    "github.com/gin-gonic/gin"
)

func Ping(c *gin.Context) {
    c.JSON(http.StatusOK, gin.H{"message": "pong"})
}
✅ รัน Backend
sh
คัดลอก
แก้ไข
go run main.go
ทดสอบ API:

sh
คัดลอก
แก้ไข
curl http://localhost:8080/ping
🖥 3. สร้าง Dashboard (Next.js)
sh
คัดลอก
แก้ไข
cd ../
npx create-next-app@latest dashboard
cd dashboard
npm install
แก้ไข pages/index.tsx

tsx
คัดลอก
แก้ไข
import { useEffect, useState } from "react";

export default function Home() {
  const [message, setMessage] = useState("");

  useEffect(() => {
    fetch("http://localhost:8080/ping")
      .then((res) => res.json())
      .then((data) => setMessage(data.message));
  }, []);

  return (
    <div>
      <h1>Dashboard</h1>
      <p>API Response: {message}</p>
    </div>
  );
}
✅ รัน Dashboard
sh
คัดลอก
แก้ไข
npm run dev
เปิดเว็บที่ http://localhost:3000

📱 4. สร้าง User App (React Native)
sh
คัดลอก
แก้ไข
cd ../
npx react-native init userApp
cd userApp
สร้าง src/api/api.ts

tsx
คัดลอก
แก้ไข
export const fetchPing = async () => {
    const res = await fetch("http://localhost:8080/ping");
    return await res.json();
};
แก้ไข App.tsx

tsx
คัดลอก
แก้ไข
import React, { useEffect, useState } from "react";
import { View, Text } from "react-native";
import { fetchPing } from "./src/api/api";

const App = () => {
    const [message, setMessage] = useState("");

    useEffect(() => {
        fetchPing().then((data) => setMessage(data.message));
    }, []);

    return (
        <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}>
            <Text>User App</Text>
            <Text>API Response: {message}</Text>
        </View>
    );
};

export default App;
✅ รันแอป
sh
คัดลอก
แก้ไข
npx react-native run-android   # สำหรับ Android
npx react-native run-ios       # สำหรับ iOS
📌 โครงสร้างสุดท้าย
perl
คัดลอก
แก้ไข
my-project/
│── backend/         # Golang REST API
│   ├── main.go
│   ├── routes/
│   ├── controllers/
│
│── dashboard/       # Next.js (Admin Dashboard)
│   ├── pages/
│   ├── components/
│
│── user-app/        # React Native (User App)
│   ├── src/
│   │   ├── api/
│   │   ├── screens/
│   ├── App.tsx
🎯 สรุป
Backend (Golang)

/ping API
รันด้วย go run main.go
Dashboard (Next.js)

Fetch API /ping
รันด้วย npm run dev
User App (React Native)

Fetch API /ping
รันด้วย npx react-native run-android


✅ สรุปคำสั่งที่ต้องใช้
sh
คัดลอก
แก้ไข
# สร้างโฟลเดอร์โปรเจค
mkdir my-project && cd my-project

# Backend (Golang)
mkdir backend && cd backend
go mod init backend
go get -u github.com/gin-gonic/gin
touch main.go
mkdir routes controllers
touch routes/routes.go controllers/ping_controller.go
go run main.go

# Dashboard (Next.js)
cd ../
npx create-next-app@latest dashboard
cd dashboard
npm install
npm run dev

# User App (React Native)
cd ../
npx react-native init userApp
cd userApp
npx react-native run-android  # หรือ npx react-native run-ios
