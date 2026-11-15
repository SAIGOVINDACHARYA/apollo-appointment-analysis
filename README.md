# 🏥 Apollo Hospital Appointment Analysis

> Exploratory data analysis of **75,000 hospital appointments (2022–2024)** to understand patient attendance, no-show behaviour, reminder effectiveness, revenue impact and doctor utilisation.

![Python](https://img.shields.io/badge/Python-3.9%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-data%20analysis-150458)
![Seaborn](https://img.shields.io/badge/Seaborn-visualisation-4c72b0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626)

---

## 📌 Business Problem

Hospitals lose revenue and capacity when patients miss appointments (no-shows), cancel late or wait too long. This project analyses Apollo appointment data to find **who misses appointments, when and why**, how much revenue is at risk, and which interventions (such as reminders) work best.

## 🎯 Objectives

1. Analyse appointment volume and outcomes over time.
2. Identify specialties, cities, booking patterns and patient groups with higher no-show rates.
3. Evaluate the effect of reminders and previous attendance behaviour on no-shows.
4. Estimate revenue lost to no-shows and study payment / insurance patterns.
5. Assess doctor utilisation, waiting time, consultation duration and satisfaction.

## 🗂️ Dataset

| File | Rows | Description |
|---|---|---|
| `apollo_appointments_fact.csv` | 75,000 (54 columns) | One row per appointment: patient, doctor, date/time, booking channel, status, reminder type, revenue, wait time, satisfaction, etc. |
| `apollo_doctors_dim.csv` | 320 (15 columns) | Doctor details: specialty, experience, consultation fee, city, rating, etc. |

> The CSV files are **not included** in this repository. See [`data/README.md`](data/README.md) for where to place them.

## 🛠️ Tools Used

- **Python** – analysis
- **Pandas / NumPy** – cleaning, aggregation, pivot tables
- **Matplotlib / Seaborn** – visualisation
- **Jupyter Notebook** – reporting

## 📁 Repository Structure

```
apollo-appointment-analysis/
├── Apollo_Appointment_Analysis.ipynb   # Full analysis with outputs
├── README.md
├── requirements.txt
├── LICENSE
├── .gitignore
├── data/
│   └── README.md                       # Put the two CSV files here
└── images/                             # Chart previews used in this README
```

## ▶️ How to Run

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/apollo-appointment-analysis.git
cd apollo-appointment-analysis

# 2. (Optional) create a virtual environment
python -m venv venv
venv\Scripts\activate          # Windows
# source venv/bin/activate     # macOS / Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Add the two CSV files to the data/ folder, then start Jupyter
jupyter notebook Apollo_Appointment_Analysis.ipynb
```

---

## 📊 Key Findings

### 1. Overview
- **75,000** appointments from **32,705** unique patients.
- **73.70%** completed, **15.45%** no-show (11,584), **7.72%** cancelled (5,793) and **3.13%** still scheduled.
- Volume is stable at roughly **25,000 appointments per year** (24,868 in 2022, 25,054 in 2023, 25,078 in 2024).
- Demand is **seasonal**: Q4 is the busiest quarter every year (up to 6,746 in 2023 Q4) and Q3 the quietest (lowest: 5,852 in 2023 Q3). The busiest month is December 2023 (2,342).

![Monthly volume](images/01_monthly_volume.png)
![Appointment outcomes](images/03_appointment_outcomes.png)

### 2. No-show analysis
| Factor | Higher risk | Lower risk |
|---|---|---|
| **Specialty** | Psychiatry **24.5%**, Dermatology **21.3%**, ENT **19.0%** | Neurology **10.7%**, Paediatrics **12.2%**, Cardiology **14.0%** |
| **Booking lead time** | 15–30 days: **20.0%**, 8–14 days: **18.8%** | 0–1 days: **13.2%** |
| **Time of day** | Evening **18.4%**, Afternoon **17.8%** | Morning **13.7%** |
| **Day type** | Weekend **18.7%** | Weekday **14.8%** |
| **Booking channel** | Walk-In **20.9%**, Partner App **18.1%** | Apollo App **14.2%** |
| **Appointment type** | Home Visit (~26%), Video Consult (~21%) | In-Clinic (~12%) |
| **Prior history** | Previous no-show: **20.6%** | No previous no-show: **15.6%** |

- No-show probability **rises steadily as the booking gap grows** (13.2% → 15.8% → 18.8% → 20.0%).
- A patient who has missed an appointment before is about **5 percentage points** more likely to miss again.
- By city, Lucknow, Mumbai and Delhi are at the top (about 17%) and Pune is the lowest (about 13%).

![No-show by specialty](images/05_noshow_by_specialty.png)
![Timing patterns](images/06_noshow_timing_patterns.png)

### 3. Reminder effectiveness ⭐
Reminders are the strongest lever found in this analysis.

| Reminder type | No-show rate | Reduction vs no reminder |
|---|---|---|
| No reminder | **30.16%** | – |
| SMS only | 16.27% | −13.90 pp (≈46% lower) |
| SMS + WhatsApp | 13.51% | −16.65 pp (≈55% lower) |
| SMS + WhatsApp + Call | **11.41%** | **−18.75 pp (≈62% lower)** |

![Reminder effectiveness](images/08_reminder_effectiveness.png)

### 4. Patient segmentation
- **Repeat patients** miss far fewer appointments (**8.6%**) than first-time patients (**66.8%**).
- Adults aged 19–45 have the highest no-show rate (about 18%); children (0–12) and seniors (60+) have the lowest (about 13.5% and 14%).
- **Gender** (≈16% for both) and **chronic condition** (≈15.5%–16.7%) show little difference.
- Visit reasons all fall in a narrow band (about 15.6%–16.8%), with Skin Issue the highest.

![Demographics](images/09_demographics.png)

### 5. Financial performance
- Average revenue per completed appointment ≈ **₹1,337**.
- Estimated revenue lost to no-shows ≈ **₹1.55 crore (₹15,485,948)**.
- **Bengaluru (₹99.9 lakh), Delhi (₹99.6 lakh) and Mumbai (₹89.9 lakh)** generate the most revenue, together about **39%** of the total (₹7.39 crore).
- Patients **with insurance pay about 43% less** out of pocket (₹649 vs ₹1,138 on average).

![Revenue loss](images/10_revenue_loss.png)
![Insurance](images/12_insurance_out_of_pocket.png)

### 6. Doctor utilisation & service quality
- **General Physician** handles the most appointments (20,272, about 27%), followed by Dermatology (7,824) and Paediatrics (6,382). Endocrinology is lowest (2,087).
- **Waiting time is similar everywhere**, around 11–12.5 minutes across specialties and time slots.
- **Consultation duration has no relationship with patient satisfaction** (correlation ≈ 0.0).
- **Doctor fees rise with experience**: roughly ₹1,300 at 2 years versus ₹2,000–2,300 at 25–31 years.

![Specialty volume](images/13_specialty_volume.png)
![Experience vs fee](images/15_experience_vs_fee.png)

---

## 💡 Recommendations

1. **Make multi-channel reminders the default.** SMS + WhatsApp + Call cuts no-shows by about 62% compared with no reminder.
2. **Target high-risk slots**: evening, weekend and long-lead-time bookings can get an extra reminder, a confirmation request or a small overbooking buffer.
3. **Focus on high-risk specialties** (Psychiatry, Dermatology, ENT) and on Walk-In, Home Visit and Video Consult bookings.
4. **Flag patients with a previous no-show** for proactive follow-up.
5. **Convert first-time patients into repeat patients** (follow-up reminders, membership offers), as they are the group most likely to miss.
6. **Encourage insurance-backed bookings**, as they reduce the patient's out-of-pocket cost.

## ⚠️ Notes & Limitations

- This is an **observational analysis**: the patterns show association, not proven cause and effect.
- The revenue-loss figure is an **estimate** (average revenue of completed visits × number of no-shows).
- The "More than 30 days" lead-time group has **no eligible appointments** in the data.
- The very large gap between repeat and first-time patients (8.6% vs 66.8%) should be checked against how `repeat_visit` is defined before drawing strong conclusions.
- No-show rates are calculated on **Completed, No-Show and Cancelled** appointments only (scheduled appointments are excluded).

## 👤 Author

**Your Name**
📧 your.email@example.com · 🔗 [LinkedIn](https://www.linkedin.com/in/your-profile) · 💻 [GitHub](https://github.com/your-username)

## 📄 License

This project is licensed under the MIT License – see the [LICENSE](LICENSE) file.
