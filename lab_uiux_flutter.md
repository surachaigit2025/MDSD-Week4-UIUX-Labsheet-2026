# 📱 ใบงานปฏิบัติที่ 3: UI/UX Design — จาก Mockup สู่ Flutter

> **วิชา:** การพัฒนาซอฟต์แวร์สำหรับอุปกรณ์เคลื่อนที่  
> **สัปดาห์ที่:** 3  
> **เวลา:** 3.5 ชั่วโมง  
> **คะแนน:** 20 คะแนน (เป็นส่วนหนึ่งของ Lab รายสัปดาห์)

---

## 🎯 วัตถุประสงค์การเรียนรู้

หลังจากทำใบงานนี้แล้ว นักศึกษาจะสามารถ:

1. อธิบายหลักการ Material Design 3 และนำไปใช้ออกแบบได้
2. สร้าง UI Mockup ด้วย Figma โดยใช้ Material Design 3 Component
3. วิเคราะห์ Design และแปลงเป็น Widget Tree ใน Flutter ได้
4. สร้าง Reusable Widget ด้วย Flutter ตามหลัก Component-Driven Design
5. ใช้ AI (Google AI Studio) ช่วยสร้าง UI Component ได้

---

## 📚 ทฤษฎีก่อนการทดลอง (อ่านมาก่อนเข้าคาบ)

> **หมายเหตุเรื่องเวลา:** ส่วนทฤษฎีด้านล่างนี้ให้อ่านล่วงหน้าก่อนเข้าคาบเรียน ไม่นับรวมในเวลา 3.5 ชั่วโมง เวลาในคาบทั้งหมดคือ การทดลอง 5 ส่วน (20+55+55+30+20 = 180 นาที) รวมกับเวลาสรุปและส่งงาน 30 นาที รวม 210 นาที (3.5 ชั่วโมง) พอดี

### ส่วนที่ 1: Material Design 3 (ทบทวนก่อนลงมือ)

Material Design 3 (Material You) คือ Design System ของ Google เวอร์ชันล่าสุด (2021–ปัจจุบัน) มีหลักการสำคัญ 3 ด้าน:

#### 1.1 Dynamic Color System

Material 3 สร้าง Color Scheme อัตโนมัติจากสี seed สีเดียว โดยแบ่งเป็น **Tonal Palettes:**

```
Primary    → ใช้กับ action หลัก, FAB, Checkbox ที่เลือกแล้ว
Secondary  → ใช้กับ filter chip, secondary action
Tertiary   → accent พิเศษ เพื่อสร้าง contrast
Error      → ข้อผิดพลาด, validation
Neutral    → surface, background, outline
```

แต่ละ role มีทั้ง **Container** (พื้นหลัง) และ **On-Container** (ตัวอักษร/icon ที่วางบน container นั้น) เช่น:
- `Primary` = สีปุ่ม
- `On Primary` = สีตัวอักษรบนปุ่ม

#### 1.2 Typography Scale ของ Material 3

| Scale | Font Size | Weight | ใช้กับ |
|-------|-----------|--------|--------|
| Display Large | 57sp | Regular | Hero text |
| Display Medium | 45sp | Regular | Section header ใหญ่ |
| Headline Large | 32sp | Regular | หัวข้อหน้าหลัก |
| Headline Medium | 28sp | Regular | หัวข้อ Card |
| Title Large | 22sp | Regular | App Bar title |
| Title Medium | 16sp | Medium | List item header |
| Body Large | 16sp | Regular | เนื้อหาหลัก |
| Body Medium | 14sp | Regular | เนื้อหาทั่วไป |
| Body Small | 12sp | Regular | Caption, timestamp, ข้อความรองขนาดเล็ก (ใช้ในการทดลองที่ 4) |
| Label Large | 14sp | Medium | ปุ่ม |
| Label Medium | 12sp | Medium | Tab, Chip |
| Label Small | 11sp | Medium | Badge, Tab label ขนาดเล็กสุด |

#### 1.3 Elevation และ Shadow ใน Material 3

Material 3 ใช้ **Color Overlay** แทน Drop Shadow เพื่อบ่งบอก elevation:
- ยิ่ง elevation สูง → ผสมสี Primary มากขึ้น (ไม่ใช่เงาดำ)
- มี 6 ระดับ: Level 0 ถึง Level 5 (0 = ไม่มี elevation, 5 = สูงสุด)

#### 1.4 Component หลักใน Material 3 ที่ต้องรู้

| Component | ใช้กับ | หมายเหตุ |
|-----------|--------|---------|
| **NavigationBar** | Bottom navigation 3–5 item | แนะนำสำหรับ Android |
| **TopAppBar** | Header ของหน้า | มี 4 แบบ: Center/Small/Medium/Large |
| **Card** | Container เนื้อหา | มี 3 style: Elevated/Filled/Outlined |
| **FilledButton** | Primary action | สีเต็ม, สำคัญที่สุด |
| **OutlinedButton** | Secondary action | มีเส้นขอบ |
| **TextButton** | Action ที่เน้นน้อยที่สุด | ไม่มีพื้นหลัง (⚠️ คำว่า "เน้นน้อยที่สุด" ในที่นี้หมายถึงลำดับความสำคัญของปุ่ม ไม่เกี่ยวกับสี Tertiary ในหัวข้อ 1.1 ซึ่งเป็นคนละแนวคิดกัน) |
| **FAB** | Action หลักของหน้า | วางมุมล่างขวา |
| **TextField** | Input | มี Filled/Outlined variant |
| **Chip** | Filter/Tag/Action | Assist/Filter/Input/Suggestion |
| **Dialog** | Confirmation/Alert | ไม่เกิน 2 action |
| **SnackBar** | Feedback สั้น | ด้านล่าง, หายเองใน 4 วินาที |

