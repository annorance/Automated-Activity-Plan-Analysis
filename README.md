# 📘 **Automated Activity Plan Analysis**

*Transforming manual spreadsheet processing into a fully automated multi-department analytical pipeline*

## 🚀 Overview

Proyek **Automated Activity Plan Analysis** dibangun untuk menggantikan proses manual dalam menggabungkan, membersihkan, menganalisis, dan melaporkan *Activity Plan* lintas departemen (PRD, ENG, BDA, WH, QA, IOS, HCD, MDP, dll).

Sebelumnya, tim harus:

* membuka banyak file Google Sheets,
* menggabungkan data secara manual,
* menghitung total activity, initiative, kategori KMI/KSI,
* membuat chart satu per satu,
* menyusun laporan secara manual.

Melalui workflow **n8n**, seluruh langkah tersebut sekarang berlangsung **otomatis 100%** hanya dengan satu klik (“Execute Workflow”).

---

## 🎯 **Key Features**

### 1. **Multi-Sheet Data Aggregation**

Workflow menarik data dari berbagai Activity Plan draft per departemen:

* PRD, ENG, BDA, QA/QAC, WH, IOS, HCD, MDP, dll.
  Setiap file diambil menggunakan **Google Sheets node** dan disatukan melalui node **Merge**.

### 2. **Automatic Data Cleaning & Normalization**

Pipeline melakukan:

* pembersihan sheet target sebelum menulis ulang,
* normalisasi kolom (misal mapping DIC/QAC/WHS/HCD),
* penomoran ulang kandidat activity (`Node 2: Number Formatting`).

### 3. **Automated Master Sheet Generation**

Seluruh activity lintas departemen disatukan ke dalam satu master sheet:
`Node A: Append row in Merged Sheet`.

### 4. **Analytical Modules (Multiple Code Nodes)**

Pipeline menghasilkan berbagai analisis, antara lain:

* **Activities per DIC**
* **Initiatives per DIC**
* **Focus Theme per DIC**
* **KMI & KSI and Dimension Mapping**
* **Collaboration Culture Mapping**
* **Support Contribution Analysis**
* **Budget Resource Distribution** (CAPEX / Department / Not Use Budget)

Setiap analisis dihitung melalui custom JavaScript di dalam node **Code**, menggunakan logic agregasi, grouping, dan counting yang kompleks.

### 5. **Automatic Chart Generation (QuickChart API)**

Workflow secara otomatis membangun:

* Pie charts,
* Bar charts (Activities & Initiatives per DIC),
* Support contribution distribution charts.

Semua chart dibuat secara dinamis melalui QuickChart dengan konfigurasi otomatis termasuk label, warna departemen, datalabels plugin, dan scaling.

### 6. **HTML Report Composer**

Beberapa node seperti:

* `Container of E.2.1`,
* `Container of F3`,
* `Container of G3`,
* `Container of I`,
* `Node J.1`,
* `Node J.2`,
* `Merge All Analyses`

… bekerja sama menghasilkan **laporan HTML lengkap** yang berisi tabel dan chart siap kirim.

### 7. **Email Delivery Automation**

Hasil akhir dikirim otomatis via Gmail:

* Subject: *tes automated activity plan*
* Body: full HTML report dengan seluruh analisis.

---

## 🧩 **Workflow Architecture (High-Level)**

Berikut alur kerja yang direkonstruksi dari file JSON:


```
1. Manual Trigger
2. Fetch Activity Plan Sheets (9+ departments)
   └─ Google Sheets Nodes
3. Merge all department sheets → one unified dataset
4. Clear master sheet → append cleaned merged data
5. Data normalization:
   └─ Re-number rows
   └─ Normalize DIC mapping
6. Analytical Modules:
   ├─ Activities per DIC
   ├─ Initiatives per DIC
   ├─ Theme Focus per DIC
   ├─ KMI/KSI Dimension Mapping
   ├─ Collaboration Network Analysis
   ├─ Support Contribution (Supporter → Core)
   └─ Budget Resource Distribution
7. Chart Generation (QuickChart.io)
8. HTML Report Builder (multiple containers)
9. Merge All Analyses into a Final Report
10. Gmail Automation → Send HTML report
```

---

## 🏗️ **Technical Stack**

| Komponen              | Teknologi                  |
| --------------------- | -------------------------- |
| Workflow Orchestrator | **n8n**                    |
| Data Source           | **Google Sheets API**      |
| Transformation Logic  | JavaScript (n8n Code Node) |
| Chart Rendering       | **QuickChart.io**          |
| Report Format         | HTML (inline CSS)          |
| Delivery              | Gmail Node (OAuth2)        |

---

## 📊 **Sample Output (Summary of Insights)**

Workflow menghasilkan otomatis:

* chart jumlah activities & initiatives per department,
* distribusi tema dominan,
* perbandingan KSI vs KMI,
* hubungan kolaborasi antar departemen,
* kebutuhan support lintas departemen,
* distribusi alokasi budget CAPEX vs Dept vs Not Use Budget.

Semua diagram dan tabel langsung dikirim via email tanpa editing manual.

---

## 🤖 **Why This Automation Matters**

Sebelum otomatisasi, proses analisis Activity Plan untuk 8–10 departemen memakan:

* ≥ **8 jam kerja**
* Risiko tinggi human error
* Konsistensi laporan sulit dijaga

Dengan pipeline ini, waktu pemrosesan turun menjadi:

### **3–5 menit → seluruh laporan lengkap siap dikirim**

Tidak ada lagi merging manual, editing chart, atau copy-paste.

---

## 📩 **How to Run**

1. Buka workflow di n8n.
2. Klik **Execute Workflow**.
3. Laporan lengkap otomatis dikirim ke email tujuan.

---

## 🧱 Folder Structure (Recommended)

```
/project-root
  ├── README.md
  ├── workflow/
  │    └── automated_activity_plan_analysis.json
  ├── docs/
  │    ├── architecture.png
  │    └── sample_report.html
  └── charts/
       └── examples.png
```

---

## 🙌 Acknowledgements

Pipeline ini dibangun dengan tujuan membantu tim manajemen dan departemen terkait dalam menyusun Activity Plan yang lebih konsisten, cepat, dan akurat.
Kontributor: Departemen Manufacturing, Development and Planning yang Mengembangkan Workflow & Tim Panitia Annual Plan 2026 yang memberikan masukan selama pengembangan — PT Kalbe Morinaga Indonesia.
