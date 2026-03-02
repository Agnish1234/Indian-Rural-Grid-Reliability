# Distributed Battery Storage for Rural Grid Reliability in India

---

## 🧠 Overview

Millions of people in rural India face frequent power outages. When the grid fails, households and small businesses often rely on expensive and polluting diesel generators. This project explores a cleaner alternative: **distributed battery storage**.

Using computer simulations, I built a model that mimics real‑world conditions in three typical rural feeders. The goal was to answer a simple but critical question:  

> *How much does a battery improve reliability, and what size gives the best value for money?*

The results are now being prepared for publication in a research journal. Meanwhile, all code, data, and visualizations are available here for anyone to explore, reuse, or build upon.

---

## 🔍 The Problem

- **Unreliable grid**: Rural areas experience several outages per month, each lasting hours.
- **Costly backup**: Diesel generators are expensive to run and harmful to the environment.
- **Uncertain sizing**: There is little data on how much battery capacity is actually needed to make a difference.

---

## 💡 The Solution

I developed a **Monte Carlo simulation** – a method that runs thousands of “what‑if” scenarios – to capture the randomness of both electricity demand and outages. For each scenario, the model:

1. Generates a realistic 30‑day pattern of household electricity use.
2. Randomly inserts outages based on local statistics.
3. Simulates a battery that discharges during outages and recharges when the grid is up.
4. Records how much energy the battery saves (the **reliability gain**) and how much diesel it displaces.

The simulation was repeated for **9 different battery sizes and power ratings**, using **2,500 random scenarios** for each – that’s over 22,000 individual simulations. To ensure a fair comparison, every battery configuration faced exactly the same set of outage patterns (a technique called **common random numbers**).

All results are presented with **95% confidence intervals**, so you can see not only the average benefit, but also how much it might vary in real life.

---

## 📊 Key Findings

- **Reliability gains increase with battery size**, but the extra benefit per kilowatt‑hour shrinks rapidly beyond 50 kWh.  
  - A 25 kWh battery provides ~63 kWh of backup energy per month.  
  - Doubling the capacity to 50 kWh adds only ~5 kWh more.  
  - Going to 75 kWh adds just another 2–3 kWh.  

  This **diminishing return** is a crucial insight for planners: the first 50 kWh delivers the most value.

- **Higher discharge power helps only for larger batteries**. For a 25 kWh battery, a 10 kW inverter is enough; for 75 kWh, a 20 kW or 30 kW inverter yields modest extra gains.

- **Diesel displacement is modest** – around 7–11 kWh per month – because the diesel generator is used only when the battery is empty. As battery size grows, diesel use drops slightly.

- **Feeder characteristics matter**. A quick check on two other feeders showed that the same battery can save anywhere from 61 to 85 kWh depending on local load and outage patterns. This highlights the need for targeted, site‑specific planning.

---

## ⚙️ Methodology (Made Simple)

1. **Load modeling**  
   I used publicly available Indian energy data to create a realistic daily demand shape, then added random noise to represent household‑level variation.

2. **Outage modeling**  
   Outages were randomly placed in time, with frequencies and durations matching typical rural data.

3. **Battery logic**  
   - During an outage: the battery discharges at its maximum power until empty.  
   - When the grid is on: the battery recharges at the same rate until full.  
   - Any demand not met by battery + grid is counted as **unserved energy**.  
   - If a diesel generator is available, it covers unserved energy up to 20 kW per hour.

4. **Uncertainty quantification**  
   Because outages are random, the results vary from one month to another. I ran **2,500 simulations** for every battery size and computed the **95% confidence intervals** – a statistical way to say: “We are 95% sure the true benefit lies within this range.”

5. **Fair comparison**  
   All batteries faced the **same 2,500 outage scenarios**, so any difference in results is purely due to the battery itself, not random luck.

---

## 🛠️ Tech Stack

- **Python** – core language  
- **NumPy / Pandas** – data handling and statistics  
- **Matplotlib / Seaborn** – publication‑ready visualisations  
- **Google Colab** – development and hosting (click the badge above to run)  
- **Monte Carlo methods** – stochastic simulation  
- **Uncertainty propagation** – 95% confidence intervals  

---


---

## 🔁 Reproducibility

Everything you need to reproduce the analysis is in the notebook. Just open it in Google Colab (click the badge above) and run all cells. The notebook:

- Sets a fixed random seed (`42`) so results are identical every time.
- Includes a fallback if the external energy dataset is unavailable.
- Saves all figures automatically.
- Prints a summary table with confidence intervals.

No additional installation is required – Colab comes with all necessary libraries.

---

## 📈 Results at a Glance

| Battery Capacity (kWh) | Max Power (kW) | Reliability Gain (kWh) | Diesel Displaced (kWh) |
|------------------------|----------------|------------------------|-------------------------|
| 25                     | 10             | 62.5 ± 14.3            | 11.2 ± 0.9              |
| 25                     | 20             | 62.6 ± 14.3            | 11.2 ± 0.9              |
| 25                     | 30             | 62.6 ± 14.3            | 11.3 ± 0.9              |
| 50                     | 10             | 67.1 ± 14.2            | 8.1 ± 0.9               |
| 50                     | 20             | 68.8 ± 14.1            | 7.6 ± 0.9               |
| 50                     | 30             | 68.8 ± 14.1            | 7.6 ± 0.9               |
| 75                     | 10             | 67.1 ± 14.2            | 8.0 ± 0.9               |
| 75                     | 20             | 70.9 ± 13.9            | 7.5 ± 0.9               |
| 75                     | 30             | 71.3 ± 13.9            | 7.5 ± 0.9               |

*Values are mean ± 95% confidence interval.*

---

## ⚠️ Limitations (Honest and Open)

- The analysis focuses on one feeder type; gains vary with local conditions (as shown in the multi‑feeder check).
- The battery charges at full power whenever the grid is up – this may overestimate recharge speed if the feeder itself is weak.
- Diesel backup is modelled as instantly available – real generators have ramp‑up delays and fuel constraints.
- The simulation covers a single month (March); results may differ in other seasons.

These limitations are clearly documented in the notebook and do not invalidate the main conclusions – they simply define the scope.

---

## 👤 Author

**Agnish Brahma**  
Independent researcher passionate about energy access, data science, and sustainable development.  

- This work was entirely self‑directed, so feel free to suggest any innovation.   
- Feedback, collaborations, and questions are very welcome.

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE). You are free to use, modify, and distribute the code with attribution.

---

## 📬 Contact

- GitHub:   
- Email: agnishbrahma2004@gmail.com  
- LinkedIn: 

---

**If you find this work useful, please star the repository – it helps others discover it!** ⭐
