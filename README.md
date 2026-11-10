# 📅 DailyTracker

> **Desktop Habit & Daily Task Tracker** — Ứng dụng theo dõi thói quen hàng ngày với SQLite và hệ thống Streak tích hợp.

![Java](https://img.shields.io/badge/Java-21-orange?logo=openjdk)
![JavaFX](https://img.shields.io/badge/JavaFX-21.0.5-blue?logo=java)
![SQLite](https://img.shields.io/badge/SQLite-3.47.0-green?logo=sqlite)
![Maven](https://img.shields.io/badge/Build-Maven-red?logo=apachemaven)
![Platform](https://img.shields.io/badge/Platform-Windows-blue?logo=windows)

---

## ✨ Tính năng

- 📋 **Today View** — Danh sách habit cần hoàn thành hôm nay, lọc theo danh mục, thanh tiến độ
- ✅ **Đánh dấu hoàn thành** — Click để toggle completed/uncompleted theo từng ngày
- 🔥 **Streak tự động** — Tính chuỗi ngày liên tiếp cho từng habit
- 🗂️ **Quản lý Habit & Category** — Thêm, sửa, xóa habit và danh mục có màu sắc
- 📊 **Analytics View** — Thống kê KPI: tổng habit, streak tốt nhất, tỷ lệ hoàn thành hôm nay
- 🎨 **Dark theme hiện đại** — Giao diện dark mode với màu Slate/Sky Blue

---

## ⚙️ Yêu cầu hệ thống

| Yêu cầu | Phiên bản |
|---|---|
| **Hệ điều hành** | Windows 10/11 (64-bit) |
| **Java** | Không cần cài — đã bundle JRE bên trong |
| **Dung lượng** | ~200 MB (bao gồm JRE + JavaFX) |

> ⚠️ **Lưu ý quan trọng**: Đường dẫn thư mục cài đặt **không được chứa ký tự đặc biệt hoặc tiếng Việt có dấu** (ví dụ: tránh dùng `Tài liệu`, `Dữ liệu`...). Khuyến nghị đặt tại `D:\DailyTracker\` hoặc `C:\DailyTracker\`.

---

## 🚀 Cách thực thi

### Cách 1: Chạy trực tiếp (Khuyến nghị)

1. Giải nén hoặc copy thư mục `DailyTracker\` ra đường dẫn **không có ký tự Unicode**
   ```
   D:\DailyTracker\
   ```
2. Vào thư mục `DailyTracker\DailyTracker\`
3. Double-click vào file **`DailyTracker.exe`**

### Cách 2: Chạy bằng lệnh (Command Prompt / PowerShell)

```powershell
cd D:\DailyTracker\DailyTracker\DailyTracker
.\DailyTracker.exe
```

### Cách 3: Chạy thẳng file JAR (cần JDK 21)

```powershell
# Yêu cầu JDK 21 được cài và trong PATH
java --enable-native-access=ALL-UNNAMED -jar app\daily-tracker-1.0.0.jar
```

### Cách 4: Build từ source (cần Maven + JDK 21)

```powershell
# 1. Clone repo
git clone <repo-url>
cd DailyTracker

# 2. Build Fat JAR
mvn clean package

# 3. Chạy với Maven
mvn javafx:run

# 4. Hoặc chạy JAR trực tiếp
java --enable-native-access=ALL-UNNAMED -jar target\daily-tracker-1.0.0.jar
```

---

## 📂 Sơ đồ cây thư mục

```
DailyTracker/                        ← Thư mục gốc (Git repo)
├── .git/                            ← Dữ liệu Git
├── .gitattributes                   ← Cấu hình Git line endings
├── README.md                        ← File tài liệu này
│
└── DailyTracker/                    ← Thư mục ứng dụng (jpackage output)
    ├── DailyTracker.exe             ← Launcher native (entry point chính)
    │
    ├── app/                         ← Thư mục chứa ứng dụng Java
    │   ├── daily-tracker-1.0.0.jar  ← Fat JAR (toàn bộ source + dependencies)
    │   ├── DailyTracker.cfg         ← Cấu hình launcher (classpath, main class)
    │   └── .jpackage.xml            ← Metadata jpackage (version, platform)
    │
    └── runtime/                     ← JRE bundled (stripped-down Java Runtime)
        ├── bin/                     ← Native DLLs (java.dll, jvm.dll, JavaFX...)
        │   ├── server/
        │   │   └── jvm.dll          ← JVM chính (HotSpot Server VM, ~13 MB)
        │   ├── java.dll
        │   ├── javafx*.dll          ← JavaFX native libraries
        │   └── *.dll                ← Windows system DLLs
        ├── conf/                    ← Cấu hình JVM (security, logging...)
        ├── legal/                   ← Giấy phép thư viện
        ├── lib/                     ← JVM modules, timezone data
        │   ├── modules              ← Java module image
        │   ├── jrt-fs.jar           ← Java runtime filesystem
        │   └── security/            ← CA certs, security policies
        └── release                  ← Thông tin phiên bản JRE
```

### Cấu trúc source code bên trong JAR

```
daily-tracker-1.0.0.jar
│
├── com/dailytracker/                ← Package gốc
│   ├── App.class                    ← JavaFX Application
│   ├── Launcher.class               ← Main entry point
│   │
│   ├── model/                       ← Tầng Model (POJO)
│   │   ├── Category.class
│   │   ├── Habit.class
│   │   ├── DailyLog.class
│   │   └── StreakStats.class
│   │
│   ├── dao/                         ← Tầng DAO (Data Access)
│   │   ├── DatabaseManager.class
│   │   ├── CategoryDao.class
│   │   ├── HabitDao.class
│   │   └── DailyLogDao.class
│   │
│   ├── service/                     ← Tầng Service (Business Logic)
│   │   ├── CategoryService.class
│   │   └── HabitService.class
│   │
│   └── ui/                          ← Tầng UI (JavaFX Views)
│       ├── MainView.class
│       ├── TodayView.class
│       ├── HabitManagementView.class
│       ├── AnalyticsView.class
│       └── components/
│           └── HabitCard.class
│
├── css/
│   └── style.css                    ← Dark theme stylesheet (JavaFX CSS)
│
└── META-INF/
    ├── MANIFEST.MF                  ← Main-Class: com.dailytracker.Launcher
    └── maven/com.dailytracker/
        └── daily-tracker/
            └── pom.xml              ← Maven build descriptor
```

---

## 📁 Chức năng các File

### File cấu hình

| File | Chức năng |
|---|---|
| `DailyTracker.exe` | Native launcher do `jpackage` tạo ra. Tự động tìm JVM trong `runtime/bin/server/jvm.dll` và chạy JAR |
| `app/DailyTracker.cfg` | Khai báo classpath (`daily-tracker-1.0.0.jar`), main class (`com.dailytracker.Launcher`), và JVM options |
| `app/.jpackage.xml` | Metadata nội bộ của jpackage: phiên bản app (`1.0`), tên launcher, platform (`windows`) |
| `app/daily-tracker-1.0.0.jar` | Fat JAR chứa toàn bộ bytecode + tất cả dependencies (JavaFX, SQLite JDBC, SLF4J) |
| `runtime/lib/modules` | Java Module Image — chứa tất cả Java standard library modules đã được tối ưu cho app |
| `css/style.css` | Stylesheet JavaFX (dark theme: màu nền `#0f172a`, accent `#38bdf8`) |

---

## 🗄️ Tổng hợp các Class trong CSDL

Dự án tuân theo kiến trúc **3-Tier**: `UI → Service → DAO → SQLite Database`

---

### 🔵 Tầng Entry Point

#### `Launcher`
```
Package : com.dailytracker
Vai trò : Main entry point của Fat JAR
```
Lớp wrapper đơn giản, chỉ gọi `App.main()`. Cần thiết vì `jpackage` và `maven-shade-plugin` yêu cầu main class không được extends `javafx.application.Application` trực tiếp để tránh lỗi module system.

#### `App`
```
Package : com.dailytracker
Vai trò : JavaFX Application — khởi tạo toàn bộ giao diện
```
- Extends `javafx.application.Application`
- Load stylesheet `css/style.css`
- Tạo `Scene` và gọi `MainView`
- Cấu hình Stage (title, kích thước cửa sổ)

---

### 🟢 Tầng Model (POJO — Plain Old Java Objects)

Các class thuần dữ liệu, ánh xạ 1-1 với bảng trong SQLite.

#### `Category`
```
Package : com.dailytracker.model
Bảng DB : categories
```
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `int` | Primary key, auto-increment |
| `name` | `String` | Tên danh mục (vd: "Sức khỏe", "Học tập") |
| `color` | `String` | Mã màu hex (vd: `#38bdf8`) để hiển thị tag |

#### `Habit`
```
Package : com.dailytracker.model
Bảng DB : habits
```
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `int` | Primary key, auto-increment |
| `name` | `String` | Tên habit (vd: "Uống 2L nước") |
| `description` | `String` | Mô tả chi tiết |
| `categoryId` | `int` | Foreign key → `categories.id` |
| `createdAt` | `String` | Ngày tạo (ISO format: `yyyy-MM-dd`) |

#### `DailyLog`
```
Package : com.dailytracker.model
Bảng DB : daily_logs
```
| Field | Kiểu | Mô tả |
|---|---|---|
| `id` | `int` | Primary key, auto-increment |
| `habitId` | `int` | Foreign key → `habits.id` |
| `date` | `String` | Ngày ghi log (`yyyy-MM-dd`) |
| `completed` | `boolean` | `true` = đã hoàn thành, `false` = chưa |

> Mỗi ngày, mỗi habit tạo ra 1 bản ghi `DailyLog`. Toggle completed = UPDATE bản ghi này.

#### `StreakStats`
```
Package : com.dailytracker.model
Bảng DB : (tính toán từ daily_logs, không có bảng riêng)
```
| Field | Kiểu | Mô tả |
|---|---|---|
| `habitId` | `int` | ID habit tham chiếu |
| `currentStreak` | `int` | Số ngày liên tiếp hiện tại (tính ngược từ hôm nay) |
| `longestStreak` | `int` | Streak dài nhất từ trước tới nay |
| `totalCompleted` | `int` | Tổng số ngày đã hoàn thành (all time) |

---

### 🟡 Tầng DAO (Data Access Object)

Chịu trách nhiệm **toàn bộ giao tiếp với SQLite**. Mỗi DAO tương ứng một bảng.

#### `DatabaseManager`
```
Package : com.dailytracker.dao
Vai trò : Quản lý kết nối SQLite và khởi tạo schema
```
**Chức năng chính:**
- Mở kết nối JDBC đến file `daily_tracker.db` (tạo mới nếu chưa có)
- Tạo 3 bảng khi khởi động lần đầu:
  ```sql
  CREATE TABLE IF NOT EXISTS categories (id, name, color)
  CREATE TABLE IF NOT EXISTS habits (id, name, description, category_id, created_at)
  CREATE TABLE IF NOT EXISTS daily_logs (id, habit_id, date, completed)
  ```
- Cung cấp `Connection` cho `CategoryDao`, `HabitDao`, `DailyLogDao`
- Đóng kết nối khi app tắt

#### `CategoryDao`
```
Package : com.dailytracker.dao
Bảng   : categories
```
| Phương thức | Mô tả |
|---|---|
| `getAllCategories()` | `SELECT * FROM categories` → `List<Category>` |
| `addCategory(Category)` | `INSERT INTO categories` |
| `updateCategory(Category)` | `UPDATE categories SET name=?, color=? WHERE id=?` |
| `deleteCategory(int id)` | `DELETE FROM categories WHERE id=?` |

#### `HabitDao`
```
Package : com.dailytracker.dao
Bảng   : habits
```
| Phương thức | Mô tả |
|---|---|
| `getAllHabits()` | `SELECT * FROM habits` → `List<Habit>` |
| `getHabitsByCategory(int categoryId)` | Lọc theo danh mục |
| `addHabit(Habit)` | `INSERT INTO habits` |
| `updateHabit(Habit)` | `UPDATE habits` |
| `deleteHabit(int id)` | `DELETE FROM habits WHERE id=?` (cascade xóa daily_logs) |

#### `DailyLogDao`
```
Package : com.dailytracker.dao
Bảng   : daily_logs
```
| Phương thức | Mô tả |
|---|---|
| `getLogsForDate(LocalDate)` | Lấy tất cả log trong ngày → `List<DailyLog>` |
| `getLogForHabitAndDate(int, LocalDate)` | Lấy log của 1 habit trong 1 ngày |
| `upsertLog(DailyLog)` | INSERT hoặc UPDATE log (toggle completed) |
| `getAllLogsForHabit(int habitId)` | Lấy toàn bộ lịch sử 1 habit → dùng tính streak |
| `deleteLogsForHabit(int habitId)` | Xóa tất cả log khi xóa habit |

---

### 🟠 Tầng Service (Business Logic)

Lớp trung gian xử lý nghiệp vụ, gọi DAO và trả kết quả cho UI.

#### `CategoryService`
```
Package : com.dailytracker.service
Phụ thuộc : CategoryDao
```
- Validate dữ liệu category trước khi lưu (tên không rỗng, màu hợp lệ)
- Bọc `CategoryDao` để UI không gọi DAO trực tiếp

#### `HabitService`
```
Package : com.dailytracker.service
Phụ thuộc : HabitDao, DailyLogDao
```
**Chức năng quan trọng:**
- Thêm/sửa/xóa habit qua `HabitDao`
- Toggle completion: gọi `DailyLogDao.upsertLog()` với ngày hiện tại
- **Tính Streak** từ `DailyLog`:
  - Lấy toàn bộ log → sort theo ngày giảm dần
  - Đếm chuỗi ngày `completed = true` liên tiếp từ hôm nay → `currentStreak`
  - Tìm chuỗi dài nhất trong toàn bộ lịch sử → `longestStreak`
  - Tổng số ngày đã completed → `totalCompleted`
- Trả về `StreakStats` cho UI hiển thị

---

### 🔴 Tầng UI (JavaFX Views)

#### `MainView`
```
Package : com.dailytracker.ui
Vai trò : Shell chính — sidebar + content area
```
- Dựng layout `BorderPane`: sidebar (trái) + content area (giữa)
- Sidebar có 3 nút điều hướng: **📋 Today**, **⚙️ Habits**, **📊 Analytics**
- Quản lý việc chuyển đổi giữa các View (replace content area)
- Giữ trạng thái nút nav active (CSS class `.nav-button-active`)

#### `TodayView`
```
Package : com.dailytracker.ui
Vai trò : Màn hình chính — danh sách habit hôm nay
```
- Hiển thị ngày tháng hiện tại (tiêu đề lớn)
- **Summary card**: motivational quote + thanh progress bar (% habits đã xong)
- **Filter pills**: All / lọc theo từng Category
- **Danh sách HabitCard**: scroll theo chiều dọc
- Refresh tự động sau mỗi lần toggle completion

#### `HabitManagementView`
```
Package : com.dailytracker.ui
Vai trò : Quản lý CRUD Habits và Categories
```
- Form thêm/sửa habit: TextField tên, TextArea mô tả, ComboBox chọn Category
- Danh sách habits hiện có với nút Edit / Delete
- Section quản lý Category: thêm tên + chọn màu, xóa category
- Validation input trước khi lưu

#### `AnalyticsView`
```
Package : com.dailytracker.ui
Vai trò : Dashboard thống kê
```
- **3 KPI Cards**:
  - 📌 Total Habits (tổng số habit)
  - 🔥 Best Streak (streak cao nhất trong tất cả habits)
  - ✅ Today's Rate (% hoàn thành hôm nay)
- **Bảng streak**: liệt kê từng habit với current streak và longest streak

#### `HabitCard` *(Component)*
```
Package : com.dailytracker.ui.components
Vai trò : UI component tái sử dụng cho 1 habit trong danh sách
```
- Hiển thị: Tên habit, mô tả, tag danh mục (có màu), streak badge (🔥 N days)
- **Check circle button**: click để toggle completed/uncompleted
- Thay đổi style khi completed (`.habit-card-completed`, tiêu đề mờ đi)
- Nhận callback `onToggle` từ `TodayView` để cập nhật UI sau khi toggle

---

## 🏗️ Sơ đồ kiến trúc

```
┌─────────────────────────────────────────────────┐
│                 DailyTracker.exe                 │
│              (jpackage launcher)                  │
└──────────────────────┬──────────────────────────┘
                       │ loads JVM → runtime/bin/server/jvm.dll
                       ▼
┌─────────────────────────────────────────────────┐
│          Launcher  ──►  App (JavaFX)             │
└──────────────────────┬──────────────────────────┘
                       │
          ┌────────────▼────────────┐
          │        MainView         │  ← Shell (Sidebar + Content)
          └────────────┬────────────┘
         ┌─────────────┼─────────────┐
         ▼             ▼             ▼
    TodayView  HabitMgmtView  AnalyticsView
         │             │             │
         ▼             │             │
    HabitCard          │             │
    (component)        │             │
                       │             │
         ════════ SERVICE LAYER ══════════════
         │             │             │
         └──────►  HabitService ◄───┘
                  CategoryService
                       │
         ════════ DAO LAYER ══════════════════
                       │
         ┌─────────────┼─────────────┐
         ▼             ▼             ▼
    HabitDao      DailyLogDao   CategoryDao
                       │
                 DatabaseManager
                       │
              [daily_tracker.db]  ← SQLite file
              ┌────────────────┐
              │  categories    │
              │  habits        │
              │  daily_logs    │
              └────────────────┘
```

---

## 📦 Dependencies

| Thư viện | Phiên bản | Giấy phép | Mục đích |
|---|---|---|---|
| `javafx-controls` | 21.0.5 | GPL v2 + CE | UI Controls |
| `javafx-graphics` | 21.0.5 | GPL v2 + CE | Rendering engine |
| `sqlite-jdbc` (org.xerial) | 3.47.0.0 | Apache 2.0 | SQLite driver |
| `slf4j-simple` | 2.0.16 | MIT | Logging |

---

## 🗃️ Database Schema

File database SQLite được tạo tự động tại thư mục làm việc khi chạy app lần đầu:

```
DailyTracker\
└── daily_tracker.db    ← Tạo tự động, chứa toàn bộ dữ liệu
```

```sql
CREATE TABLE categories (
    id    INTEGER PRIMARY KEY AUTOINCREMENT,
    name  TEXT    NOT NULL,
    color TEXT    NOT NULL DEFAULT '#38bdf8'
);

CREATE TABLE habits (
    id          INTEGER PRIMARY KEY AUTOINCREMENT,
    name        TEXT    NOT NULL,
    description TEXT,
    category_id INTEGER REFERENCES categories(id),
    created_at  TEXT    NOT NULL
);

CREATE TABLE daily_logs (
    id        INTEGER PRIMARY KEY AUTOINCREMENT,
    habit_id  INTEGER NOT NULL REFERENCES habits(id),
    date      TEXT    NOT NULL,
    completed INTEGER NOT NULL DEFAULT 0,
    UNIQUE(habit_id, date)
);
```

---

## 🔧 Build từ Source

### Yêu cầu
- JDK 21 (khuyến nghị [Eclipse Temurin 21](https://adoptium.net/))
- Apache Maven 3.8+

### Các lệnh Maven

```powershell
# Chạy trong quá trình phát triển
mvn javafx:run

# Build Fat JAR
mvn clean package
# Output: target/daily-tracker-1.0.0.jar

# Tạo native package (cần JDK có jpackage)
jpackage `
  --input target/ `
  --name DailyTracker `
  --main-jar daily-tracker-1.0.0.jar `
  --main-class com.dailytracker.Launcher `
  --type app-image `
  --dest output/
```

---

## ❓ Troubleshooting

| Vấn đề | Nguyên nhân | Giải pháp |
|---|---|---|
| App không hiện gì khi click `.exe` | Đường dẫn chứa ký tự Unicode/tiếng Việt | Di chuyển thư mục ra `D:\DailyTracker\` |
| App crash khi khởi động | Java hệ thống xung đột với bundled JVM | Chạy thẳng `.exe` thay vì dùng `java -jar` |
| Màn hình trắng/đen | Lỗi load JavaFX native DLL | Đảm bảo thư mục `runtime\bin\` còn đầy đủ DLL |
| Database không lưu | Không có quyền ghi vào thư mục | Chạy từ thư mục có quyền write (không dùng `C:\Program Files\`) |

---

*Phiên bản: 1.0.0 — Java 21 + JavaFX 21.0.5 + SQLite 3.47.0*