---

### ส่วนที่ 2: Figma สำหรับ Mobile Design

**Figma** คือเครื่องมือ UI Design แบบ Cloud-based ที่ทีมสามารถทำงานร่วมกันได้ real-time

#### 2.1 Concept หลักที่ต้องรู้ใน Figma

| Concept | คำอธิบาย |
|---------|---------|
| **Frame** | "หน้าจอ" หรือ container หลัก (เทียบกับ Screen ในแอป) |
| **Component** | Element ที่ reuse ได้ (เหมือน Widget ใน Flutter) |
| **Instance** | สำเนาของ Component ที่ใช้ใน Design |
| **Auto Layout** | ระบบ Layout อัตโนมัติ เหมือน Flexbox/Column/Row |
| **Constraint** | กำหนดว่า Element ยึดขอบไหนเมื่อ Frame ขนาดเปลี่ยน |
| **Variant** | Component หลายสถานะ (เช่น Button: Default/Hover/Disabled) |
| **Style** | Color Style, Text Style ที่ใช้ซ้ำได้ (เหมือน Design Token) |

#### 2.2 Mobile Frame Size มาตรฐาน

| Device | ขนาด |
|--------|------|
| Android (360dp) | 360 × 800 |
| Android Large (412dp) | 412 × 892 |
| iPhone 14 Pro | 393 × 852 |
| iPhone SE | 375 × 667 |

> **แนะนำ:** ออกแบบที่ 360 × 800 เพื่อรองรับ Android ขนาดกลาง

#### 2.3 Material Design 3 Kit ใน Figma

Google มี **Material 3 Design Kit** ให้ใช้ฟรีใน Figma Community ซึ่งมี Component ครบตาม Spec  
→ ใช้ kit นี้แทนการสร้าง component เองจะเร็วกว่าและถูกต้องกว่า

---

### ส่วนที่ 3: การแปลง Design เป็น Flutter Widget

#### 3.1 กระบวนการ Design-to-Code

```
Figma Design
    ↓ วิเคราะห์ Layout Structure
Widget Tree (บน Paper)
    ↓ เขียน Code
Flutter Widgets
    ↓ ตรวจสอบกับ Design
Adjust & Refine
```

#### 3.2 การวิเคราะห์ Layout เป็น Widget Tree

วิธีคิดง่าย ๆ:
1. มองหา **กลุ่มแนวตั้ง** → `Column`
2. มองหา **กลุ่มแนวนอน** → `Row`
3. มองหา **ซ้อนทับกัน** → `Stack`
4. มองหา **เนื้อหา scroll ได้** → `ListView` / `SingleChildScrollView`
5. มองหา **padding/margin** → `Padding` / `SizedBox`
6. มองหา **พื้นหลังหรือขอบ** → `Container` / `Card`

**ตัวอย่าง:**
```
[Design: Card ที่มีรูปซ้าย, ชื่อและรายละเอียดขวา]
    ↓
Card
  └── Padding
        └── Row
              ├── Image (ซ้าย)
              └── Column (ขวา)
                    ├── Text (ชื่อ)
                    └── Text (รายละเอียด)
```

#### 3.3 ThemeData และ Material 3 ใน Flutter

Flutter รองรับ Material 3 ผ่าน `ThemeData` โดยตั้งค่า `useMaterial3: true`:

```dart
MaterialApp(
  theme: ThemeData(
    useMaterial3: true,
    colorScheme: ColorScheme.fromSeed(
      seedColor: Colors.deepPurple,    // สี seed เพียงสีเดียว
      brightness: Brightness.light,
    ),
  ),
  home: MyHomePage(),
)
```

Flutter จะ generate Color Scheme ทั้งหมดให้อัตโนมัติจาก seedColor

---

### ส่วนที่ 4: Google AI Studio สำหรับ UI Generation

**Google AI Studio** ช่วยในการสร้าง Flutter UI Component ได้โดย:

1. **Describe UI ด้วยภาษาธรรมชาติ** → ให้ Gemini เขียน Flutter code
2. **ส่งรูป Mockup** → ให้ Gemini วิเคราะห์และเขียน code
3. **ให้ Gemini Review code** → หา bug หรือ suggest ปรับปรุง

#### Prompt Engineering สำหรับ UI Generation

```
Prompt ที่ดี:
"Create a Flutter ProfileCard widget using Material Design 3.
The card should have:
- Circular avatar (64px)
- Name (Title Medium style)
- Email (Body Small, grey color)
- Follow button (FilledButton)
Use Card widget with elevation, proper padding (16px all sides).
Follow Material 3 theming with ColorScheme."

Prompt ที่ไม่ดี:
"Make a profile card"
```

---

## 🧪 การทดลอง

### การทดลองที่ 1: สร้าง Color Scheme ด้วย Material Theme Builder (20 นาที)

#### วัตถุประสงค์
เข้าใจระบบ Dynamic Color ของ Material 3 และสร้าง Color Scheme สำหรับ Project

#### ขั้นตอน

**ขั้นตอนที่ 1.1: เปิด Material Theme Builder**
1. เปิด Browser ไปที่ https://m3.material.io/theme-builder
2. จะเห็น UI Preview ของ Material 3 App พร้อม Color Picker

