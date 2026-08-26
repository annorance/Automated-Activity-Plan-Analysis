# 📘 **Automated Annual Activity Plan Analysis**

*Transforming manual spreadsheet processing into a fully automated multi-department analytical pipeline*

## 🚀 Overview

The **Automated Annual Activity Plan Analysis** project was built to replace the manual process of merging, cleaning, analyzing, and reporting the *Annual Activity Plan* across departments.

Previously, the team had to:

* open multiple Google Sheets files,
* merge data manually,
* calculate totals for activities, initiatives, and KMI/KSI categories,
* build charts one by one,
* compile reports manually.

Through an **n8n** workflow leveraging various nodes such as OpenAI, JavaScript, and QuickChart, the entire process now runs **100% automatically** with just a single click ("Execute Workflow").

---

## 🎯 **Key Features**

### 1. **Multi-Sheet Data Aggregation**

* The workflow pulls data from various Activity Plan drafts across departments

* Each file is retrieved using a **Google Sheets node** and combined through a **Merge** node.

### 2. **Automatic Data Cleaning & Normalization**

The pipeline performs:

* cleaning of the target sheet before rewriting,
* column normalization (e.g., mapping DIC/QAC/WHS/HCD),
* re-numbering of activity candidates (`Node 2: Number Formatting`).

### 3. **Automated Master Sheet Generation**

All activities across departments are consolidated into a single master sheet:
`Node A: Append row in Merged Sheet`.

### 4. **Analytical Modules (Multiple Code Nodes)**

The pipeline generates various automated analyses, including:

* **Activities and Initiatives per DIC**
* **Focus Theme per DIC**
* **KMI & KSI and Dimension Mapping**
* **Collaboration Culture Mapping**
* **Support Contribution Analysis**
* **Budget Resource Distribution** (CAPEX / Department / Not Use Budget)
* **Duplicated Activities Detection**
* **Automated QCDSME Classification**
* **Activity Breakdown by Weight & Category**
* **Activity Count by Weight per Month & Automated Busyness per Month Detection**

How does it work?
* Each analysis is calculated through custom JavaScript inside **Code** nodes, using complex aggregation, grouping, and counting logic.
* Analyses on data containing **large volumes of text data**, such as detecting duplicate activities across departments and QCDSME classification, are performed using a **ChatGPT model** via an **OpenAI node**.

### 5. **Automatic Chart Generation (QuickChart API)**

The workflow automatically builds:

* Pie charts,
* Bar charts (Activities & Initiatives per DIC),
* Support contribution distribution charts.

All charts are generated dynamically through **QuickChart**, with automatic configuration including labels, department colors, the datalabels plugin, and scaling.

### 6. **HTML Report Composer**

Several nodes such as:

* `Container of E.2.1`,
* `Container of F3`,
* `Container of G3`,
* `Container of I`,
* `Node J.1`,
* `Node J.2`,
* `Merge All Analyses`

… work together to generate a **complete HTML report** containing tables and charts ready to be sent.

### 7. **Email Delivery Automation**

The final result is sent automatically via Gmail:

* Subject: *tes automated activity plan*
* Body: full HTML report containing all analyses.

---

## 🧩 **Workflow Architecture (High-Level)**

Below is the workflow reconstructed from the JSON file:

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

| Component                         | Technology                  |
| --------------------------------- | -------------------------- |
| Workflow Orchestrator             | **n8n**                    |
| Data Source                       | **Google Sheets API**      |
| Transformation Logic              | JavaScript (n8n Code Node) |
| AI Text Analysis                  | **ChatGPT API**       |
| Chart Rendering                   | **QuickChart.io**          |
| Report Format                     | HTML (inline CSS)          |
| Delivery                          | Gmail Node (OAuth2)        |

---

## 📊 **Sample Output (Summary of Insights)**

The workflow automatically generates:

* charts of the number of activities & initiatives per department,
* distribution of dominant themes,
* comparison of KSI vs KMI,
* collaboration relationships between departments,
* cross-department support needs,
* budget allocation distribution across CAPEX vs Department vs Not Use Budget.
* automatic detection of duplicated activities across departments
* automatic QCDSME classification for each activity plan
* activity breakdown by weight and category, as well as total weight per month, which is then used to report the busiest month and the least busy month

All charts and tables are sent directly via email without any manual editing.

---

## 🤖 **Why This Automation Matters**

Before automation, the Activity Plan analysis process for 8–10 departments took:

* ≥ **8 hours of work**
* High risk of human error
* Difficulty maintaining report consistency

With this pipeline, processing time has dropped to:

### **3–5 minutes → a complete, ready-to-send report**

No more manual merging, chart editing, or copy-pasting.

---

## 📩 **How to Run**

1. Open the workflow in n8n.
2. Click **Execute Workflow**.
3. The complete report is automatically sent to the destination email.

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

This pipeline was built with the aim of helping the management team and related departments compile the Activity Plan more consistently, quickly, and accurately.
Contributors: the Manufacturing, Development and Planning Department that developed the workflow, and the Annual Plan 2026 Committee Team who provided input during development — PT Kalbe Morinaga Indonesia.
