# 🎂 Happy Birthday Panchw (Interactive Web App) 🐈

เว็บแอปพลิเคชันอวยพรวันเกิดสุดพิเศษที่เขียนขึ้นมาเพื่อคนสำคัญโดยเฉพาะ 🧡 มาพร้อมกับธีมสีส้มที่สดใสและน้องแมวสุดน่ารัก! โปรเจคนี้สร้างด้วย **SvelteKit** และใช้พลังของ **Pure CSS Animations** ในการสร้างลูกเล่น 3D และ Interactive UI โดยไม่ต้องพึ่งพาไลบรารีแอนิเมชันภายนอกเลย เพื่อให้เว็บโหลดเร็วที่สุด!

## ✨ Features (ลูกเล่นในเว็บ)

- 🐱 **3D Cat Loading Screen:** หน้าจอโหลดพร้อมแอนิเมชันกล่องน้องแมว 3D หมุนกลิ้งไปตามเปอร์เซ็นต์การโหลด (Pure CSS 3D Transform)
- 🔐 **Cute Login System:** ระบบยืนยันตัวตนสุดน่ารักที่ต้องกรอก Instagram Username (`panchw_`) ให้ถูกต้องก่อนเข้าชม
- ✏️ **Writing Transition:** หน้าจอเชื่อมผ่าน (Transition) จำลองการเขียนข้อความด้วยดินสอดุ๊กดิ๊ก
- 💌 **Interactive Envelope:** ซองจดหมายอวยพรวันเกิด ที่เมื่อกดคลิกแล้วฝาซองจะพับเปิดออก และดึงการ์ดอวยพรขึ้นมาแสดงแบบสมูทๆ

## 🛠️ Tech Stack

- **Framework:** [SvelteKit](https://kit.svelte.dev/) (Svelte 5)
- **Tooling:** [Vite](https://vitejs.dev/)
- **Styling:** CSS3 (Flexbox, Keyframes Animations, 3D Transforms)
- **Environment:** พัฒนาและทดสอบบน Arch Linux 🐧

## 🚀 Getting Started (วิธีรันโปรเจค)

ถ้าต้องการโคลนโปรเจคนี้ไปรันบนเครื่องของคุณ สามารถทำตามขั้นตอนด้านล่างได้เลย:

### 1. ติดตั้ง Dependencies

เปิด Terminal แล้วเข้าไปที่โฟลเดอร์โปรเจค จากนั้นรันคำสั่ง:

```bash
npm install
```

### 2. รัน Local Development Server

เริ่มเซิร์ฟเวอร์สำหรับทดสอบ:

```bash
npm run dev
```

เซิร์ฟเวอร์จะรันขึ้นมา (ปกติจะอยู่ที่ http://localhost:5173) สามารถเปิดเบราว์เซอร์เพื่อดูผลลัพธ์ได้ทันที

📂 Project Structure (ไฟล์สำคัญ)

- `src/routes/+page.svelte` - โค้ดหลักที่จัดการ State การทำงานทั้งหมด (Loading -> Login -> Transition -> Card)
- `src/routes/layout.css` - ไฟล์ CSS ที่รวม Global Styles และ Animations ทั้งหมดเอาไว้

💖 Credits
Made with love & lots of code. Happy Birthday, Panchw! 🧡