**ขั้นตอนที่ 1.2: สร้าง Color Scheme ของตัวเอง**
1. คลิกที่ **"Primary"** color circle
2. เลือกสีที่เป็น brand color ของ App ที่จะทำ Project
   - ตัวอย่าง: สีเขียว `#2E7D32` สำหรับ App เกี่ยวกับสิ่งแวดล้อม
   - ตัวอย่าง: สีฟ้า `#1565C0` สำหรับ App เกี่ยวกับการเงิน
3. สังเกตว่า Secondary, Tertiary, Neutral **เปลี่ยนอัตโนมัติ** ตาม Primary ที่เลือก
4. ทดลองสลับดูระหว่าง **Light** และ **Dark** mode (สังเกตว่า contrast ยังดีอยู่)

**ขั้นตอนที่ 1.3: Export เป็น Flutter Code**
1. คลิก **"Export"** ที่มุมขวาบน
2. เลือก **"Flutter"**
3. จะได้ไฟล์ `color_schemes.g.dart` ที่มี `ColorScheme` สำหรับ Light และ Dark
4. บันทึกไฟล์ไว้ (จะนำมาใช้ในการทดลองที่ 3)

**ขั้นตอนที่ 1.4: บันทึกผล**

| รายการ | ค่าที่ได้ |
|--------|---------|
| Primary Color (Hex) | _________________ |
| Secondary Color (Hex) | _________________ |
| Primary Container (Hex) | _________________ |
| Surface (Hex) | _________________ |

> **คำถาม:** ทำไม Material 3 ถึงไม่ให้เราเลือกสีทุกสีเอง แต่ generate จาก seed color เดียว?

---

### การทดลองที่ 2: ออกแบบ UI Mockup ด้วย Figma (55 นาที)

#### วัตถุประสงค์
สร้าง Mockup ของ Mobile App อย่างน้อย 3 หน้าด้วย Material Design 3

#### ขั้นตอนเตรียมการ Figma

**ขั้นตอนที่ 2.1: ตั้งค่า Figma Project**
1. ไปที่ https://figma.com และ Login (สร้าง Account ฟรีถ้ายังไม่มี)
2. คลิก **"+ New design file"**
3. ตั้งชื่อไฟล์: `[ชื่อของคุณ]_Week03_MobileUI`
4. ลบ Frame เริ่มต้นออก (ถ้ามี)

**ขั้นตอนที่ 2.2: Import Material Design 3 Kit**
1. กด `Ctrl+P` (Windows) หรือ `Cmd+P` (Mac) เพื่อเปิด Quick Actions
2. พิมพ์ "Community" และเลือก "Open Community"
3. ค้นหา **"Material Design 3"** (โดย Google)
4. คลิก **"Duplicate"** เพื่อ copy เข้า workspace ของคุณ
5. กลับมาที่ไฟล์ของคุณ และเปิด **Assets Panel** (ด้านซ้าย, icon กล่อง)
6. คลิก **"Team Library"** icon → Enable Material 3 Kit

**ขั้นตอนที่ 2.3: สร้าง Frame สำหรับ Mobile**
1. กด `F` (Frame tool)
2. ด้านขวามือ เลือก Preset: **"Android Small"** (360 × 800)
3. สร้าง Frame 3 ชุด ตั้งชื่อ:
   - `Home Screen`
   - `Detail Screen`
   - `Profile Screen`
4. จัดเรียง Frame ให้ชิดกัน ห่างกัน 40px

#### ขั้นตอนออกแบบหน้าหลัก (Home Screen)

**ขั้นตอนที่ 2.4: ออกแบบ App Bar**
1. คลิกที่ Frame `Home Screen`
2. ไปที่ Assets → ค้นหา **"Top App Bar"**
3. ลาก Component `Center-aligned Top App Bar` ลงบน Frame
4. วางที่ด้านบนสุด (y = 0)
5. ปรับ width ให้เต็ม Frame (360px)
6. Double-click เพื่อแก้ไขชื่อ: เปลี่ยนเป็นชื่อ App ของคุณ

**ขั้นตอนที่ 2.5: ออกแบบ Content Area**

สำหรับ App หมวดไหนก็ได้ที่คุณต้องการ (เช่น Recipe App, Todo App, E-commerce):

1. **สร้าง Card สำหรับ Item:**
   - ไปที่ Assets Panel → ค้นหา **"Card"** แล้วลาก Component `Elevated Card` (หรือ `Filled Card`) จาก Material 3 Kit ลงบน Frame แทนการวาด Rectangle เอง — Corner Radius จะติดมากับ Component โดยอัตโนมัติตามสเปก M3 ไม่ต้องตั้งเอง
   - ปรับขนาดเป็น 328 × 100
   - ถ้าต้องการปรับสีพื้น ให้ไปที่ Fill → เลือก **Color Style** จาก Library ที่ Enable ไว้ในขั้นตอน 2.2 (เช่น "Surface Variant") แทนการพิมพ์ Hex Code เอง เพราะ Kit ผูก Design Token ไว้ให้แล้ว การพิมพ์ Hex ตรง ๆ จะทำให้ Dark Mode พังทันทีตามที่อธิบายในทฤษฎีข้อ 1.1
   - จัดตำแหน่ง: x=16, y=80 (ใต้ App Bar)

