# 🏥 SENTINEL ICU: AI Vital-Stack Intelligence System

> **Data Structures & Algorithms (DSA) Project:** A real-time, 50-bed ICU monitoring system built to demonstrate advanced LIFO Stack operations (Push, Pop, Peek) and differential trend analysis for early patient crash detection.

---

## 📌 Overview

High-acuity medical environments generate massive streams of physiological data. Traditional monitoring systems often focus on instantaneous values, missing the critical context provided by temporal trends. 

**SENTINEL ICU** solves this by managing live data for 50 beds simultaneously using custom Stack data structures. The system prioritizes recent data (LIFO), handles memory constraints through automated cleanup, and provides early warning alerts based on rate-of-change mathematics.

---

## 📸 Application Screenshots

<img width="960" height="503" alt="Screenshot 2026-10-26 194110" src="https://github.com/user-attachments/assets/ee51ed4d-bc18-4195-8be3-68ed3f005458" />
<img width="960" height="500" alt="Screenshot 2026-10-26 194129" src="https://github.com/user-attachments/assets/adf90dbb-48cd-4e97-8e83-fa2b96d68924" />
<img width="960" height="499" alt="Screenshot 2026-10-26 194202" src="https://github.com/user-attachments/assets/062076ad-a0c2-41a7-a7c6-cd1ca7ebacad" />

---

## 🧠 Core Data Structure: `VitalStack` (LIFO)

The system relies on a custom `VitalStack` implementation to manage patient medical snapshots (Timestamp, HR, BP, SpO2). It explicitly showcases three distinct clinical scenarios for the **POP** operation:

1. **Auto-POP (Memory Management):** Prevents crashes by acting as a circular buffer. If the stack size exceeds 100, it automatically triggers `pop_oldest()` to remove stale data.
2. **Manual POP (Correction):** Standard `pop()` removal of the most recent erroneous reading from the top of the stack.
3. **Bulk POP (Patient Discharge):** Utilizes `pop_all()` to completely clear the stack and free up resources, resetting the bed to a "VACANT" state.

### 📈 Differential Trend Analyzer (`PEEK`)
The system utilizes the `peek(offset)` operation to access the top 3 readings without destroying the stack. If the heart rate drops by $\ge10\%$ across consecutive readings, the system bypasses standard warnings and triggers a **PRE-CRASH ALERT**.

---

## ⚙️ System Architecture & Logic Flow

```text
 1. DATA INGESTION   ──► Sensor pushes `MedicalSnapshot` (HR, BP, SpO2, Time).
 2. STACK UPDATE     ──► `stack.push(snapshot)` adds data to TOP.
 3. CAPACITY CHECK   ──► IF `stack.size > 100` ──► `stack.pop_oldest()` (Memory Safe).
 4. TREND ANALYSIS   ──► `analyzer.peek(3)` evaluates % change in vital signs.
 5. VISUALIZATION    ──► Flask Frontend polls API to update 50-Bed Grid & Stack Viz.
 6. DISCHARGE        ──► `stack.pop_all()` resets Bed to VACANT.
```

---

## 📂 Repository File Structure

```text
SENTINEL_ICU_VitalStack/
│
├── ICU_Vitals_Stack.ipynb           # Main Colab Notebook (Flask backend + UI + ngrok)
├── README.md                        # Project documentation
└── LICENSE                          # MIT Open Source License
```

*(Note: Patient vitals are generated dynamically in real-time during simulation via Gaussian random walks, so no static CSV datasets are required in this repository).*

---

## 🚀 Quickstart & Deployment

This application is designed to run seamlessly in **Google Colab** with a Flask backend exposed via ngrok.

1. Open `ICU_Vitals_Stack.ipynb` in Google Colab.
2. Run **Cell 1** to install dependencies (`flask`, `flask-cors`, `pyngrok`).
3. Run **Cell 2 & 3** to initialize the HTML templates and the 50-bed ICU Ward.
4. Add your free ngrok token in **Cell 4** and execute it to launch the live web dashboard.

---

## 👥 Authors & Collaborators

* **Srushti Lambdade** (PRN: 25030421021) 
* **Sanobar Shaikh** (PRN: 25030421039) 
* **Prajakta Suryavanshi** (PRN: 25030421029) 

**Program:** B.Sc. Artificial Intelligence (Academic Year 2025-2026)  
**Institution:** Symbiosis Artificial Intelligence Institute (SAII, SIU Pune)  
**Project Guide:** Dr. Priti Kulkarni  

---

## ⚠️ Academic Disclaimer
This system was developed as a 1st-year Data Structures & Algorithms (DSA) academic project. Vitals are generated using Gaussian random walks for simulation purposes. It is **not** intended for actual clinical deployment.
