# TechPathAI iOS App (MVP)

TechPathAI helps computer science students and new grads build a **personalized weekly routine** and **interview prep plan** using OpenAI — all while keeping data 100% local to the device.  

The backend is a lightweight Node.js API that simply forwards structured prompts to OpenAI.  
No accounts, no cloud, no data storage.

---

## 🧠 MVP Overview

**Goal:**  
Generate a Monday–Friday routine and interview prep plan in under two minutes.  
All data stays **on the user’s device**.

**Stack:**
- **Frontend:** Swift / SwiftUI  
- **Backend:** Node.js + Express  
- **Storage:** Local JSON files (no database)  
- **AI:** OpenAI API  

---

## ✨ Core Features

### 1. Onboarding & Profile  
Users enter:
- Name  
- Stage (e.g. “2nd Year”, “Recent Grad”)  
- Target role (e.g. “iOS SWE”)  
- Time budget (hours per day)  
- Available days and constraints  

Saved locally as `profile.json`.

---

### 2. Generate Routine  
Tap **Generate Plan** → calls backend → OpenAI returns structured JSON:
- Time-boxed blocks (Mon–Fri)
- Daily tasks  
- Weekly milestones  
- Recommended resources  

Saved locally as a versioned file (`plan_YYYY-MM-DD.json`).

---

### 3. Daily Checklist  
View “Today” tab → see tasks → mark **Done / Skipped**.  
Progress + streak saved to `progress.json`.

---

### 4. Interview Prep Pack  
One-tap generation of:
- Topic ladder (DS&A, iOS, systems)  
- Weekly drill plan  
- Starter questions  
- Resource links  

---

### 5. Quick Re-Rolls  
Regenerate only parts of your plan (e.g., time blocks or resources)  
without deleting your whole week.

---

## 🧩 Architecture

### iOS (Swift / SwiftUI)
- Tabs: **Onboarding**, **Week**, **Today**, **Prep**, **Settings**
- Stores JSON in app’s local Documents folder  
- `UserDefaults` for small preferences  
- Optional Keychain storage for user’s API key  

### Node.js (Express)
- **Stateless backend**
- Endpoints:
  - `POST /generate/routine`
  - `POST /generate/prep`
  - `POST /reroll/:section`
- Each route builds a JSON-based prompt and calls OpenAI.

---

## 🗂️ Example Data

**`profile.json`**
```json
{
  "name": "Andrew",
  "stage": "recent_grad",
  "targetRole": "iOS Software Engineer",
  "timeBudgetHoursPerDay": 3,
  "availableDays": ["Mon", "Tue", "Wed", "Thu", "Fri"],
  "constraints": ["no weekends"],
  "updatedAt": "2025-10-06T21:00:00Z"
}