2. **เพิ่ม Text บน Card:**
   - กด `T` (Text tool) คลิกบน Card
   - พิมพ์ชื่อ Item แล้วไปที่ Text Style ในแผงขวา → เลือก **"Title Medium"** จาก Library (แทนการตั้งขนาด 16/Weight Medium เอง)
   - เพิ่ม Subtitle แล้วเลือก Text Style **"Body Medium"** จาก Library จากนั้นเปลี่ยนสีตัวอักษรเป็น Color Style **"On Surface Variant"** (แทนการพิมพ์ `#666666`) เพื่อให้สีเปลี่ยนตาม Light/Dark Mode อัตโนมัติเช่นเดียวกับพื้น Card

3. **สร้าง Card รูปแบบเดียวกัน 3–4 ชุด:**
   - Select Card ทั้งหมด (กด Cmd/Ctrl + G เพื่อ Group)
   - Duplicate ด้วย `Cmd/Ctrl + D`
   - เลื่อนลงมา 16px จาก Card บน
   - ทำซ้ำ 2–3 ครั้ง

4. **เพิ่ม Bottom Navigation Bar:**
   - ไปที่ Assets → ค้นหา **"Navigation Bar"**
   - ลาก Component ลงที่ด้านล่างสุด (y = 752 สำหรับ Frame 800px)
   - ปรับ width: 360px
   - แก้ไข Label: เลือก 3 Tab ที่เหมาะกับ App (เช่น Home/Search/Profile)

5. **เพิ่ม FAB (Floating Action Button):**
   - ไปที่ Assets → ค้นหา **"FAB"**
   - เลือก Extended FAB หรือ Regular FAB
   - วางที่ด้านล่างขวา: x=280, y=680

**ขั้นตอนที่ 2.6: ออกแบบ Detail Screen (ทำเองอย่างน้อย 1 จอ)**

คิด flow ว่า: เมื่อกด Card บน Home จะไป Detail Screen อะไร  
ออกแบบ Detail Screen ให้มีอย่างน้อย:
- Top App Bar พร้อม Back button (ไอคอน arrow_back)
- รูปภาพ/Banner ขนาดใหญ่
- ชื่อและรายละเอียด
- ปุ่ม Action หลัก 1 ปุ่ม (FilledButton)

**ขั้นตอนที่ 2.6b: ออกแบบ Profile Screen (Bonus ไม่บังคับ)**

Frame `Profile Screen` ที่สร้างไว้ในขั้นตอนที่ 2.3 ไม่ใช่ส่วนบังคับของ Checklist การประเมิน (ซึ่งต้องการแค่ Home + 1 หน้าอื่นเป็นอย่างน้อย) แต่ถ้ามีเวลาเหลือ แนะนำให้ลองออกแบบเพื่อฝึกฝีมือเพิ่ม โดยควรมีอย่างน้อย:
- Avatar วงกลมและชื่อผู้ใช้ (Title Large)
- Bottom Navigation Bar เดียวกับ Home Screen (ให้ Tab "โปรไฟล์" เป็น Active)
- ปุ่ม "แก้ไขโปรไฟล์" (OutlinedButton)

หากไม่มีเวลาออกแบบ Profile Screen ให้ลบ Frame นี้ทิ้งหรือปล่อยว่างไว้ได้ ไม่มีผลต่อคะแนน

**ขั้นตอนที่ 2.7: เพิ่ม Prototype Connection (Optional, สำหรับ Demo)**
1. สลับไปที่ **Prototype tab** (แผง Properties ขวา)
2. Hover ที่ Card บน Home Screen → จะเห็น `+` ปรากฏ
3. ลาก Connection ไปยัง Detail Screen
4. ตั้งค่า Interaction: "On tap" → Navigate to → Detail Screen
5. Transition: Push (Right) → ทดลอง Preview ด้วย `Cmd/Ctrl + Shift + Enter`

**ขั้นตอนที่ 2.8: บันทึกผล**

Screenshot Design ของคุณทั้ง 3 หน้า และตอบคำถาม:

| คำถาม | คำตอบ |
|-------|-------|
| App ที่ออกแบบคือ? | _________________ |
| Primary Color ที่ใช้? | _________________ |
| Navigation Pattern ที่เลือก? | _________________ |
| ทำไมเลือก Pattern นี้? | _________________ |

---

### การทดลองที่ 3: แปลง Design เป็น Flutter Code (55 นาที)

#### วัตถุประสงค์
เขียน Flutter Widget จาก Design ที่ออกแบบใน Figma

#### ขั้นตอนเตรียมการ

**ขั้นตอนที่ 3.1: เตรียม Flutter Project**
1. เปิด Terminal/Command Prompt
2. สร้าง Flutter Project ใหม่:
   ```bash
   flutter create week03_ui_lab
   cd week03_ui_lab
   ```
3. เปิดด้วย VS Code:
   ```bash
   code .
   ```
4. คัดลอกไฟล์ `color_schemes.g.dart` ที่ Export มาจาก**การทดลองที่ 1** (ขั้นตอนที่ 1.3) ไปวางไว้ที่ `lib/color_schemes.g.dart` — นี่คือจุดที่งานจากการทดลองที่ 1 ถูกนำมาใช้จริงในการทดลองนี้

**ขั้นตอนที่ 3.2: ตั้งค่า Material 3 Theme**

เปิดไฟล์ `lib/main.dart` และแก้ไขเป็น:

```dart
import 'package:flutter/material.dart';
import 'color_schemes.g.dart'; // ไฟล์ที่ Export จาก Material Theme Builder ในการทดลองที่ 1

void main() {
  runApp(const MyApp());
}

class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Week 03 UI Lab',
      debugShowCheckedModeBanner: false,
      theme: ThemeData(
        useMaterial3: true,           // เปิดใช้ Material 3
        colorScheme: lightColorScheme, // ← ColorScheme ที่ Export มาจากการทดลองที่ 1 (Light)
      ),
      darkTheme: ThemeData(
        useMaterial3: true,
        colorScheme: darkColorScheme,  // ← ColorScheme ที่ Export มาจากการทดลองที่ 1 (Dark)
      ),
      themeMode: ThemeMode.system,     // สลับตามระบบ
      home: const HomeScreen(),
    );
  }
}
```

> **หมายเหตุ:** ถ้าไฟล์ `color_schemes.g.dart` หายหรือ Export ไม่สำเร็จ ให้ใช้ทางเลือกสำรองนี้แทน (ผลลัพธ์ใกล้เคียงกันมาก เพราะคำนวณจาก Seed Color เดียวกัน):
> ```dart
> colorScheme: ColorScheme.fromSeed(
>   seedColor: const Color(0xFF2E7D32), // ← เปลี่ยนเป็นสีที่คุณเลือกใน Figma
>   brightness: Brightness.light,
> ),
> ```

**ขั้นตอนที่ 3.3: วิเคราะห์ Design เป็น Widget Tree**

ก่อนเขียน code ให้วาด Widget Tree บนกระดาษหรือ Whiteboard:

```
สำหรับ Home Screen:

Scaffold
├── AppBar
│   └── Text("ชื่อ App")
├── body: ListView
│   ├── ItemCard (item 1)
│   ├── ItemCard (item 2)
│   └── ItemCard (item 3)
├── floatingActionButton: FloatingActionButton
└── bottomNavigationBar: NavigationBar
      ├── NavigationDestination (Home)
      ├── NavigationDestination (Search)
      └── NavigationDestination (Profile)
```

**ขั้นตอนที่ 3.4: สร้างไฟล์โครงสร้าง**

สร้างไฟล์ใหม่ใน `lib/`:
```
lib/
├── main.dart
├── screens/
│   ├── home_screen.dart
│   └── detail_screen.dart
└── widgets/
    └── item_card.dart
```

สร้างโฟลเดอร์และไฟล์:
```bash
mkdir -p lib/screens lib/widgets
touch lib/screens/home_screen.dart
touch lib/screens/detail_screen.dart
touch lib/widgets/item_card.dart
```

#### ขั้นตอนเขียน Widget หลัก

**ขั้นตอนที่ 3.5: สร้าง ItemCard Widget**

เปิด `lib/widgets/item_card.dart`:

```dart
import 'package:flutter/material.dart';

/// ItemCard แสดงข้อมูล Item แบบ Card
/// เป็น Reusable Widget ที่รับ data ผ่าน Constructor
class ItemCard extends StatelessWidget {
  final String title;
  final String subtitle;
  final IconData icon;
  final VoidCallback? onTap;

  const ItemCard({
    super.key,
    required this.title,
    required this.subtitle,
    required this.icon,
    this.onTap,
  });

  @override
  Widget build(BuildContext context) {
    // ดึง ColorScheme จาก Theme ที่ตั้งค่าไว้ใน main.dart
    final colorScheme = Theme.of(context).colorScheme;
    final textTheme = Theme.of(context).textTheme;

    return Card(
      // Material 3 Card: elevation = 1 (Elevated style)
      elevation: 1,
      margin: const EdgeInsets.symmetric(horizontal: 16, vertical: 6),
      // สำคัญ: ต้องมี clipBehavior เพื่อให้ Ripple effect ของ InkWell
      // ถูกตัดให้โค้งตามขอบ Card ไม่ล้นออกไปเป็นมุมเหลี่ยม
      clipBehavior: Clip.antiAlias,
      child: InkWell(
        onTap: onTap,
        borderRadius: BorderRadius.circular(12),
        child: Padding(
          padding: const EdgeInsets.all(16),
          child: Row(
            children: [
              // Icon Container
              Container(
                width: 48,
                height: 48,
                decoration: BoxDecoration(
                  color: colorScheme.primaryContainer,
                  borderRadius: BorderRadius.circular(12),
                ),
                child: Icon(
                  icon,
                  color: colorScheme.onPrimaryContainer,
                  size: 24,
                ),
              ),
              const SizedBox(width: 16),
              // Text Content
              Expanded(
                child: Column(
                  crossAxisAlignment: CrossAxisAlignment.start,
                  children: [
                    Text(
                      title,
                      // ใช้ titleMedium จาก TextTheme (Material 3)
                      style: textTheme.titleMedium,
                      maxLines: 1,
                      overflow: TextOverflow.ellipsis,
                    ),
                    const SizedBox(height: 4),
                    Text(
                      subtitle,
                      // ใช้ bodyMedium ให้ตรงกับสเปกที่ออกแบบไว้ใน Figma
                      // (ขั้นตอนที่ 2.5 ใช้ Text Style "Body Medium" สำหรับ Subtitle)
                      style: textTheme.bodyMedium?.copyWith(
                        color: colorScheme.onSurfaceVariant,
                      ),
                      maxLines: 2,
                      overflow: TextOverflow.ellipsis,
                    ),
                  ],
                ),
              ),
              // Chevron Icon
              Icon(
                Icons.chevron_right,
                color: colorScheme.onSurfaceVariant,
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

**ขั้นตอนที่ 3.6: สร้าง Home Screen**

เปิด `lib/screens/home_screen.dart`:

```dart
import 'package:flutter/material.dart';
import '../widgets/item_card.dart';
import 'detail_screen.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  // State: tab ที่เลือกอยู่ใน Bottom Navigation
  int _selectedIndex = 0;

  // ข้อมูลตัวอย่าง (ในโปรเจกต์จริงจะดึงจาก API/Database)
  final List<Map<String, dynamic>> _items = [
    {
      'title': 'รายการที่ 1',
      'subtitle': 'คำอธิบายสั้น ๆ ของรายการนี้',
      'icon': Icons.star_outline,
    },
    {
      'title': 'รายการที่ 2',
      'subtitle': 'ข้อมูลเพิ่มเติมของรายการที่สอง',
      'icon': Icons.favorite_outline,
    },
    {
      'title': 'รายการที่ 3',
      'subtitle': 'รายละเอียดของรายการที่สาม',
      'icon': Icons.bookmark_outline,
    },
    {
      'title': 'รายการที่ 4',
      'subtitle': 'ข้อมูลของรายการที่สี่',
      'icon': Icons.schedule_outlined,
    },
  ];

  void _onItemTapped(int index) {
    setState(() {
      _selectedIndex = index;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // Material 3 AppBar: Center-aligned
      appBar: AppBar(
        centerTitle: true,
        title: const Text('My App'),
        actions: [
          IconButton(
            icon: const Icon(Icons.search),
            onPressed: () {
              // TODO: เพิ่ม Search functionality
            },
            tooltip: 'ค้นหา',
          ),
        ],
      ),

      // Body: ListView แสดง ItemCard
      body: ListView.builder(
        padding: const EdgeInsets.symmetric(vertical: 8),
        itemCount: _items.length,
        itemBuilder: (context, index) {
          final item = _items[index];
          return ItemCard(
            title: item['title'],
            subtitle: item['subtitle'],
            icon: item['icon'],
            onTap: () {
              // Navigate ไป Detail Screen พร้อมส่งข้อมูล
              Navigator.push(
                context,
                MaterialPageRoute(
                  builder: (context) => DetailScreen(
                    title: item['title'],
                    subtitle: item['subtitle'],
                  ),
                ),
              );
            },
          );
        },
      ),

      // FAB: Primary action ของหน้า
      floatingActionButton: FloatingActionButton.extended(
        onPressed: () {
          // TODO: เพิ่มรายการใหม่
          ScaffoldMessenger.of(context).showSnackBar(
            const SnackBar(
              content: Text('เพิ่มรายการใหม่'),
              behavior: SnackBarBehavior.floating,
            ),
          );
        },
        icon: const Icon(Icons.add),
        label: const Text('เพิ่มใหม่'),
      ),

      // Bottom Navigation Bar (Material 3)
      bottomNavigationBar: NavigationBar(
        selectedIndex: _selectedIndex,
        onDestinationSelected: _onItemTapped,
        destinations: const [
          NavigationDestination(
            icon: Icon(Icons.home_outlined),
            selectedIcon: Icon(Icons.home),
            label: 'หน้าหลัก',
          ),
          NavigationDestination(
            icon: Icon(Icons.search_outlined),
            selectedIcon: Icon(Icons.search),
            label: 'ค้นหา',
          ),
          NavigationDestination(
            icon: Icon(Icons.person_outline),
            selectedIcon: Icon(Icons.person),
            label: 'โปรไฟล์',
          ),
        ],
      ),
    );
  }
}
```

**ขั้นตอนที่ 3.7: สร้าง Detail Screen**

เปิด `lib/screens/detail_screen.dart`:

```dart
import 'package:flutter/material.dart';

class DetailScreen extends StatelessWidget {
  final String title;
  final String subtitle;

  const DetailScreen({
    super.key,
    required this.title,
    required this.subtitle,
  });

  @override
  Widget build(BuildContext context) {
    final colorScheme = Theme.of(context).colorScheme;
    final textTheme = Theme.of(context).textTheme;

    return Scaffold(
      appBar: AppBar(
        // Back button เพิ่มให้อัตโนมัติเมื่อ Navigator มี stack
        title: Text(title),
      ),
      body: SingleChildScrollView(
        child: Column(
          crossAxisAlignment: CrossAxisAlignment.start,
          children: [
            // Banner Image Placeholder
            Container(
              width: double.infinity,
              height: 200,
              color: colorScheme.primaryContainer,
              child: Icon(
                Icons.image_outlined,
                size: 64,
                color: colorScheme.onPrimaryContainer,
              ),
            ),

            Padding(
              padding: const EdgeInsets.all(16),
              child: Column(
                crossAxisAlignment: CrossAxisAlignment.start,
                children: [
                  // Title
                  Text(
                    title,
                    style: textTheme.headlineMedium,
                  ),
                  const SizedBox(height: 8),

                  // Subtitle
                  Text(
                    subtitle,
                    style: textTheme.bodyMedium?.copyWith(
                      color: colorScheme.onSurfaceVariant,
                    ),
                  ),
                  const SizedBox(height: 24),

                  // Detail Content
                  Text(
                    'รายละเอียด',
                    style: textTheme.titleLarge,
                  ),
                  const SizedBox(height: 8),
                  Text(
                    'นี่คือพื้นที่สำหรับเนื้อหาของรายการ '
                    'ในโปรเจกต์จริงจะแสดงข้อมูลที่ดึงมาจาก API หรือฐานข้อมูล '
                    'ตามที่ออกแบบไว้ใน Figma',
                    style: textTheme.bodyLarge,
                  ),
                  const SizedBox(height: 32),

                  // Action Button
                  SizedBox(
                    width: double.infinity,
                    child: FilledButton.icon(
                      onPressed: () {
                        // TODO: Primary Action
                        ScaffoldMessenger.of(context).showSnackBar(
                          const SnackBar(
                            content: Text('ดำเนินการสำเร็จ'),
                            behavior: SnackBarBehavior.floating,
                          ),
                        );
                      },
                      icon: const Icon(Icons.check),
                      label: const Text('ดำเนินการ'),
                    ),
                  ),
                  const SizedBox(height: 8),

                  // Secondary Action
                  SizedBox(
                    width: double.infinity,
                    child: OutlinedButton.icon(
                      onPressed: () {
                        Navigator.pop(context); // กลับหน้าก่อน
                      },
                      icon: const Icon(Icons.arrow_back),
                      label: const Text('กลับ'),
                    ),
                  ),
                ],
              ),
            ),
          ],
        ),
      ),
    );
  }
}
```

**ขั้นตอนที่ 3.8: อัปเดต main.dart**

เพิ่ม import และเปลี่ยน home:

```dart
import 'package:flutter/material.dart';
import 'screens/home_screen.dart';  // ← เพิ่ม import

void main() {
  runApp(const MyApp());
}

// ... (ส่วน MyApp คงเดิม แต่เปลี่ยน home:)
// home: const HomeScreen(),  ← แก้ไขบรรทัดนี้
```

**ขั้นตอนที่ 3.9: รัน App และตรวจสอบ**

```bash
flutter run
```

ตรวจสอบ:
- [ ] App Bar แสดงชื่อถูกต้อง
- [ ] มี Card แสดง 4 รายการ
- [ ] กด Card แล้วไป Detail Screen ได้
- [ ] กด Back button กลับ Home ได้
- [ ] Bottom Navigation สลับ Tab ได้ (ไฮไลท์ถูกต้อง)
- [ ] FAB ปรากฏและแสดง SnackBar เมื่อกด
- [ ] สีตรงกับ Material 3 Color Scheme

---

### การทดลองที่ 4: ใช้ AI ช่วย Generate UI Component (30 นาที)

#### วัตถุประสงค์
ฝึกใช้ Google AI Studio สร้าง Flutter Widget และ evaluate ผล

#### ขั้นตอน

**ขั้นตอนที่ 4.1: เปิด Google AI Studio**
1. ไปที่ https://aistudio.google.com
2. Login ด้วย Google Account
3. คลิก **"+ New prompt"** → เลือก **"Chat prompt"**

**ขั้นตอนที่ 4.2: Generate ProfileCard Widget**

Copy Prompt ต่อไปนี้ใส่ใน AI Studio:

```
You are an expert Flutter developer using Material Design 3.

Create a Flutter StatelessWidget called "UserProfileCard" that:
1. Shows a circular user avatar (radius 32) using CircleAvatar with initials as fallback
2. Displays username using titleLarge TextStyle
3. Shows email using bodyMedium TextStyle in onSurfaceVariant color
4. Shows a "Follow" FilledButton and "Message" OutlinedButton side by side
5. Shows a row of 3 stats: Posts, Followers, Following (using Column: number + label)
6. Uses Card widget with proper Material 3 elevation
7. Reads colors from Theme.of(context).colorScheme (NO hardcoded colors)
8. Has proper padding (16px) and spacing (8px between elements)
9. Accepts these constructor parameters: name, email, avatarUrl (nullable), 
   postsCount, followersCount, followingCount

Add brief comments explaining each section.
```

**ขั้นตอนที่ 4.3: วิเคราะห์ Code ที่ได้**

อ่าน code ที่ AI สร้างและตอบคำถาม:

| คำถาม | คำตอบ |
|-------|-------|
| AI ใช้ Widget อะไรสร้าง Avatar? | _________________ |
| AI handle กรณี avatarUrl เป็น null อย่างไร? | _________________ |
| AI ใช้ color จาก Theme หรือ hardcode? | _________________ |
| มีส่วนไหนที่ควรปรับปรุง? | _________________ |

**ขั้นตอนที่ 4.4: นำ Code ไปใช้ใน Project**

1. สร้างไฟล์ `lib/widgets/user_profile_card.dart`
2. วาง code จาก AI Studio
3. แก้ไขส่วนที่ผิดหรือไม่เหมาะสม (ถ้ามี)
4. Import และใช้ใน Profile Tab ของ Home Screen

**ขั้นตอนที่ 4.5: ทดลอง Multimodal — ส่งรูป Figma ให้ AI วิเคราะห์**

1. Screenshot Design จาก Figma ที่ทำในการทดลองที่ 2
2. ใน AI Studio คลิก **"+"** → **"Upload image"**
3. Upload รูป Screenshot
4. พิมพ์ Prompt:
   ```
   This is a mobile app UI design in Figma using Material Design 3.
   Analyze the layout and write the Flutter widget tree structure (as code comments).
   Then implement it as a Flutter StatelessWidget.
   Use Material 3 components and read colors from Theme.of(context).colorScheme.
   ```
5. ดู code ที่ได้ และเปรียบเทียบกับ code ที่เขียนเองในการทดลองที่ 3

---

### การทดลองที่ 5: Dark Mode และ Accessibility Check (20 นาที)

#### วัตถุประสงค์
ทดสอบว่า UI ทำงานได้ดีทั้ง Light/Dark Mode และผ่าน Accessibility เบื้องต้น

**ขั้นตอนที่ 5.1: ทดสอบ Dark Mode**

1. ใน `main.dart` เปลี่ยน `themeMode` เป็น `ThemeMode.dark` ชั่วคราว
2. รัน App → ตรวจสอบว่าทุก Text อ่านออกไหม
3. มีสีไหนที่ contrast ต่ำเกินไปไหม (ตัวอักษรจางบนพื้นหลังจาง)
4. เปลี่ยนกลับเป็น `ThemeMode.system`

> **ถ้าพบปัญหา:** ตรวจสอบว่าใช้ `colorScheme.onSurface` / `colorScheme.onSurfaceVariant` สำหรับ text แทนที่จะ hardcode สี

**ขั้นตอนที่ 5.2: ตรวจสอบ Touch Target Size**

ใน Flutter DevTools:
1. รัน App ใน Debug mode: `flutter run --debug`
2. เปิด **Flutter Inspector** ใน DevTools
3. Enable **"Show guidelines"** → จะเห็น layout boundary
4. ตรวจสอบว่า Interactive element ทุกชิ้นมีขนาดอย่างน้อย **48×48 dp**

**ขั้นตอนที่ 5.3: ตรวจสอบ Semantic Labels**

เพิ่ม `Semantics` widget สำหรับ element ที่ไม่มี label ชัดเจน:

```dart
// ก่อน: Icon ที่ไม่มี label
IconButton(
  icon: const Icon(Icons.search),
  onPressed: () {},
)

// หลัง: เพิ่ม tooltip เป็น Semantic label
IconButton(
  icon: const Icon(Icons.search),
  onPressed: () {},
  tooltip: 'ค้นหา',  // Screen Reader จะอ่านค่านี้
)
```

ตรวจสอบทุก `IconButton` ว่ามี `tooltip` ครบ

---

## 📝 สรุปและส่งงาน

### สิ่งที่ต้องส่ง

| รายการ | รูปแบบ | คะแนน |
|--------|--------|-------|
| Figma Design (link หรือ export PDF) | .pdf หรือ Figma link | 5 คะแนน |
| Flutter Project | .zip หรือ GitHub link | 10 คะแนน |
| สรุปการเรียนรู้ (ตอบคำถามด้านล่าง) | ในใบงานนี้ | 5 คะแนน |

### คำถามสรุปการเรียนรู้ (ตอบทุกข้อ)

**ข้อ 1:** Material 3 ต่างจาก Material 2 อย่างไรในด้าน Color System? (3–5 ประโยค)

```
คำตอบ: _______________________________________________
```

**ข้อ 2:** เมื่อแปลง Figma Design เป็น Flutter Widget พบปัญหาอะไรบ้าง และแก้ไขอย่างไร?

```
คำตอบ: _______________________________________________
```

**ข้อ 3:** Code ที่ AI สร้างให้นั้นดีแค่ไหน? ต้องปรับปรุงอะไรบ้าง?

```
คำตอบ: _______________________________________________
```

**ข้อ 4:** ถ้าจะนำ UI ที่ออกแบบไปใช้กับ Project จริง จะปรับปรุงอะไรบ้าง?

```
คำตอบ: _______________________________________________
```

---

## 🎯 Checklist การประเมิน

### Figma Design (5 คะแนน)
- [ ] มี Frame ขนาด 360 × 800 หรือ Mobile standard
- [ ] ออกแบบอย่างน้อย 2 หน้า (Home + 1 หน้าอื่น)
- [ ] ใช้ Material Design 3 Component (AppBar, Card, Button, Navigation)
- [ ] สีสม่ำเสมอ ใช้ Color Scheme จาก Material Theme Builder
- [ ] Typography ถูกต้องตาม Scale (ไม่ใช้ขนาดสุ่ม)

### Flutter Code (10 คะแนน)
- [ ] ตั้งค่า Material 3 ด้วย `useMaterial3: true` และ `ColorScheme.fromSeed`
- [ ] มี `ItemCard` widget แยกไฟล์ และ reusable
- [ ] มี Bottom Navigation Bar ทำงานได้ถูกต้อง
- [ ] Navigate ไป Detail Screen และ Back ได้
- [ ] ไม่มีการ hardcode สี (ใช้ `colorScheme` จาก Theme ทั้งหมด)
- [ ] Code อ่านได้ มี comment อธิบาย
- [ ] รองรับ Dark Mode โดยไม่มีปัญหา Contrast (ตรวจตามขั้นตอนในการทดลองที่ 5.1)
- [ ] `IconButton` ทุกตัวมี `tooltip` หรือ Semantic label ครบ (ตรวจตามขั้นตอนในการทดลองที่ 5.3)

### สรุปการเรียนรู้ (5 คะแนน)
- [ ] ตอบครบทุกข้อ
- [ ] แสดงให้เห็นว่าเข้าใจ ไม่ใช่แค่ copy-paste

---

## 📖 แหล่งอ้างอิง

- [Material Design 3 Official](https://m3.material.io/)
- [Material Theme Builder](https://m3.material.io/theme-builder)
- [Flutter Material 3 Migration Guide](https://docs.flutter.dev/release/breaking-changes/material-3-migration)
- [Flutter Widget Catalog](https://docs.flutter.dev/ui/widgets)
- [Figma — Getting Started](https://help.figma.com/hc/en-us/categories/360002051613)
- [Google AI Studio](https://aistudio.google.com)
